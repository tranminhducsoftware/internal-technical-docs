# ADR 0001: Use RabbitMQ for Messaging

**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** Platform Team

---

## Context
Hệ thống cần một message broker để xử lý:
- **Giao dịch bất đồng bộ** (đặt/hủy lệnh, thông báo trạng thái).  
- **Event-driven integration** giữa các service (API ↔ Orleans ↔ external).  
- **Đảm bảo tính tin cậy** (durability) và khả năng quan sát queue.  

Các ứng viên phổ biến: **RabbitMQ** và **Apache Kafka**.  

- RabbitMQ: hỗ trợ queue-based, routing linh hoạt, dễ vận hành.  
- Kafka: throughput rất cao, lưu trữ log dài hạn, phù hợp analytics và stream processing.  

## Options
1. **RabbitMQ**  
   + Queue semantics (work queue, fanout, topic).  
   + Quorum queues (HA, durability).  
   + Dễ vận hành, nhiều client SDK, UI management sẵn.  
   – Throughput giới hạn hơn Kafka; không tối ưu cho event log dài hạn.  

2. **Kafka**  
   + Throughput cực cao, partition scale.  
   + Lưu trữ event lâu dài, reprocessing dễ.  
   – Ops phức tạp hơn (Zookeeper/Controller quorum).  
   – Overkill cho use-case command/queue hiện tại.  

3. **Azure Service Bus / AWS SQS** (cloud-managed)  
   + Ít phải vận hành, tích hợp dễ.  
   – Vendor lock-in, latency cao hơn, chi phí.  

## Decision
- Chọn **RabbitMQ** làm message broker chính cho hệ thống.  
- Sử dụng **Quorum Queues** để đảm bảo HA/durability.  
- Cấu hình **DLX (Dead Letter Exchange)** cho error handling.  
- Tích hợp **Outbox Pattern** để publish event từ DB transaction sang RabbitMQ an toàn.  

## Consequences
+ Đơn giản hóa tích hợp, phù hợp throughput hiện tại.  
+ Dễ training & onboarding dev/ops.  
– Không phù hợp cho event sourcing/analytics dài hạn → có thể bổ sung Kafka song song trong tương lai.  

## Implementation Notes
- Exchange: `orders.exchange` (direct), `events.exchange` (topic).  
- Queue policy: `quorum.initial-group-size=3`, mirror all nodes.  
- DLX: `dead.exchange`, TTL retry 60s.  
- Monitoring: `messages_ready`, `unacked`, `consumers` qua Prometheus/RabbitMQ Exporter.  

## Related
- ADR 0003 (Outbox Pattern for reliable messaging)  
- ADR 0005 (Idempotency Keys for deduplication)  
- ADR 0007 (Message Semantics & Delivery Guarantees)
