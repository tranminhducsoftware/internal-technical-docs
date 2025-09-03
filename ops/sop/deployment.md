# 🚀 Deployment SOP (ArgoCD)

1) Build & push image (CI).
2) Update image tag trong Helm values (bot/PR).
3) ArgoCD auto-sync (or manual `argocd app sync trading-api`).
4) Verify:
   - `/healthz/ready` = 200
   - No 5xx spike
   - Orleans membership stable
5) Post-deploy checks: DB migrations success.
Rollback: `kubectl rollout undo deploy/trading-api`.
