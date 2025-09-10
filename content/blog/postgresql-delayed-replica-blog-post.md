# PostgreSQL Delayed Replicas: The Monitoring Nightmare That Woke Me Up at 1 AM

I recently spent a day debugging one of those wonderfully frustrating monitoring issues that makes you question everything you know about databases. What followed was a technical rabbit hole that led to some interesting discoveries about how PostgreSQL delayed replicas work and why they're basically designed to drive our monitoring systems into madness.

## The Problem

Our monitoring setup was generating critical alerts for PostgreSQL replication lag on what appeared to be perfectly healthy delayed replicas. These were database replicas purposefully configured with a 2-hour delay to assist in recovery scenarios.

The alert (`PostgresqlApplyLagBeyondDelay`) was designed to catch *apply* lag (ex. i/o can't keep up). 

## The Initial Confusion

What really threw me off initially was the pattern of these alerts. Intuitively, I thought: "If this was actually a replication issue, wouldn't we see the alert on the non-delayed hosts first, then see the same alert on the delayed hosts two hours later?" 

But that's not what was happening. The delayed replicas were the primary source of false positives, while their non-delayed counterparts stayed quiet. This didn't make sense until I understood the fundamental difference in how lag is calculated.

## Our PostgreSQL Monitoring Stack

To understand the fix, it helps to see the full context of our PostgreSQL replication monitoring. We have three alerts working together:

**Recording Rules:**
```promql

- record: pg:excess_time_lag_seconds
  expr: |
    clamp_min(
      pg_replication_lag_seconds
      - on(instance) pg_settings_recovery_min_apply_delay_seconds,
      0
    )
- record: pg:receiver_data_in_1m
  expr: increase(pg_stat_wal_receiver_latest_end_lsn[1m])

- record: pg:receiver_data_in_30m
  expr: increase(pg_stat_wal_receiver_latest_end_lsn[30m])

- record: pg:receiver_msg_age_seconds
  expr: time() - pg_stat_wal_receiver_last_msg_receipt_time
```

**PostgresqlApplyLagBeyondDelay (Critical):**
```promql
(pg:excess_time_lag_seconds > 300)
and on(instance) (pg:receiver_data_in_1m > 0)
```

**PostgresqlWalReceiverStalled (Critical):**
```promql
pg:receiver_msg_age_seconds > 120
```

**PostgresqlTimeLagWithoutInput (Warning):**
```promql
(pg:excess_time_lag_seconds > 1800)
and on(instance) (pg:receiver_data_in_30m == 0)
```

The `PostgresqlApplyLagBeyondDelay` alert was our problem child - firing away at the worst of times. Especially when I was sleeping peacefully!

## Down the PostgreSQL Rabbit Hole

After digging into the PostgreSQL documentation and postgres_exporter source code, I found the smoking gun. The lag calculation uses this query:

```sql
SELECT
    CASE
        WHEN NOT pg_is_in_recovery() THEN 0
        WHEN pg_last_wal_receive_lsn() = pg_last_wal_replay_lsn() THEN 0
        ELSE GREATEST(0, EXTRACT(EPOCH FROM (now() - pg_last_xact_replay_timestamp())))
    END AS lag
```

That last line is the key: `now() - pg_last_xact_replay_timestamp()`. This measures the time since the last COMMIT was replayed, not when it was received.

## The "Aha!" Moment

Here's where it gets interesting. For normal replicas:
- Transaction commits at 10:00 AM on primary
- Replica replays it immediately at 10:00 AM
- `pg_last_xact_replay_timestamp` = 10:00 AM
- Primary goes idle at 10:00 AM
- At 10:30 AM: lag = 0 seconds (because now `pg_last_wal_receive_lsn() == pg_last_wal_replay_lsn()`)

But for delayed replicas with a 2-hour delay:
- Transaction commits at 10:00 AM on primary
- Replica holds it until 12:00 PM, then replays it
- `pg_last_xact_replay_timestamp` = 10:00 AM (original commit time!)
- At 12:30 PM: lag = 2.5 hours = 1800s excess lag

Even though the delayed replica is completely caught up with everything it's allowed to replay, the lag metric keeps growing because it's measuring from the original transaction timestamp, not when the replica processed it.

This explains why delayed replicas were disproportionately affected. They start with a 2-hour-old timestamp and any idle period compounds on top of that existing delay, while non-delayed replicas only accumulate lag from the current moment. In other words, the delayed replicas will rarely hit this clause:
```sql
WHEN pg_last_wal_receive_lsn() = pg_last_wal_replay_lsn() THEN 0
```

The only time this would be true is if the primary was idle for >= 2 hours!

## The Sawtooth Pattern Finally Makes Sense

This discovery also explained the bizarre sawtooth pattern I'd been seeing in the replication lag graphs for delayed replicas, compared to the flat line of non-delayed replicas:

**Non-delayed replica lag pattern:**
```
Lag (seconds)
     ^
 300 |                                        
     |                                        
 200 |                                        
     |                                        
 100 |                                        
     |________________________________________>
   0                                        Time
     (stays at 0 when caught up)
```

**Delayed replica lag pattern:**
```
Lag (seconds)
     ^
9000 |                        /\
     |                       /  \
8000 |  ______        /\    /    \
     | /      \      /  \  /      \
7200 |/        \    /    \/        \
     |          \                   \
   0 |___________\___________________\________>
                                            Time
     (drops to 0 when caught up, jumps to 7200s with new WAL)
```

The delayed replica constantly cycles between "caught up" (0 lag) when it has no WAL old enough to replay, and "processing backlog" (growing from 7200s+) when new transactions become eligible.

## The Fix

The solution was to modify the alert logic so that it looked into WAL receiver activity 2 hours ago for the delayed replicas; instead of just checking "is WAL arriving now?" for both types of hosts.

**New Recording Rule:**
```promql
- record: pg:wal_activity_in_delay_window
  expr: |
    increase(
      pg_stat_wal_receiver_latest_end_lsn[1m] 
      offset 2h
    ) > 0
```

**Updated Alert Expression:**
```promql
(pg:excess_time_lag_seconds > 300)
and on(instance) (pg:receiver_data_in_1m > 0)
and on(instance) (
  # For non-delayed replicas - always alert (no additional conditions)
  (pg_settings_recovery_min_apply_delay_seconds == 0)
  or
  # For delayed replicas - only alert if there was WAL activity 2h ago
  (
    (pg_settings_recovery_min_apply_delay_seconds > 0)
    and on(instance)
    pg:wal_activity_in_delay_window
  )
)
```

The new logic:
- For normal replicas: Keep existing behavior (no change)
- For delayed replicas: Only alert if there was WAL activity 2 hours ago that should be available for replay

This prevents false positives during legitimate idle periods while still catching real apply stalls when there's actual work backing up.

## The Result

The fix eliminated the false positives while maintaining full coverage through layered monitoring:
- `PostgresqlApplyLagBeyondDelay`: Catches performance issues when there's actual work to do
- `PostgresqlWalReceiverStalled`: Catches connection/network problems within 120 seconds
- `PostgresqlTimeLagWithoutInput`: Warns about extended idle periods

## Lessons learned

This whole experience reinforced how important it is to understand the data sources behind your metrics. The postgres_exporter lag calculation has subtle behavior that becomes problematic in edge cases like delayed replicas, and the "obvious" alert logic breaks down when you dig into the actual mechanics.

---

*If you're dealing with similar PostgreSQL monitoring challenges or have war stories about delayed replicas. I'd love to hear them!
