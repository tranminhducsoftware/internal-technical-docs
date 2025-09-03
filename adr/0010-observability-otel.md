# ADR 0010: Observability with OpenTelemetry
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** Platform Team

## Context
Cần chuẩn hoá logs/traces/metrics cho .NET 8, Orleans, EF, RabbitMQ để debug nhanh & đo SLO.

## Decision
- **Traces**: OpenTelemetry (W3C), exporters **OTLP** → Tempo/Jaeger.  
- **Logs**: Serilog JSON, **enrich** `traceId`, `spanId`, `userId`, `clientId`, `env`, `app`.  
- **Metrics**: Prometheus; bắt buộc:
  - HTTP server duration (histogram, by route/status).
  - Orleans: activations, queue length, failures.
  - RabbitMQ: `messages_ready`, `unacked`, `consumers`.
  - SQL: deadlocks/min, connection pool usage.
- Error response luôn chứa `traceId`.

## Consequences
+ Chuẩn hoá quan sát; rút ngắn MTTR.  
– Chi phí lưu trữ/logging; cần retention policy.

## Implementation Notes
- .NET: `OpenTelemetry.Extensions.Hosting`; add ASP.NET/HttpClient/EF/Orleans instrumentation.  
- Sampling: Parent-based + 20% (prod), 100% (staging).  
- Log scrubber: mask PII/secrets.

## Related
- ADR 0016 (Error model — nếu có)  
- ADR 0004 (Rate limit — expose metrics)
