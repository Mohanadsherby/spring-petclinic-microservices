# DevOps practice workspace

My hands-on DevOps lifecycle practice on the Spring PetClinic microservices app.
Each folder maps to a phase of the roadmap.

| Folder | Phase | What goes here |
|--------|-------|----------------|
| `notes/`      | all      | My learning notes, commands that worked, gotchas |
| `ci-cd/`      | 2, 3     | CI/CD pipeline files, build/test/push automation |
| `security/`   | 4        | Image + dependency scanning config (Trivy, etc.) |
| `k8s/`        | 5        | Raw Kubernetes manifests for the 8 services |
| `helm/`       | 5        | Helm chart (packaged version of the k8s manifests) |
| `monitoring/` | 6        | Prometheus/Grafana dashboards + alert rules |
| `terraform/`  | 8        | Infrastructure as Code (advanced) |

## Roadmap progress

- [ ] Phase 0 — Run it locally with docker-compose
- [ ] Phase 1 — Git branching + PR flow
- [ ] Phase 2 — CI: tests + coverage
- [ ] Phase 3 — Build + push images to a registry
- [ ] Phase 4 — Security scanning in the pipeline
- [ ] Phase 5 — Deploy to local Kubernetes (kind)
- [ ] Phase 6 — Observability (Prometheus + Grafana)
- [ ] Phase 7 — Chaos / resilience testing
- [ ] Phase 8 — GitOps / IaC (Terraform, ArgoCD)
