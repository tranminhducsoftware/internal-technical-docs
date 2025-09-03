# 🛣️ Product & Technical Roadmap

## Mục tiêu
Tài liệu này định hướng **phát triển dài hạn** của hệ thống:  
- Giúp team biết **ưu tiên** (priority) trong từng quý.  
- Liên kết giữa **business goals** ↔ **technical decisions** (ADR, features, releases).  
- Tránh làm trùng lặp hoặc thiếu đồng bộ khi nhiều team cùng phát triển.

---

## Nguyên tắc
- Roadmap được chia theo **quý (Q1, Q2, Q3, Q4)** hoặc **tháng** nếu cần chi tiết.  
- Mỗi mục gồm:  
  - 🎯 Business Goal  
  - 🛠️ Technical Deliverables (features, infra, ADR liên quan)  
  - 📅 Timeline dự kiến  
  - 👤 Owner  

---

## 2025 Roadmap (ví dụ)

### Q1 (Jan–Mar)
- 🎯 **Stabilize Core Trading System**
  - 🛠️ Hoàn thiện [Auth & Login](./features/auth-login.md)  
  - 🛠️ Release [v1.0](./releases/v1.0.md)  
  - 🛠️ ADR: [0001-use-rabbitMQ.md](./adr/0001-use-rabbitMQ.md), [0003-outbox-pattern.md](./adr/0003-outbox-pattern.md)  
  - 👤 Owner: Platform Team  

### Q2 (Apr–Jun)
- 🎯 **Scalability & Reliability**
  - 🛠️ Thêm [Rate Limiting](./features/order-placement.md#requirements) (ADR 0004)  
  - 🛠️ Bổ sung monitoring & runbook cho Orleans silo ([orleans-silo.md](./ops/runbooks/orleans-silo.md))  
  - 🛠️ Release [v1.1](./releases/v1.1.md)  
  - 👤 Owner: Platform + Ops Team  

### Q3 (Jul–Sep)
- 🎯 **Advanced Features**
  - 🛠️ [Pricing Stream](./features/pricing-stream.md) + WebSocket API  
  - 🛠️ ADR: [0008-saga-style.md](./adr/0008-saga-style.md) cho Order Lifecycle  
  - 🛠️ Release v1.2  
  - 👤 Owner: Trading Team  

### Q4 (Oct–Dec)
- 🎯 **Security & Compliance**
  - 🛠️ ADR: [0009-secrets-management.md](./adr/0009-secrets-management.md)  
  - 🛠️ Thêm audit log, chuẩn hóa [observability](./observability/README.md)  
  - 🛠️ PCI/GDPR compliance checklist  
  - 👤 Owner: Security Team  

---

## Liên quan
- [Features](./features/README.md)  
- [ADR Index](./adr/README.md)  
- [Releases](./releases/README.md)  
- [Ops](./ops/README.md)  

---

## Best practice
- Roadmap **không phải commit cứng**, mà là **định hướng** (có thể thay đổi khi business thay đổi).  
- Update roadmap **ít nhất mỗi quý**.  
- Luôn link sang feature/ADR/release cụ thể để team dễ trace.  
- Nếu có dependency giữa các mục (ví dụ: Pricing stream cần ADR saga trước), hãy ghi rõ.  

---
