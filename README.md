# Warhammer 40k 10th Edition Calculator - GitOps Repository

This repository contains the **GitOps configuration** for the Kubernetes (k3s) cluster hosting the [Warhammer 40k 10th Edition Calculator](https://github.com/AnNoName1/warhammer40k10thCalc) web application.

All changes are managed declaratively via **Argo CD** using the **app-of-apps** pattern.

## Architecture Overview

- **Single cluster** (k3s)
- **Argo CD** as the continuous delivery engine
- **Helm** for the main application (web-server)
- **Argo Rollouts** for progressive delivery in production
- **OpenTofu** (Terraform) for infrastructure provisioning (not stored in this repo)

## Current Structure

```bash
.
├── cluster-config/
│   ├── apps/
│   │   └── web-server/                 # Shared Helm chart (single source of truth)
│   │       ├── Chart.yaml
│   │       ├── values.yaml             # Base values (defaults)
│   │       ├── values-stage.yaml       # Stage-specific overrides
│   │       ├── values-prod.yaml        # Production-specific overrides
│   │       └── templates/
│   │           ├── _helpers.tpl
│   │           ├── workload.yaml       # Conditional: Deployment (stage) or Rollout (prod)
│   │           ├── service.yaml
│   │           ├── ingress.yaml
│   │           └── analysis-template.yaml
│   ├── argo-apps/
│   │   ├── root.yaml                   # Root App-of-Apps
│   │   └── web-server-appset.yaml      # ApplicationSet (manages stage + prod)
│   └── infra/
│       ├── kyverno/
│       ├── metallb/
│       └── monitoring/
└── README.md