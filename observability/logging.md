
---

# 9) `observability/logging.md` + `tracing.md` + `metrics.md`

```markdown
# 📊 Logging (Serilog)
- Output: JSON; enrich: `TraceId`, `SpanId`, `UserId`, `ClientId`, `App`, `Env`.
- MinimumLevel: Information (Prod), Debug (Dev).
- Sensitive fields: mask (password, token, card…).

# 🧵 Tracing (OpenTelemetry)
- Propagation: W3C (`traceparent`).
- Sources: ASP.NET, EF Core, HttpClient, Orleans (ActivitySource).
- Exporters: OTLP → Tempo/Jaeger.
- Bắt buộc gắn `traceId` vào logs & error responses.

# 📈 Metrics (Prometheus)
- `http_server_duration_seconds` (histogram; route/verb/code).
- `orleans_activations`, `orleans_queue_length`.
- `rabbitmq_queue_messages_ready`, `published_total`.
- `sql_connection_pool_usage`, `deadlocks_total`.
