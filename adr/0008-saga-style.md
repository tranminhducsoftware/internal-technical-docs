# ADR 0008: Saga Style — Orchestration via Orleans
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** Domain Team

## Context
Các giao dịch nghiệp vụ nhiều bước (Create Order → Reserve Balance → Route LP → Confirm/Cancel). Cần cơ chế điều phối + bù trừ (compensation).

## Options
1) **Choreography** (event-chained) — đơn giản nhưng khó quan sát/rollback.  
2) **Orchestration** bằng 1 coordinator (Saga) — rõ ràng, dễ bù trừ; thêm 1 thành phần điều phối.

## Decision
- Dùng **Orleans Grain** làm **Saga orchestrator** theo **orchestration** style.
- Mỗi Saga có **state** (step, context, timeouts), **compensation steps** rõ ràng.
- Timeout/Retry per step; emit `SagaCompleted`/`SagaFailed` event.

## Consequences
+ Tập trung logic, dễ quan sát & test; phù hợp khi đã dùng Orleans.  
– Cần quản trị vòng đời grain & backpressure khi nhiều saga song song.

## Implementation Notes
- Grain: `OrderSagaGrain` key = `OrderId`.  
- State persisted via Orleans storage (SQL).  
- Step calls qua Mediator/HTTP/RPC; log `traceId`.

## Related
- ADR 0002 (Orleans storage)  
- ADR 0007 (Message semantics)
