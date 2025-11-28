# GitHub Project Plan — devops-portfolio (Sprint Plan)

## Goal
Create a single repo demonstrating production-grade DevOps practices: infra as code, deployment pipelines, monitoring, and runbooks.

## Milestones (4 sprints)
### Sprint 1 — Basic infra & app
- Create sample app (Python Flask)
- Dockerfile (multi-stage)
- Terraform: VPC + EKS skeleton
- CI: Build and push image

### Sprint 2 — K8s + Deploy
- Helm chart for app
- Deploy to EKS (dev)
- ArgoCD setup for GitOps
- Add ingress & TLS (Let's Encrypt / cert-manager)

### Sprint 3 — Observability & Security
- Prometheus metrics & Grafana dashboards
- Loki log aggregation
- Trivy image scanning in CI
- Vault/Secrets demo (sealed secrets or SSM)

### Sprint 4 — Automation & Docs
- Auto-scaling demo & cost optimization notes
- Runbooks & RCA examples
- Release notes generator workflow
- README & walkthrough videos

## CI/CD Workflows
- `ci/build.yml` — build & push
- `ci/deploy-dev.yml` — deploy to dev via ArgoCD
- `ci/security-scan.yml` — run Trivy & SonarQube

## PR Requirements
- Tests must pass
- Linting & security scan green
- Peer review + approval

## How to present
- Use `README.md` with a clear demo script and `Makefile` to provision dev infra locally via `kind` or remote EKS.

