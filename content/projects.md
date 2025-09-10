+++
title = 'Projects'
menu = 'main'
weight = 3
+++

## Projects

---

## Enterprise Monitoring Platform

Built a comprehensive monitoring platform that watches over multiple datacenters, catching issues before users even notice them. The system provides real-time visibility into database performance, application health, and infrastructure metrics across our entire stack.

I designed the architecture using VictoriaMetrics for metrics storage, Grafana for visualization, and Prometheus for data collection. The platform has saved countless hours of troubleshooting and dramatically improved our incident response times.

---

## Lightning-Fast CDN Migration

Migrated all production CDN configurations between two different CDN providers in just two days. My push to get everything into Terraform paid off big time - what could have been weeks of manual work became a smooth, automated process.

I wrote Terraform modules to manage domain configurations, security rules, and site redirects. The infrastructure-as-code approach made the migration repeatable and auditable.

---

## GitOps Kubernetes Management

Turned chaotic Kubernetes deployments into smooth GitOps workflows with ArgoCD. Now infrastructure changes flow as smoothly as code commits, and every deployment is tracked and reversible.

I implemented automated remote write configurations for centralized monitoring and established deployment patterns that the entire team could follow. No more "it works on my machine" - everything is declarative and version-controlled.

---

## PostgreSQL High Availability

Set up high-availability PostgreSQL clusters that can handle anything from network hiccups to full datacenter outages. Sleep is important, after all.

I implemented replication strategies, automated backup processes, and monitoring systems that provide early warning for performance issues. The database systems now maintain 99.99% uptime even during major infrastructure changes.

---

---

## nsc

![nsc diagram](/images/nsc.png)

Given a phone number, the NetSapiens Console (NSC) application traverses through PBX call routes, and dynamically generates an IVR chart. NSC has saved the organization hundreds of hours over the course of three years, and it is still being used to this day.

I wrote the backend Node.js and the front-end in React. It was the first project I ever worked on as a software engineering intern.

---
