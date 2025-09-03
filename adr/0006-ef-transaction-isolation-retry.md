# ADR 0006: EF Transaction Isolation & Retry Policy
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** Data Team

## Context
Khối lượng transaction cao, có nguy cơ deadlock/timeout.

## Options
1) **READ COMMITTED** + Retry (Polly) – cân bằng, phổ biến.  
2) SNAPSHOT – giảm lock read, nhưng cần bật ALLOW_SNAPSHOT_ISOLATION, có side-effects.  
3) SERIALIZABLE – an toàn nhưng lock mạnh, giảm throughput.

## Decision
- Mặc định **READ COMMITTED**.  
- Bật **READ_COMMITTED_SNAPSHOT** tại DB để giảm shared lock.  
- Áp dụng **retry** (deadlock/timeout): 3–5 lần, exponential backoff.  
- Giao dịch nhỏ; luôn ghi chú “lock order” nhất quán.

## Consequences
+ Cân bằng tính nhất quán và hiệu năng; giảm deadlock rate.  
– Phải audit transaction scope trong code review.

## Implementation Notes
- EF Core execution strategy (EnableRetryOnFailure).  
- Polly: `SqlException` numbers 1205/4060/40197/40501/40613…  
- Metrics: deadlocks/min, avg tx duration.

## Related
- ADR 0002 (Orleans storage)  
- ADR 0013 (Cache)
