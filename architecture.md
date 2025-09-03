# 🏗️ System Architecture (.NET 8 + Orleans + SQL Server + RabbitMQ + Redis)

## Context & Non-functional Requirements
- Domain: FX/Order/Trading backend.
- Throughput mục tiêu: 3–10k req/min (API), 10–50k msgs/min (broker).
- Latency mục tiêu (P95): < 100ms cho API sync; < 300ms cho xử lý async.
- HA: ≥ 99.9%. Zero-downtime deploy qua ArgoCD.
- Audit/Compliance: lưu journal order, audit login, permission trace.

## High-level Components
- **API Gateway/Ingress**: Nginx/K8s Ingress (mTLS → API).
- **BFF/API (.NET 8)**:
  - Controllers/Minimal API.
  - **Rate Limiting** (fixed-window/sliding).
  - **AuthN** (JWT/OIDC) + **AuthZ** (Role/Permission).
  - OpenAPI/Swagger.
- **Application Layer** (CQRS + MediatR):
  - Commands/Queries, Validation (FluentValidation).
  - Outbox (tuỳ chọn) cho event integration.
- **Domain Layer**:
  - Aggregates/Entities/ValueObjects + Domain Events.
- **Orleans Cluster**:
  - **Silo** (K8s) + Gateway.
  - Grains: OrderGrain, PriceStreamGrain, SessionGrain…
  - **Storage**: ADO.NET/EF-backed (hoặc riêng table) + Redis clustering cho pub/sub nhẹ.
- **Persistence**:
  - **SQL Server** (ACID) — EF Core.
  - **Redis** (cache, distributed lock, idempotency keys).
- **Messaging**:
  - **RabbitMQ** (publish domain events, async workflows).
- **Observability**:
  - Serilog (JSON) → Loki (hoặc ELK).
  - OpenTelemetry Traces/Metrics → Tempo/Jaeger + Prometheus/Grafana.
- **CI/CD**:
  - Docker multi-stage → ECR/Registry.
  - Helm/Manifest → ArgoCD sync.

## Data Flow (typical)
1. Client → API → MediatR Command → Domain → EF transaction.
2. Domain event (post-commit) → publish RabbitMQ → Consumer xử lý downstream.
3. Grains (Orleans) quản lý state dài hạn: per-Order, per-UserSession, per-Symbol.
4. Read model được cache ở Redis (key policy bên `/dependencies/redis-keys.md`).

## Trade-offs & Rationale
- **Orleans** cho stateful, concurrency per key, đơn giản hoá locking (thay vì manual distributed locks).
- **RabbitMQ** ưu tiên flow command/queue, dễ vận hành hơn Kafka cho volume hiện tại.
- **Redis** cho cache + ephemeral coordination (rate-limit counters, dedup).

## Failure Model
- API down → lỗi 5xx; Runbook `ops/runbooks/api-down.md`.
- Rabbit backpressure → tăng consumer, dead-letter; Runbook `ops/runbooks/rabbit-backpressure.md` (thêm file).
- Redis timeout → scale/eviction, network; `redis-timeout.md`.
- SQL deadlock → retry/transaction scope tuning; `sql-deadlock.md` (thêm file).
- Orleans silo partition/loss → membership & liveness; `orleans-silo.md` (thêm file).
