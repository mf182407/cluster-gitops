# MicroK8s Helm GitOps with Argo CD

This repository is for managing Helm releases with Argo CD:

- `argo-cd/` bootstraps the root Application, contains child Applications, and holds Argo CD chart values.
- `grafana-cloud/` holds Grafana Kubernetes Monitoring chart values.
- `grafana-cloud-alloy/` holds Grafana Alloy chart values.
- `kor/` holds Kor values.
- `magic-mirror/` holds MagicMirror values.

## 1. Configure the Applications

1. The Applications point to `https://github.com/mf182407/cluster-gitops.git`; update that URL if you fork or rename this repository.
2. Replace chart version placeholders with the exact installed versions. Grafana's `k8s-monitoring` and `alloy` charts are in `https://grafana.github.io/helm-charts`.
3. The folder and Argo CD Application names are just labels; they do not rename the Helm release.
4. The MagicMirror Application uses the chart at the root of `https://gitlab.com/khassel/magicmirror-helm.git`. Set `targetRevision` to the Git tag/ref for the chart version.

The root Application watches `argo-cd/apps/` on the `main` branch and creates the configured child Applications. After the root Application is healthy, commit and push changes to the values files or chart versions; Argo CD will detect them and sync the desired state.

## Repository layout

```text
argo-cd/
  apps/
    argo-cd.yaml.example
    grafana-cloud.yaml
    grafana-cloud-alloy.yaml
    magic-mirror.yaml
  root-application.yaml
  values.yaml
grafana-cloud/
  values.yaml
grafana-cloud-alloy/
  values.yaml
kor/
  values.yaml
magic-mirror/
  values.yaml
```

TODO:
-update all update_later fields,
-update targetRevision in each /apps/.yaml,
-update /apps/argo-cd.yaml.example,
-add kor data https://github.com/yonahd/kor