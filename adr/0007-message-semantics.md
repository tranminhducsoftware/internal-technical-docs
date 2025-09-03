# ADR 0007: Message Semantics & Delivery Guarantees
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** Platform Team

## Context
Tích hợp qua RabbitMQ + Outbox + Orleans consumers. Cần thống nhất “độ đảm bảo” khi gửi/nhận để thiết kế idempotency & error handling.

## Decision
- Chuẩn hệ thống: **At-least-once delivery** (gửi ≥1; consumer phải idempotent).
- **Không theo đuổi exactly-once** ở tầng tích hợp (cost quá cao).
- Mọi message phải có:
  - `messageId` (UUID), `occurredAt`, `producer`, `schemaVersion`.
  - `correlationId`/`traceId` để liên kết với request.
- Consumer:
  - Idempotent bằng **Redis key** `dedup:{messageId}` (TTL 24h).
  - Ack **sau** khi xử lý thành công (persist xong); lỗi thì `nack` → DLQ.
- Retry policy: exponential backoff; tối đa N lần trước khi đẩy DLQ.

## Consequences
+ Đơn giản, dễ vận hành, phù hợp quy mô hiện tại.  
– Yêu cầu kỷ luật idempotency ở tất cả consumers.

## Related
- ADR 0003 (Outbox)  
- ADR 0005 (Idempotency Keys)
