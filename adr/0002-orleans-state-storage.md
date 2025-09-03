# ADR 0002: Orleans State Storage Provider
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** Platform Team

## Context
Grain state cần durable storage. Ứng viên: (1) SQL Server (AdoNet/EF), (2) Redis (volatile), (3) Blob/Object storage.

- Yêu cầu: transactional consistency với nghiệp vụ (Order/Risk), backup đơn giản, vận hành quen thuộc.
- Khối lượng: hàng triệu records/tháng, kích thước state nhỏ–vừa (≤ 50KB/grain).

## Options
1) **SQL Server (AdoNet/EF provider)**  
   + ACID, backup/restore quen thuộc; có thể dùng chung infra DB.  
   – Tải cao có thể tạo áp lực IOPS; cần index/partitioning.

2) Redis  
   + Nhanh; phù hợp ephemeral state.  
   – Mất durable guarantee; phức tạp backup, risk data loss.

3) Blob/Object  
   + Rẻ, scale lớn.  
   – Latency cao; khó query/ops chung với transaction DB.

## Decision
- Chọn **SQL Server AdoNet provider** cho **grains nghiệp vụ** (OrderGrain, SessionGrain).  
- Cho **ephemeral stream/cache grains** có thể dùng Redis nhưng **không** làm nguồn sự thật.

## Consequences
+ Dễ đồng bộ với EF transactions, backup theo chuẩn DBA.  
– Cần tối ưu index, batch write; theo dõi deadlock.

## Implementation Notes
- Provider: `Orleans.Persistence.AdoNet` + SQL Server.  
- Table per grain type (hoặc shared) + PK theo GrainId.  
- Migration theo script kèm infra repo.  
- Metrics: write/read latency; deadlock count.

## Related
- ADR 0006 (EF isolation & retry)  
- ADR 0013 (Cache strategy)
