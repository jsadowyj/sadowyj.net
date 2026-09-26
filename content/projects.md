+++
title = 'Projects'
menu = 'main'
weight = 3
+++

## Projects

---

## Multi-Datacenter Monitoring Solution

![victoria-metrics-cluster-diagram](https://docs.victoriametrics.com/helm/victoria-metrics-k8s-stack/img/k8s-stack-overview.webp)

Built a monitoring platform that surfaced infrastructure problems before they turned into outages. Over 300 alerting rules covered everything from database replication lag to network saturation, so most issues were caught while they were still trending the wrong way rather than after something broke.

I designed the whole stack: VictoriaMetrics for metrics storage, Grafana for dashboards, and custom exporters for some pretty niche Triton SmartOS environments. The entire platform ran on Kubernetes using ArgoCD's "Apps of Apps" pattern, so every component was declarative and version-controlled. Each of the 300+ alerts shipped with its own AI-generated playbook, which meant whoever got paged started with a runbook instead of a blank page.

**Under the hood**:
- VictoriaMetrics Cluster
- Grafana with Azure AD SSO
- ArgoCD with Apps of Apps pattern
- k0s Kubernetes
- DirectPV storage
- sealed-secrets controller
- UpdateCLI for automated updates
- Kubernetes custom resources
- cert-manager for TLS
- ingress-nginx for routing
- custom Prometheus exporters
- VictoriaMetrics Operator
- Kustomize for manifest management

---

## Two-day CDN Migration

![cloudflare-logo](https://upload.wikimedia.org/wikipedia/commons/c/c5/Cf-logo-v-rgb.jpg)

Compressed what would have been weeks of manual console work into a two-day migration. Managing 100+ domains across multiple environments had been a slow, error-prone process; afterward the entire configuration lived in code.

I built the whole thing with Terraform modules for DNS management and CDN configurations that made the migration repeatable and auditable. The documentation was detailed enough that new team members could make DNS and CDN changes without inheriting tribal knowledge first.

**Under the hood**:
- Terraform modules for DNS and CDN configuration
- CloudFlare API for domain management
- site redirects and security rules automation
- origin certificate management
- multi-environment domain configurations
- BetterStack monitoring integration

---

## Terraform GitOps Conversions

![terraform-gitops-diagram](https://upload.wikimedia.org/wikipedia/commons/d/d7/Terraform-logo.png)

Converted hand-managed infrastructure to a GitOps workflow, which put an end to configuration drift and surprise changes - every change was code-driven, reviewed, and version-controlled.

I implemented automated Terraform workflows with plans on pull requests and applies on merge, plus SOPS encryption for secrets. The CI/CD pipeline was smart enough to detect exactly what changed and only rebuild those specific components. I'd rather spend an afternoon writing a module than make the same manual change twice - if it can be automated, it should be automated.

**Under the hood**:
- smart CI/CD that only runs terraform for modified applications
- SOPS with Age encryption for secrets
- remote state management in S3
- automated terraform plans on pull requests
- terraform applies on merge to main branch
- reusable terraform modules

---

## PostgreSQL Automations

![postgres-cake](https://live.staticflickr.com/7503/15471867088_5ef7392005_b.jpg)

Built PostgreSQL clusters that rode out network interruptions without manual intervention, with cross-datacenter replication for the failure modes that could take an entire site offline.

I wrote Ansible playbooks that knew their way around database replication, automated the backup process to allow for seamless point-in-time recovery, and built monitoring that warned us well before replication lag turned into an incident.

**Under the hood**:
- Ansible with custom roles
- PostgreSQL with streaming replication
- Molecule testing framework
- S3-compatible backup storage
- automated user provisioning
- Ansible Vault for secrets

---

## nsc

![nsc diagram](/images/nsc.png)

Given a phone number, the NetSapiens Console (NSC) application traverses through PBX call routes, and dynamically generates an IVR chart. NSC has saved the organization hundreds of hours over the course of many years, and it is still being used to this day as far as I know.

I wrote the backend Node.js and the front-end in React. It was the first project I ever worked on as a software engineering intern.

## LingQML

![lingqml diagrams](/images/lingqml.png)

My computer science capstone project exploring how machine learning can identify vocabulary gaps for language learners. The application analyzed a user's known words exported from [LingQ](https://www.lingq.com/en/) and applied K-Nearest Neighbors on FastText word embeddings to suggest semantically related words that might be missing from their vocabulary.

**Key Components**

- Parsing and normalizing FastText embeddings, frequency lists, and part-of-speech data from multiple public sources
- Part-of-speech distribution charts, frequency coverage plots, and word clouds built with matplotlib
- Unsupervised K-NN using cosine similarity on 300-dimensional word vectors to find semantically similar vocabulary gaps

**Under the hood**:
- Python
- scikit-learn
- FastText
- pandas
- matplotlib
- NumPy
- Jupyter Notebook
- Docker

**What I Learned**

- Working with high-dimensional word embeddings and vector normalization for cosine similarity
- Batch processing large datasets (2M+ word vectors) efficiently with NumPy
- Building interactive Jupyter notebooks
- Validating unsupervised ML models without labeled training data

---
