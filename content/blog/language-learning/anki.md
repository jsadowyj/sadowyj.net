+++
title = 'How I Learn Languages, Part 6: Anki'
date = 2026-09-26T21:00:00-04:00
draft = true
+++

This is the second stage of the pipeline: **learning**. It's where the actual mental connections form.

Aminte makes *cloze* cards: each card shows a full sentence from a LingQ lesson with the new word blanked out, and I fill in the blank. Anki's spaced repetition then schedules each card to come back right before I'd forget it. This is where I make the jump from translating everything in my head to understanding the language directly. As I keep up with the daily reviews, the reading in LingQ gets noticeably easier.

Aminte also has an optional paid text-to-speech add-on that reads the sentences aloud. It reinforces how the language sounds, and helps with pronunciation too, if you care about that like I do.

## My Anki settings

These are the deck settings I use with Aminte:

![Anki deck options, part 1: 30 new cards per day, 9,999 maximum reviews per day, 10-minute learning and relearning steps, leech threshold of 4, leech action set to Suspend Card](/images/anki_settings_1.png)
![Anki deck options, part 2: display order settings, with FSRS enabled and desired retention at 90%](/images/anki_settings_2.png)
![Anki deck options, part 3: burying, audio, timer, and auto-advance settings](/images/anki_settings_3.png)

The ones that matter most:

- **30 new cards a day, with no cap on reviews.** I'd rather clear every review due that day than let them pile up.
- **FSRS on, at 90% retention.** FSRS is Anki's newer scheduling algorithm. It adapts to how you actually remember cards.
- **Leech threshold of 4, set to suspend.** More on this below.

## Leeches

Some cards just won't stick without an extra nudge. This gets more common as I progress, because I start noticing that a second word would fit the sentence just as well as the "correct" one, and I keep mixing them up. Anki calls a card I keep failing a **leech**. Once a card hits the leech threshold, Anki *suspends* it, meaning it stops showing up in reviews until I fix it. I set the threshold to 4 instead of the default 8, so I don't have to fail a card eight times before I get to the fix.

The fix: when a card is marked as a leech, I click **Edit** on it and fill in the **Cue** field, which then shows up under the sentence. The trick is to give myself the *smallest* hint that works. Writing the English translation would make the card too easy, so I try to find the minimum information I need to get it right next time. Two examples:

### A mnemonic cue

![A leeched Anki card for the Russian sentence "Затем он постирает свою одежду в стиральной машине" (Then he washes his clothes in the washing machine), with the cue "post malone riot with laundry detergent"](/images/leech_1.png)

I couldn't fill in постирает (washes) after multiple attempts, so I made up a silly [mnemonic]({{< relref "lingq-reading.md#mnemonics-for-stuck-words" >}}): the word sounds vaguely like "posty-riot," so I picture Post Malone rioting with laundry detergent.

### A tense and infinitive cue

![A leeched Anki card for the Russian sentence "Жора решил посмотреть новую комедию" (Zhora decided to watch a new comedy), with the cue "m. past, решать"](/images/leech_2.png)

This card was genuinely ambiguous, for two reasons:

1. The blank could just as easily have been the present tense of решил (decided), so the cue says it's masculine past tense.
2. "Decided" isn't the only verb that fits. "Wanted" works in this sentence just as well. So the cue also gives the infinitive, решать (to decide), and I write it in Russian, not English, so the card still makes me recall the word.

### Is it worth fixing leeches?

I think so. A leech I let stay suspended never gets as firmly set in my mind as the words I actually review. That said, if you're short on time, letting leeches stay suspended is fine. And if a card turned into a leech because two words fit equally well, that's a good sign: it means you're starting to notice nuance.

## Why not just read more in LingQ?

Anki pays off most once I start speaking. When I blank on a word mid-sentence, I can usually remember a card it appeared on and replay that whole sentence in my head until the word comes back. The "just read a ton" approach that LingQ pushes can't give you that. Anki also solves the problem of "when do I stop translating in my head?" The front of every cloze card is entirely in the target language, so I recall each word from the sentence around it, not from its English translation. After enough reviews, words connect straight to their meaning, and the translating stops on its own without me forcing it.

---

[← Part 5: LingQ reading]({{< relref "lingq-reading.md" >}}) · [Part 7: LingQ listening →]({{< relref "lingq-listening.md" >}})
