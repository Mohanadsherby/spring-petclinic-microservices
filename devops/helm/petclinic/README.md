# Petclinic Helm chart

This chart is a single, generic template set (one Deployment, one Service, one
ConfigMap). You install it **once per microservice**, passing that service's values
file from the `values/` folder.

The Ingress is **not** part of this chart. It lives as a plain manifest at
`devops/k8s/base/petclinic-ingress.yaml`.

## Layout

```text
templates/
  deployment.yaml   # one Deployment, driven by .Values
  service.yaml      # one ClusterIP Service
  configmap.yaml    # <service>-config ConfigMap
values/
  config-server.yaml
  discovery-server.yaml
  customers-service.yaml
  vets-service.yaml
  visits-service.yaml
  api-gateway.yaml
```

Each file in `values/` is **self-contained** — it holds every value the templates
need (`name`, `image`, `tag`, `port`, `healthPath`, `replicaCount`, `imageRegistry`,
`imagePullSecret`, `config`, `service`, `resources`, and the `probes`). For example,
`values/api-gateway.yaml` produces this image reference:

```text
nexus:8081/docker-hosted/dev/api-gateway:0.1.1
```

Images are built and pushed to Nexus by the Jenkins pipeline.

The registry credential is deliberately not in the chart. The cluster must already
have the `nexus-registry-secret` Secret in the `dev` namespace.

## Render without changing Kubernetes

```powershell
helm template api-gateway devops/helm/petclinic --namespace dev -f devops/helm/petclinic/values/api-gateway.yaml
```

## Manual Helm deployment (later Argo CD will do this instead)

Install each service with its own values file:

```powershell
helm upgrade --install config-server     devops/helm/petclinic -n dev -f devops/helm/petclinic/values/config-server.yaml
helm upgrade --install discovery-server  devops/helm/petclinic -n dev -f devops/helm/petclinic/values/discovery-server.yaml
helm upgrade --install customers-service devops/helm/petclinic -n dev -f devops/helm/petclinic/values/customers-service.yaml
helm upgrade --install vets-service      devops/helm/petclinic -n dev -f devops/helm/petclinic/values/vets-service.yaml
helm upgrade --install visits-service    devops/helm/petclinic -n dev -f devops/helm/petclinic/values/visits-service.yaml
helm upgrade --install api-gateway       devops/helm/petclinic -n dev -f devops/helm/petclinic/values/api-gateway.yaml
```
