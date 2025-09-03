# ADR 0005: Idempotency Keys for Public Commands
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** API Team

## Context
Client có thể retry (mạng chập chờn) → tránh tạo lệnh trùng.

## Options
1) Không làm (dựa vào client) → rủi ro.  
2) **Idempotency-Key header** + server-side store TTL.  
3) Dựa vào natural key (OrderNo) – không phù hợp mọi use-case.

## Decision
- Bắt buộc **`Idempotency-Key`** cho các **command nhạy cảm** (`POST /orders`).  
- Lưu dấu trong **Redis**: `dedup:{key}`, TTL = 24h, giá trị = `{status, responseHash}`.  
- Nếu nhận lại key trong TTL → **trả lại response cũ** (hoặc 409 tuỳ api).

## Consequences
+ Tránh double-commit; UX ổn định khi client retry.  
– Tốn Redis & cần housekeeping.

## Implementation Notes
- Hash response (sha256) để trả nhanh; log `traceId` gắn với key.  
- Với Outbox, `MessageId` = `Idempotency-Key`.

## Related
- ADR 0003 (Outbox)  
- ADR 0007 (Message semantics)
