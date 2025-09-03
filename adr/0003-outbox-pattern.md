# ADR 0003: Outbox Pattern for Reliable Messaging
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** Platform Team

## Context
Sau khi ghi DB (EF/SQL), cần publish event sang RabbitMQ **đúng-ít-nhất-một-lần**; tránh mất event khi API crash giữa chừng.

## Options
1) Publish trực tiếp trong transaction → Không khả thi (broker không tham gia 2PC).  
2) Publish sau commit (fire-and-forget) → Có thể mất event nếu crash.  
3) **Outbox**: ghi event vào bảng `Outbox` trong cùng transaction, một background publisher đọc & gửi, đánh dấu `Processed`.

## Decision
- Dùng **Outbox Pattern** cho tất cả domain events cần tích hợp.  
- Background publisher chạy dưới dạng hosted service (API) hoặc job (worker).

## Consequences
+ Đảm bảo **at-least-once**; dễ audit/replay.  
– Tốn thêm bảng & job; cần cleanup policy.

## Implementation Notes
- Table: `Outbox(Id, Type, Payload, OccurredAt, ProcessedAt, Attempts)`  
- Publisher: đọc theo FIFO, publish → RabbitMQ exchange, confirm ack; update `ProcessedAt`.  
- Retry: exponential backoff, DLQ nếu quá N lần.  
- Idempotency consumer: dùng `MessageId` & Redis key `dedup:{id}` TTL 24h.  

## Related
- ADR 0007 (Message semantics)  
- ADR 0005 (Idempotency keys)
