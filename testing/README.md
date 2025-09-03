# 🧪 Testing Documentation

## Mục tiêu
- Đảm bảo **chất lượng phần mềm** và **tính ổn định** khi thay đổi.  
- Bắt lỗi càng sớm càng tốt (shift-left).  
- Tích hợp test vào CI/CD để mọi commit đều được kiểm chứng.

## Các tầng kiểm thử
1. **[Unit Test](./unit-test.md)**  
   - Kiểm thử logic thuần, domain rules, CQRS handlers.  
   - Nhanh, không cần I/O, chạy trên mọi PR.  

2. **[Integration Test](./integration-test.md)**  
   - Test tích hợp API, DB (EF/SQL Server), RabbitMQ, Redis, Orleans grains.  
   - Dùng Testcontainers/Docker Compose để spin up dependencies.  

3. **[Performance Test](./performance-test.md)**  
   - Đo throughput & latency với JMeter/k6.  
   - Gate trong CI/CD: fail nếu vượt P95 latency/error rate threshold.  

4. **[End-to-End Test](./e2e-test.md)**  
   - Giả lập full user flow (Login → Place Order → Cancel → Query).  
   - Thường chạy trên staging trước khi release.

---

## CI/CD Pipeline
- **Pull Request**: chạy Unit + Integration test.  
- **Nightly build**: full suite + Performance test.  
- **Pre-release**: E2E test trên môi trường staging.  

---

## Liên quan
- [Onboarding Guide](../onboarding/README.md) — Dev mới cần biết cách viết test.  
- [ADR 0003: Outbox Pattern](../adr/0003-outbox-pattern.md) — Liên quan đến test messaging.  
- [ADR 0007: Message Semantics](../adr/0007-message-semantics.md) — Quy định consumer idempotent test.  

---

✅ Mọi người khi làm PR hãy đảm bảo tick đầy đủ checklist test trong [Pull Request Template](../../.github/pull_request_template.md).  
