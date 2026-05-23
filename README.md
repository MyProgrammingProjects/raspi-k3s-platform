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
| [`raspi-k3s-jenkins`](https://github.com/MyProgrammingProjects/raspi-k3s-jenkins) | Jenkins configuration and CI/CD experimentation | In Progress |
| [`raspi-k3s-applications`](#) | Sample applications deployed into the cluster | In Progress |
| [`raspi-k3s-helm-charts`](#) | Reusable Kubernetes Helm charts | In Progress |
| [`raspi-k3s-gitops`](#) | GitOps deployment state and Argo CD configuration | Planned |

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
| Jenkins deployment | In Progress |
| Dynamic Kubernetes agents | In Progress |
| Container image pipelines | In Progress |
| Azure Container Registry integration | In Progress |

Repository:
- [`raspi-k3s-jenkins`](https://github.com/MyProgrammingProjects/raspi-k3s-jenkins)

---

## Phase 4 — Kubernetes Packaging

| Task | Status |
|---|---|
| Helm chart structure | In Progress |
| Environment parameterization | Planned |
| Chart reuse strategy | Planned |

Repository:
- [`raspi-k3s-helm-charts`](#)

---

## Phase 5 — GitOps

| Task | Status |
|---|---|
| Argo CD installation | In Progress |
| GitOps repository structure | In Progress |
| Automated deployment reconciliation | Planned |
| Environment separation | Planned |

Repository:
- [`raspi-k3s-gitops`](#)

---

## Phase 6 — Platform Operations

| Task | Status |
|---|---|
| Ingress management | Planned |
| TLS automation | Planned |
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

# Related Content

Additional project updates and implementation details are periodically shared on LinkedIn.



![Cluster](./images/cluster_setup.jpg)
