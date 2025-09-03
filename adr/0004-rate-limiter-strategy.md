# ADR 0004: API Rate Limiter Strategy
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** API Team

## Context
Bảo vệ API public/internal trước burst; công bằng theo khách hàng; vẫn đảm bảo trải nghiệm.

## Options
1) **Fixed Window** (ASP.NET built-in) – đơn giản, dễ cấu hình.  
2) Token Bucket – mượt hơn, phức tạp triển khai phân tán.  
3) Sliding Window – cân bằng, cần store chính xác hơn.

## Decision
- Public API: **Fixed Window** 1 phút (300 req/min), queue 50.  
- Internal API: **Token Bucket** (sau) nếu có nhu cầu.  
- Partition key: `clientId` (fallback `userId` → IP).  
- Store counter: **Redis** khi chạy nhiều replicas; local memory khi single pod (dev).

## Consequences
+ Dễ vận hành; rõ ràng thông số.  
– Fixed window có thể burst đầu–cuối cửa sổ → chấp nhận.

## Implementation Notes
- ASP.NET `AddRateLimiter` + `PartitionedRateLimiter`.  
- Header: trả `Retry-After`, `X-RateLimit-*`.  
- Metric: 429 count, permit acquired, queue length.

## Related
- ADR 0012 (AuthZ model)  
- ADR 0013 (Cache strategy)
