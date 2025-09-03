# ⚙️ Operations Documentation (Ops)

## Mục tiêu
Thư mục `ops/` lưu trữ tài liệu vận hành hệ thống:  
- **SOPs (Standard Operating Procedures):** Quy trình chuẩn, lặp đi lặp lại hằng ngày hoặc khi cần thao tác (deploy, backup, monitoring...).  
- **Runbooks:** Hướng dẫn xử lý **sự cố cụ thể**, giúp giảm MTTR khi hệ thống gặp vấn đề.

---

## Các thành phần

### 1. [SOPs](./sop/)
- **[deployment.md](./sop/deployment.md):** Quy trình chuẩn để deploy qua ArgoCD/Kubernetes.  
- **[monitoring.md](./sop/monitoring.md):** Cách kiểm tra dashboards & alert thresholds.  
- **[backup-restore.md](./sop/backup-restore.md):** Quy trình backup/restore DB, Redis, RabbitMQ.  
- **[security.md](./sop/security.md):** Quản lý secrets, key rotation, TLS certificates.  

👉 SOP = **công việc chuẩn** mà dev/ops nào cũng có thể làm theo.

---

### 2. [Runbooks](./runbooks/)
- **[api-down.md](./runbooks/api-down.md):** API không lên → cách kiểm tra pod/logs & rollback.  
- **[db-connection.md](./runbooks/db-connection.md):** DB connection error → bước check SQL Server & secrets.  
- **[kafka-lag.md](./runbooks/kafka-lag.md) / [rabbit-backpressure.md](./runbooks/rabbit-backpressure.md):** Queue lag, backlog tăng.  
- **[redis-timeout.md](./runbooks/redis-timeout.md):** Redis timeout → scale & check eviction.  
- **[sql-deadlock.md](./runbooks/sql-deadlock.md):** Xử lý deadlock EF/SQL.  
- **[orleans-silo.md](./runbooks/orleans-silo.md):** Orleans silo không ổn định → membership, GC, network.  
- **[token-leak.md](./runbooks/token-leak.md):** Token/secret bị lộ → revoke, rotate, audit log.  

👉 Runbook = **xử lý tình huống khẩn cấp**, "nếu X thì làm Y".

---

## Convention
- **Tên file**: lowercase-kebab-case (`api-down.md`, `db-connection.md`).  
- Mỗi SOP/Runbook có cấu trúc:  
  1. **Context** / Symptoms  
  2. **Steps** chi tiết (CLI, dashboard, logs)  
  3. **Rollback / Recovery** nếu có  
  4. **Escalation** (ai liên hệ nếu không xử lý được)  

---

## Tổ chức thư mục
```yaml
/docs/ops
│── README.md
│── sop/ # Quy trình chuẩn
└── runbooks/ # Xử lý sự cố
```

---

## Best practice
- Luôn link Runbook từ **alert rule** (Grafana/Prometheus).  
- SOP viết rõ từng bước, không mơ hồ → ai cũng có thể làm theo.  
- Khi gặp sự cố mới chưa có Runbook → sau khi xử lý xong phải bổ sung file mới.  
- Các SOP/Runbook quan trọng phải được **review định kỳ** để tránh lỗi thời.

---
