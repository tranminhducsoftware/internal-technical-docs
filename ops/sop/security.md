# 🔐 Security SOP
- Secrets: K8s sealed-secrets/Vault. Rotation 90 days.
- JWT signing key rotation (kid).
- TLS cert renew via cert-manager.
- Incident: token leak → revoke sessions, rotate keys, notify.
