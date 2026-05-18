# Datacenter GitOps — App of Apps

Full GitOps management of Kubernetes cluster via ArgoCD App of Apps pattern.

## One Command to Rule Them All

```bash
kubectl apply -f datacenter-apps.yaml
```

ArgoCD automatically deploys:
- **Prometheus + Grafana** — monitoring
- **Nginx Ingress Controller** — traffic routing
- **HashiCorp Vault** — secrets management
- **test-app** — Flask app with Vault sidecar
- **Watchlist** — microservice app (FastAPI + PostgreSQL + Redis + Celery)

## Architecture
datacenter-gitops (this repo)
└── apps/              ← ArgoCD reads this
├── prometheus     ← creates Application → helm chart → monitoring namespace
├── ingress-nginx  ← creates Application → helm chart → ingress-nginx namespace
├── vault          ← creates Application → helm chart → vault namespace
├── test-app       ← creates Application → k8s manifests → default namespace
└── watchlist-dev  ← creates Application → bog-watchlist-helm → watchlist-dev namespace

## Related Repos

- [datacenter-k8s](https://github.com/MassonTG/datacenter-k8s) — cluster setup docs
- [bog-watchlist-helm](https://github.com/bog-watchlist/bog-watchlist-helm) — Watchlist Helm charts
- [bog-watchlist-app](https://github.com/bog-watchlist/bog-watchlist-app) — Watchlist source code