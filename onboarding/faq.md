# ❓ FAQ Onboarding

### 1. Nếu chạy `dotnet ef database update` báo lỗi?
- Kiểm tra SQL Server container đã chạy chưa (`docker ps`).
- Connection string lấy từ `appsettings.Development.json`.

### 2. RabbitMQ không truy cập được?
- UI: http://localhost:15672 (user: guest/guest)
- Nếu lỗi → restart container `docker compose restart rabbitmq`

### 3. Redis key không thấy expire?
- Kiểm tra TTL: `TTL <key>`
- Nếu = -1 → key chưa set expiry → cần fix code.

### 4. Orleans silo không join cluster?
- Xem log `OrleansMembershipTable`
- Kiểm tra network K8s (service endpoint)

### 5. PR bị reject vì thiếu test?
- Xem `docs/testing/unit-test.md` để biết cách viết test chuẩn.
