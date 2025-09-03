# 📑 Architecture Decision Records (ADR)

## Giới thiệu
ADR (Architecture Decision Record) là tài liệu ghi lại **các quyết định kiến trúc quan trọng** trong dự án.  
Mục tiêu: truyền đạt **vì sao** (why) hơn là chỉ có **cách làm** (how), giúp thế hệ sau hiểu rõ bối cảnh & trade-off.  

Mỗi ADR là một file Markdown, đặt trong thư mục `docs/adr/`, tên theo format:

```markdown
0001-short-title.md
```

## Quy ước viết ADR
- **Số thứ tự**: 4 chữ số, tăng dần (0001, 0002, …).  
- **Tên file**: ngắn gọn, dạng kebab-case (`0004-rate-limiter-strategy.md`).  
- **Trạng thái**:  
  - `Proposed`: đang đề xuất  
  - `Accepted`: đã chấp nhận  
  - `Rejected`: đã bác bỏ  
  - `Deprecated`: không còn dùng  
  - `Superseded by 00xx`: bị thay thế bởi ADR mới  
- **Cấu trúc chuẩn** (nên giữ format này trong mỗi ADR):
  1. **Title** (ví dụ: ADR 0004: API Rate Limiter Strategy)  
  2. **Status / Date / Owner**  
  3. **Context** (bối cảnh, ràng buộc, vấn đề cần giải quyết)  
  4. **Options** (các lựa chọn khả dĩ, kèm ưu/nhược)  
  5. **Decision** (quyết định cuối cùng)  
  6. **Consequences** (hệ quả, trade-off)  
  7. **Implementation Notes** (nếu có: thư viện, config, convention)  
  8. **Related ADRs** (liên kết đến ADR khác để tham chiếu chéo)  

👉 **Nguyên tắc quan trọng**:
- Mỗi ADR chỉ giải quyết **1 quyết định kiến trúc**.  
- Khi thay đổi quyết định → viết ADR mới **supersede** ADR cũ, **không sửa trực tiếp**.  
- Viết **ngắn, rõ, dễ đọc**, tập trung vào bối cảnh & trade-off.  

---

## 📋 Danh sách ADR

### Messaging & Integration
- [0001-use-rabbitMQ.md](./0001-use-rabbitMQ.md) — Chọn RabbitMQ cho async workflow  
- [0003-outbox-pattern.md](./0003-outbox-pattern.md) — Outbox để đảm bảo at-least-once  
- [0005-idempotency-keys.md](./0005-idempotency-keys.md) — Idempotency cho command  
- [0007-message-semantics.md](./0007-message-semantics.md) — Chuẩn hoá semantics & delivery  
- [0008-saga-style.md](./0008-saga-style.md) — Saga orchestration bằng Orleans  

### Orleans & Persistence
- [0002-orleans-state-storage.md](./0002-orleans-state-storage.md) — Storage provider cho Orleans grains  
- [0006-ef-transaction-isolation-retry.md](./0006-ef-transaction-isolation-retry.md) — Isolation level & retry EF/SQL  

### API & Security
- [0004-rate-limiter-strategy.md](./0004-rate-limiter-strategy.md) — Rate limiter cho API  
- [0011-api-versioning.md](./0011-api-versioning.md) — Chính sách versioning API  
- [0012-authz-model.md](./0012-authz-model.md) — Mô hình Role + Policy-based Permissions  
- [0009-secrets-management.md](./0009-secrets-management.md) — Secrets management & rotation  

### Observability & Reliability
- [0010-observability-otel.md](./0010-observability-otel.md) — OpenTelemetry cho logs/traces/metrics  
- [0013-cache-strategy.md](./0013-cache-strategy.md) — Chiến lược Redis cache  

---

## 📝 Hướng dẫn tạo ADR mới
1. Copy template sau và lưu vào file `00xx-title.md`:

```markdown
# ADR 00xx: <Tên quyết định>
**Status:** Proposed  
**Date:** YYYY-MM-DD  
**Owner:** <Team/Người phụ trách>

## Context
Mô tả bối cảnh, vấn đề, constraint.

## Options
1) Lựa chọn A — Ưu/nhược  
2) Lựa chọn B — Ưu/nhược  

## Decision
Quyết định chọn phương án nào, vì sao.

## Consequences
Hệ quả, trade-off, chi phí vận hành.

## Implementation Notes
Thư viện, config, ví dụ code (nếu có).

## Related
- ADR liên quan
