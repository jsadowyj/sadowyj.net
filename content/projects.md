+++
title = 'Projects'
menu = 'main'
weight = 3
+++

## Projects

---

## Multi-Datacenter Monitoring Solution

Built a monitoring platform that's basically a crystal ball for infrastructure problems - it knows about issues before they happen. With over 300 alerting rules watching everything from database hiccups to network sneezes, it catches problems while they're still just bad ideas.

I designed the whole stack using VictoriaMetrics for metrics storage, Grafana for dashboards that actually make sense, and custom exporters for some pretty niche Triton SmartOS environments. Each alert comes with its own AI-generated playbook - that's 300+ troubleshooting guides because apparently infrastructure finds new and creative ways to break.

---

## Two-day CDN Migration

Turned what should have been weeks of manual DNS surgery into a two-day Terraform symphony. Managing 25+ domains across multiple environments used to involve a lot of prayer and caffeine - now it's just code that works.

I built the whole thing with SOPS-encrypted secrets (because API keys floating around in plain text give me nightmares) and a CI/CD pipeline that's smart enough to only rebuild what actually changed. The documentation is clear enough that new team members don't need to decipher ancient infrastructure hieroglyphics.

---

## GitOps Conversions

Turned Kubernetes chaos into something that actually makes sense using ArgoCD's "Apps of Apps" pattern. No more "it works on my laptop" syndrome - everything is declarative, version-controlled, and refreshingly predictable.

I implemented the whole GitOps workflow with sealed-secrets for keeping credentials actually secret, and UpdateCLI for automated image updates that don't randomly explode. It's become my personal crusade to get absolutely everything possible into Terraform - if it can be automated, it should be automated.

---

## PostgreSQL Automation

Built PostgreSQL clusters that handle network hiccups like champs and have cross-datacenter replication for when things really hit the fan. Sleep is important, after all.

I wrote Ansible playbooks that know their way around database replication, automated the backup process until data loss became more of a theoretical worry than a real one, and built monitoring that gives me a heads up before PostgreSQL starts having a bad day. The cross-datacenter replication means we can survive a full datacenter outage without too much drama.

---

## nsc

![nsc diagram](/images/nsc.png)

Given a phone number, the NetSapiens Console (NSC) application traverses through PBX call routes, and dynamically generates an IVR chart. NSC has saved the organization hundreds of hours over the course of many years, and it is still being used to this day as far as I know.

I wrote the backend Node.js and the front-end in React. It was the first project I ever worked on as a software engineering intern.

---
