# ADR 0009: Secrets Management & Rotation
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** Security Team

## Context
Keys/cert/connection strings cho API, SQL, RabbitMQ, Redis. Yêu cầu: bảo mật, audit, rotate định kỳ.

## Decision
- **Kubernetes Secrets** được quản lý bằng **Sealed Secrets** (git-safe).  
- Với secrets nhạy (JWT signing, DB creds prod): tích hợp **Vault** (hoặc Cloud KMS) khi khả dụng.  
- **Rotation**: 90 ngày; JWT signer hỗ trợ **key id (kid)** & **dual keys** cho giai đoạn chuyển đổi.
- Chỉ mount/ENV vào **namespace** tương ứng; nguyên tắc **least privilege**.

## Consequences
+ An toàn khi lưu trong Git; hỗ trợ rotation/audit.  
– Cần quy trình & tooling cho phát hành/rotate.

## Implementation Notes
- CI tạo/rotate sealed-secret bằng `kubeseal`.  
- JWKS endpoint để publish public keys (kid).  
- TLS: cert-manager auto-renew.

## Related
- ADR 0010 (Observability — audit logs)  
- ADR 0012 (AuthZ — claims & keys)
