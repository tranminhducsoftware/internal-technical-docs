
---

## 4. `performance-test.md`
```markdown
```
# 🚀 Performance Test Guidelines

## Tool
- JMeter hoặc k6.  
- Gatling (Scala) nếu cần advanced scenario.

## Scenario
- PlaceOrder: 70%  
- CancelOrder: 20%  
- Login/Refresh: 10%  

## Metrics cần đo
- P50, P95, P99 latency (API, message processing).
- Error rate (% failed requests).
- Consumer lag (RabbitMQ queue depth).
- Orleans activations, throughput.

## Threshold (baseline)
- P95 < 100ms (API).
- P95 < 300ms (async order confirm).
- Error rate < 1%.
- Silo CPU < 80%.

## CI/CD Integration
- Chạy nightly test với JMeter/k6.
- Fail build nếu vượt ngưỡng baseline.

## Báo cáo
- Export JMeter HTML report hoặc k6 JSON → Grafana dashboard.
