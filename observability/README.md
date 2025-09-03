# 👀 Observability Documentation

## Mục tiêu
Observability giúp team:
- Hiểu rõ **tình trạng hệ thống** trong mọi thời điểm.
- Phát hiện lỗi sớm, giảm MTTR (Mean Time to Recovery).
- Theo dõi **SLO/SLA** và hỗ trợ root-cause analysis.

Thư mục `observability/` lưu các hướng dẫn chuẩn để **log → trace → metric** đều nhất quán.

---

## Các thành phần chính

### 1. [Logging](./logging.md)
- Chuẩn log: JSON, structured logging.
- Enrich với `traceId`, `userId`, `clientId`, `env`, `app`.
- Tool: **Serilog** + **OpenTelemetry Logs**.
- Export: Loki hoặc ELK.

### 2. [Tracing](./tracing.md)
- Distributed tracing cho request đi qua API → Orleans → DB → RabbitMQ.
- Chuẩn propagation: **W3C Trace Context** (`traceparent`).
- Tool: **OpenTelemetry Traces** → Tempo/Jaeger.
- Luôn attach `traceId` vào response API (ProblemDetails).

### 3. [Metrics](./metrics.md)
- Prometheus scrape metrics từ API, Orleans, RabbitMQ, Redis, SQL.
- Dùng **histogram** cho latency, **counter** cho request/error.
- Tool: **Prometheus** + **Grafana** dashboard.

---

## Convention
- Mọi service đều phải expose endpoint `/metrics` cho Prometheus.  
- Logs phải có **correlation ID** → link trace-log-metric.  
- Alerting dựa trên metric, không chỉ dựa trên log.  

---

## Tổ chức thư mục
```yaml
/docs/observability
│── README.md # Giới thiệu
│── logging.md # Chuẩn log
│── tracing.md # Chuẩn trace
└── metrics.md # Chuẩn metric
```

---

## Best practice
- Không log dữ liệu nhạy cảm (password, token, PII).  
- Sampling trace: 100% cho staging, 20% cho production.  
- Dashboard Grafana phải được chuẩn hoá (naming, panels).  
- Alert rule → link sang [Runbooks](../ops/runbooks/) để dễ xử lý sự cố.  

Ví dụ:  
- Alert: `rabbitmq_queue_messages_ready > 1000` → link [rabbit-backpressure.md](../ops/runbooks/rabbit-backpressure.md)  

---
