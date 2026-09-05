# Petclinic Helm chart

This chart packages the six required Petclinic services and the Ingress rule.

## Important values

`values.yaml` is the configuration file. For example, this value:

```yaml
imageTag: 0.1.1
```

creates this Kubernetes image reference:

```text
nexus:8081/docker-hosted/dev/api-gateway:0.1.1
```

The registry credential is deliberately not in the chart. Kubernetes already has
the `nexus-registry-secret` Secret in the `dev` namespace.

## Render without changing Kubernetes

```powershell
helm template petclinic devops/helm/petclinic --namespace dev
```

## Manual Helm deployment (later Argo CD will do this instead)

```powershell
helm upgrade --install petclinic devops/helm/petclinic --namespace dev
```
