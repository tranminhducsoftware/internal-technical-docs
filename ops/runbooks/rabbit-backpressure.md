# 🐰 Runbook: RabbitMQ Backpressure (messages_ready tăng liên tục)

Symptoms: `messages_ready` ↑, `consumers` ít, API timeout.

Steps:
1) Check queue depth & rate:
   - `rabbitmqctl list_queues name messages_ready messages_unacknowledged consumers`
2) Scale consumers:
   - `kubectl scale deploy/orders-consumer --replicas=...`
3) Kiểm tra prefetch (QoS) & ack đảm bảo không ack quá chậm.
4) DLQ rate: nếu tăng → inspect message payload lỗi.
5) Tạm thời bật lazy queues nếu memory áp lực cao.
6) Nếu vẫn tắc → bật rate limit producer hoặc tách queue theo routing key.
