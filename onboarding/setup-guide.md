# 🛠️ Setup Môi Trường Local

## 1. Cài đặt công cụ
- .NET 8 SDK  
- Docker Desktop + Docker Compose  
- SQL Server client (Azure Data Studio / SSMS)  
- Redis client (RedisInsight)  
- RabbitMQ Management Plugin (http://localhost:15672)  
- VS Code hoặc Rider

## 2. Clone code & chạy services phụ thuộc
```bash
git clone https://github.com/our-org/our-repo.git
cd our-repo
docker compose up -d sqlserver redis rabbitmq
```
## 3. Apply migrations & seed data

```bash
dotnet ef database update --project src/Persistence

```
## 4. Run API
```bash
dotnet run --project src/Api
```
## 5. Verify
- Swagger: http://localhost:5000/swagger
- Health check: http://localhost:5000/healthz/ready
- Orleans Dashboard (nếu bật): http://localhost:8080
- ✅ Nếu tất cả đều OK → bạn đã sẵn sàng!