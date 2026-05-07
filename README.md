# GitOps with ArgoCD — Portfolio Project

Continuous delivery using GitOps — the Git repo is the single source of truth.
ArgoCD watches this repo and automatically syncs the cluster to match it.
No kubectl apply. No manual deployments. Git is the deployment mechanism.

## How it works

1. A manifest change is pushed to this repo
2. ArgoCD detects the change within 3 minutes
3. ArgoCD applies it to the cluster automatically
4. If anyone manually changes the cluster, ArgoCD corrects it back (self-healing)

## What was proved

| Test | Result |
|---|---|
| Replica scale from 2 to 4 via Git commit | ArgoCD synced automatically, 4 pods running |
| Manual pod deletion | ArgoCD self-healed, replacement pod up in under 10 seconds |
| Cluster drift correction | Any manual kubectl change reverted automatically |

## Project structure

apps/nginx/deployment.yaml -- Nginx deployment and service manifest

## Key concepts demonstrated

GitOps -- Git is the source of truth. The cluster reflects exactly what is in this repo at all times.

Automated sync -- ArgoCD polls the repo every 3 minutes and applies any changes automatically.

Self-healing -- selfHeal: true means ArgoCD detects and corrects any drift between the cluster and Git.

Pruning -- prune: true means resources deleted from Git are also deleted from the cluster.

## Stack

ArgoCD, Kubernetes, Docker Desktop, GitHub, YAML

## What I would add next

- Helm chart support for parameterised deployments
- Multi-environment setup with Kustomize overlays
- ArgoCD Image Updater to automatically bump image tags on new builds
- RBAC to restrict who can sync which applications
- Notifications to Slack when sync fails
