# Warhammer 40k 10th Edition Calculator - GitOps Repository

This repository contains the GitOps configuration for the Kubernetes cluster hosting the Warhammer 40k 10th Edition Calculator web application.

## Structure

- `cluster-config/`: Root directory for all cluster configurations
  - `apps/`: Application-specific manifests
    - `web-server/`: Web application deployment configs
  - `infra/`: Infrastructure components
    - `ingress/`: Ingress controller configuration
    - `metallb/`: Load balancer configuration
    - `kyverno/`: Policy engine configurations
    - `monitoring/`: Monitoring stack configurations
  - `argo-apps/`: Argo CD Application manifests

## Deployment

Deployments are handled automatically by Argo CD when changes are pushed to this repository. The main application CI pipeline updates the image tags in the rollout manifests.

## Properties

- **Idempotent**: Multiple applications of the same config produce the same result
- **Drift-correcting**: Argo CD continuously reconciles the cluster state with the desired state
- **Observable**: Full visibility into deployment status and health through Argo CD UI