# 🔗 Dependencies Documentation

## Mục tiêu
Thư mục `dependencies/` lưu trữ thông tin về **các phụ thuộc bên ngoài và nội bộ** mà hệ thống sử dụng.  
Mục đích: giúp team nắm rõ hệ thống **tương tác với ai, qua đâu, bằng cách nào**, và tránh quên khi maintain hoặc troubleshoot.

---

## Các loại dependencies

### 1. External APIs (`external-apis.md`)
- Liệt kê toàn bộ API bên ngoài mà hệ thống gọi đến (CoreBank API, Liquidity Provider, Payment Gateway…).  
- Thông tin cần có:
  - Base URL / Endpoint  
  - Auth (JWT, mTLS, API key)  
  - Rate limit & retry policy  
  - Chủ sở hữu (team nào quản lý API đó)  

---

### 2. Messaging (`rabbitmq-queues.md` hoặc `kafka-topics.md`)
- Liệt kê các **queue/topic** dùng trong hệ thống.  
- Thông tin cần có:
  - Tên exchange/queue/topic  
  - Routing key / partition  
  - Loại (direct, topic, quorum queue, DLQ…)  
  - Policy (TTL, DLX, quorum, retention)  
  - Producer/Consumer là service nào  

---

### 3. Redis Keys (`redis-keys.md`)
- Document hóa các key pattern quan trọng.  
- Thông tin cần có:
  - Namespace (`auth:session:{userId}`)  
  - TTL  
  - Dữ liệu lưu (JWT, refresh token, cache order…)  
  - Mục đích (auth, caching, idempotency, rate limiting)  

---

## Convention đặt tên file
- `external-apis.md` — API bên ngoài  
- `rabbitmq-queues.md` — cấu hình RabbitMQ (hoặc `kafka-topics.md` nếu dùng Kafka)  
- `redis-keys.md` — Redis key pattern  

👉 Các file nên tách nhỏ, không nhồi tất cả vào 1 file để dễ maintain.

---

## Tổ chức thư mục
```yaml
/docs/dependencies
│── external-apis.md # API tích hợp bên ngoài
│── rabbitmq-queues.md # Queues & Exchanges (hoặc kafka-topics.md)
└── redis-keys.md # Key patterns trong Redis
```

---

## Best practice
- Mỗi khi thêm **integration mới**, phải thêm entry ở `dependencies/`.  
- Nếu đổi queue/topic hoặc Redis key pattern → update ngay.  
- Luôn ghi rõ **team owner** để dễ liên hệ khi sự cố.  
- ADR nào liên quan (ví dụ: ADR 0001 Use RabbitMQ, ADR 0013 Cache Strategy) nên link trong phần cuối file.  

Ví dụ link trong doc:  
```markdown
```
Xem thêm [ADR 0001: Use RabbitMQ](../adr/0001-use-rabbitMQ.md)
