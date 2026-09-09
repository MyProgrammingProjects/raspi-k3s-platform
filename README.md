## Overview

This repository documents the evolution of a Raspberry Pi Kubernetes home lab designed to simulate a small-scale platform engineering environment.

The project started as a way to explore Kubernetes fundamentals and progressively evolved into a broader initiative focused on:

- Infrastructure as Code
- CI/CD automation
- GitOps workflows
- Cluster operations
- Observability
- Reproducible infrastructure
- Platform engineering concepts

The environment is intentionally self-hosted and resource-constrained in order to expose operational tradeoffs commonly hidden by managed cloud services.

---

# Infrastructure

Current cluster layout:

| Node | Role | Description |
|---|---|---|
| master | Kubernetes control plane | Cluster orchestration |
| worker1 | Worker node | Application workloads |
| worker2 | Worker node | Application workloads |
| tools | Tooling node | CI/CD and supporting services |

Hardware:

- Raspberry Pi 4 Model B
- Debian GNU/Linux 13 (Trixie)
- Ethernet-based cluster networking

---

# Platform Architecture

The cluster exposes services externally through a Cloudflare Tunnel rather than opening inbound ports on the home network.

External traffic enters Cloudflare, traverses the tunnel established by cloudflared, reaches the Kubernetes ingress layer, and is then routed to the Gateway API responsible for forwarding requests to backend services.

This architecture provides:

* Secure external access without port forwarding
* Centralized request routing
* Service isolation within the cluster
* Internal-only backend services
* A platform structure similar to production environments


```txt
Internet
    │
    ▼
Cloudflare
    │
    ▼
Cloudflare Tunnel (cloudflared)
    │
    ▼
Ingress
    │
    ▼
Gateway API
    │
    ├──► Users Service
    │
    ├──► Products Service
    │
    ├──► Orders Service
    │
    └──► Other Internal Services

```


---

# Goals

The primary objective is not simply "running Kubernetes at home".

The goal is to progressively build a reproducible and automated platform environment while documenting:

- architecture decisions
- operational constraints
- automation strategies
- implementation tradeoffs
- infrastructure evolution

---

# Repository Structure

This platform is intentionally separated into multiple repositories in order to isolate concerns and reflect real-world infrastructure boundaries.

| Repository | Purpose | Status |
|---|---|---|
| [`raspi-k3s-ansible`](https://github.com/MyProgrammingProjects/raspi-k3s-ansible) | Infrastructure automation and node provisioning | Completed |
| [`raspi-k3s-jenkins`](https://github.com/MyProgrammingProjects/raspi-k3s-jenkins) | Jenkins configuration and CI/CD experimentation | Completed |
| [`raspi-k3s-applications`](https://github.com/MyProgrammingProjects/raspi-k3s-applications) | Sample applications deployed into the cluster | Completed |
| [`raspi-k3s-helm-charts`](https://github.com/MyProgrammingProjects/raspi-k3s-helm-charts)  | Reusable Kubernetes Helm charts | Completed |
| [`raspi-k3s-gitops`](https://github.com/MyProgrammingProjects/raspi-k3s-gitops) | GitOps deployment state and Argo CD configuration | Completed |

---

# Roadmap

## Phase 1 — Cluster Foundation

| Task | Status |
|---|---|
| Raspberry Pi cluster assembly | Completed |
| Debian installation and node preparation | Completed |
| Kubernetes bootstrap | Completed |
| Internal cluster networking | Completed |

---

## Phase 2 — Infrastructure Automation

| Task | Status |
|---|---|
| SSH automation | Completed |
| Ansible inventory organization | Completed |
| Cluster-wide package management | Completed |
| Reusable Ansible roles | Completed |
| Node standardization | Completed |

Repository:
- [`raspi-k3s-ansible`](https://github.com/MyProgrammingProjects/raspi-k3s-ansible)

---

## Phase 3 — CI/CD Platform

| Task | Status |
|---|---|
| Jenkins deployment | Completed |
| Dynamic Kubernetes agents | Completed |
| Container image pipelines | Completed |
| Azure Container Registry integration | Completed |

Repositories:
- [`raspi-k3s-jenkins`](https://github.com/MyProgrammingProjects/raspi-k3s-jenkins)
- [`raspi-k3s-applications`](https://github.com/MyProgrammingProjects/raspi-k3s-applications)

---

## Phase 4 — Kubernetes Packaging

| Task | Status |
|---|---|
| Helm chart structure | Completed |
| Environment parameterization | Completed |
| Chart reuse strategy | Completed |

Repository:
- [`raspi-k3s-helm-charts`](https://github.com/MyProgrammingProjects/raspi-k3s-helm-charts)

---

## Phase 5 — GitOps

| Task | Status |
|---|---|
| Argo CD installation | Completed |
| GitOps repository structure | Completed |
| Automated deployment reconciliation | Completed |
| Environment separation | Planned |

Repository:
- [`raspi-k3s-gitops`](https://github.com/MyProgrammingProjects/raspi-k3s-gitops)

---

## Phase 6 — Platform Operations

| Task | Status |
|---|---|
| External TLS Management (Cloudflare) | Completed |
| Ingress management | Completed |
| Observability stack | Planned |
| Prometheus metrics | Planned |
| Centralized logging | Planned |
| Persistent storage strategy | Planned |
| Backup strategy | Planned |

---

# Architecture Principles

Several principles guide the structure of this project:

## Separation of concerns

Infrastructure automation, CI/CD, deployment state, and application code are intentionally isolated into dedicated repositories.

This mirrors real-world operational boundaries and simplifies maintenance.

---

## Git as source of truth

Infrastructure and deployment state are progressively moving toward declarative GitOps workflows using Argo CD.

---

## Reproducibility over manual administration

The project prioritizes automation and repeatability in order to reduce operational drift and simplify cluster rebuilds.

---

## Operational realism

The cluster intentionally runs on constrained ARM hardware in order to expose:

- resource limitations
- networking complexity
- storage tradeoffs
- ARM compatibility issues
- operational friction

---

# Challenges Encountered

Some recurring challenges throughout the project:

- ARM container image compatibility
- SD card reliability concerns
- Kubernetes networking complexity
- Storage persistence strategies
- Internal routing issues
- Resource limitations on Raspberry Pi hardware
- Balancing simplicity vs production-like architecture

These constraints are considered part of the learning process rather than obstacles to hide.

---

# Why this project exists

This repository is not intended to present a production-grade Kubernetes platform.

The purpose is to document the progressive transformation of a small home lab into a reproducible and operationally coherent platform engineering environment.

The emphasis is placed on:
- engineering decisions
- operational tradeoffs
- automation strategy
- infrastructure evolution

rather than simply demonstrating tools in isolation.

---

# Current Focus

Current areas of work:

- Jenkins integration
- Helm chart standardization
- GitOps repository design
- Argo CD deployment workflows


---

# Validation

The following screenshots demonstrate the platform operating end-to-end:

- Successful Jenkins pipeline execution

![Jenkins Pipelines](./images/jenkins_pipelines.png)
![Jenkins Gateway Application Pipeline Stages](./images/jenkins_gateway_api_pipeline.png)
![Jenkins Accounts API Pipeline Stages](./images/jenkins_accounts_api_pipeline.png)
![Jenkins Search API Pipeline Stages](./images/jenkins_search_api_pipeline.png)
![Jenkins Users API Pipeline Stages](./images/jenkins_users_api_pipeline.png)

- Container image publication to Azure Container Registry

![ACR Repositories](./images/acr_repositories.png)
![ACR Gateway Container Image](./images/acr_gateway_image.png)
![ACR Accounts Container Image](./images/acr_accounts_image.png)
![ACR Search Container Image](./images/acr_search_image.png)
![ACR Users Container Image](./images/acr_users_image.png)

![Kubernetes](./images/kubernetes_pods_images_tags.png)

- Kubernetes deployment rollout

![Kubernetes](./images/kubernetes_pods.png)
![Kubernetes](./images/kubernetes_argocd_pods_svc.png)

- Internal service communication

curl -X POST http://users-api-svc/api/users/register -H "Accept: application/json" -H "Content-Type: application/json" -d '{"Username": "usern4ame4","Password": "g!ycuWir3g!ycuWir3","Email": "my.dummy.email2@test.com" }'

curl -X POST http://accounts-api-svc/api/account/authenticate -H "Accept: application/json" -H "Content-Type: application/json" -d '{"Username": "usern4ame4","Password": "g!ycuWir3g!ycuWir3"}'

curl -X GET http://search-api-svc/api/search/users -H "Accept: application/json" -H "Content-Type: application/json" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1bmlxdWVfbmFtZSI6InVzZXJuM2FtZTMiLCJuYW1laWQiOiI1OGFmNjNhMS0zYTA5LTRiNjMtODRkNC1iNzEzZWI1M2ZmYzYiLCJzZXNzaW9uaWQiOiJmNWJiNmJmNC02MDI5LTQ4ZWUtYmQxZS04ZTQwZDBjODEzOTkiLCJyb2xlIjoiVXNlciIsIm5iZiI6MTc3OTU0OTgxMywiZXhwIjoxNzc5NjExMjUzLCJpYXQiOjE3Nzk1NDk4MTMsImlzcyI6InByb2dyYW1taW5ncHJvamVjdHMiLCJhdWQiOiJyZXN0cmljdGVkIn0.oowm25GXEFGroW3WmtfgMfFi9kciUNRa2eE75SChlFs"


- Gateway API request routing


curl -X POST http://gateway-api-svc/users/register -H "Accept: application/json" -H "Content-Type: application/json" -d '{"Username": "usern5ame5","Password": "g!ycuWir3g!ycuWir3","Email": "my.dummy.email2@test.com" }'

curl -X POST http://gateway-api-svc/accounts/authenticate -H "Accept: application/json" -H "Content-Type: application/json" -d '{"Username": "usern5ame5","Password": "g!ycuWir3g!ycuWir3"}'

curl -X GET http://gateway-api-svc/search/users -H "Accept: application/json" -H "Content-Type: application/json" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1bmlxdWVfbmFtZSI6InVzZXJuM2FtZTMiLCJuYW1laWQiOiI1OGFmNjNhMS0zYTA5LTRiNjMtODRkNC1iNzEzZWI1M2ZmYzYiLCJzZXNzaW9uaWQiOiJmNWJiNmJmNC02MDI5LTQ4ZWUtYmQxZS04ZTQwZDBjODEzOTkiLCJyb2xlIjoiVXNlciIsIm5iZiI6MTc3OTU0OTgxMywiZXhwIjoxNzc5NjExMjUzLCJpYXQiOjE3Nzk1NDk4MTMsImlzcyI6InByb2dyYW1taW5ncHJvamVjdHMiLCJhdWQiOiJyZXN0cmljdGVkIn0.oowm25GXEFGroW3WmtfgMfFi9kciUNRa2eE75SChlFs"



- External access through Cloudflare Tunnel


curl -X POST https://gateway.hidden_domain/users/register -H "Accept: application/json" -H "Content-Type: application/json" -d '{"Username": "usern5ame5","Password": "g!ycuWir3g!ycuWir3","Email": "my.dummy.email2@test.com" }'

curl -X POST https://gateway.hidden_domain/accounts/authenticate -H "Accept: application/json" -H "Content-Type: application/json" -d '{"Username": "usern5ame5","Password": "g!ycuWir3g!ycuWir3"}'

curl -X GET https://gateway.hidden_domain/search/users -H "Accept: application/json" -H "Content-Type: application/json" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1bmlxdWVfbmFtZSI6InVzZXJuM2FtZTMiLCJuYW1laWQiOiI1OGFmNjNhMS0zYTA5LTRiNjMtODRkNC1iNzEzZWI1M2ZmYzYiLCJzZXNzaW9uaWQiOiJmNWJiNmJmNC02MDI5LTQ4ZWUtYmQxZS04ZTQwZDBjODEzOTkiLCJyb2xlIjoiVXNlciIsIm5iZiI6MTc3OTU0OTgxMywiZXhwIjoxNzc5NjExMjUzLCJpYXQiOjE3Nzk1NDk4MTMsImlzcyI6InByb2dyYW1taW5ncHJvamVjdHMiLCJhdWQiOiJyZXN0cmljdGVkIn0.oowm25GXEFGroW3WmtfgMfFi9kciUNRa2eE75SChlFs"



---

# Future Areas of Exploration

Planned future topics include:

- Blue/Green deployments
- Policy enforcement
- Secret management
- Multi-environment deployments
- Cluster observability
- Backup and disaster recovery
- Security hardening

---

# Known Observations

## Secret Management

Application secrets are currently stored as standard Kubernetes Secret resources. While values are base64 encoded, they are not encrypted and should not be considered secure for storing sensitive information in Git repositories.

Future improvements may include implementing Sealed Secrets, SOPS, or an External Secrets solution to ensure secret values are encrypted or retrieved from a dedicated secret management system before deployment.


---

# Related Content

Additional project updates and implementation details are periodically shared on LinkedIn.



![Cluster](./images/cluster_setup.jpg)
