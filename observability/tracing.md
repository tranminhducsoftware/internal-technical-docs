# 🧵 Tracing (OpenTelemetry)
- Propagation: W3C (`traceparent`).
- Sources: ASP.NET, EF Core, HttpClient, Orleans (ActivitySource).
- Exporters: OTLP → Tempo/Jaeger.
- Bắt buộc gắn `traceId` vào logs & error responses.

