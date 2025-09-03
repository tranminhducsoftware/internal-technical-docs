# ADR 0013: Redis Cache Strategy (Read-Through/Aside)
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** Data Team

## Context
Giảm tải SQL, tăng tốc read model; tránh cache stampede & stale dữ liệu.

## Decision
- Mẫu **Cache-Aside** cho read models:
  - Miss → fetch từ DB → set cache TTL (5–15m tuỳ domain).
  - Write → update DB → **invalidate** cache key liên quan (event-driven khi cần).
- Key conventions: xem `/dependencies/redis-keys.md`.
- Chống stampede: **per-key lock** (Redis SET NX + TTL ngắn) hoặc local semaphore.
- Large list/paging: cache **page** (size cố định) thay vì toàn bộ tập.

## Consequences
+ Đơn giản, kiểm soát TTL; dễ rollout.  
– Cần cẩn thận invalidation; có thể trả dữ liệu cũ trong TTL.

## Implementation Notes
- Serializer: System.Text.Json; compress nếu > 8KB.  
- Eviction: allkeys-lru; set size limit.  
- Metric: hit ratio, avg load time, evictions/sec.

## Related
- ADR 0005 (Idempotency — dùng Redis)  
- ADR 0002 (Orleans storage)  
- ADR 0003 (Outbox — invalidate on event)
