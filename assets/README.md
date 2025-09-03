# 🗂️ Assets Directory

## Mục tiêu
Thư mục `assets/` lưu trữ **tài nguyên hỗ trợ cho tài liệu** như sơ đồ, hình ảnh, biểu đồ, mockup.  
Mục đích: giúp tài liệu **dễ hiểu, trực quan** và giữ tất cả hình ảnh liên quan trong một nơi duy nhất.

---

## Các loại assets

### 1. Sơ đồ kiến trúc & kỹ thuật
- System architecture (high-level)
- Deployment (Kubernetes, Cloud)
- C4 Diagrams (Context, Container, Component, Code)

👉 Ví dụ:  
- `architecture/system-architecture.png`  
- `architecture/deployment-k8s.svg`

---

### 2. Database & Data Models
- ERD (Entity Relationship Diagram)
- Schema diagram

👉 Ví dụ:  
- `data-model/order-erd.png`  
- `data-model/auth-db-schema.svg`

---

### 3. Feature & Workflow Diagrams
- Flow chart cho use-case (Login, Place Order, Pricing stream)
- State machine (Order lifecycle)

👉 Ví dụ:  
- `features/order-flow.png`  
- `features/auth-login-sequence.svg`

---

### 4. Screenshots / UI Mockups
- Swagger screenshots
- Grafana dashboards
- Wireframes từ Figma

👉 Ví dụ:  
- `screenshots/swagger-auth.png`  
- `screenshots/grafana-dashboard.png`

---

### 5. Icons & Symbols
- Logo dịch vụ (RabbitMQ, Redis, Orleans, SQL Server)
- Hình minh họa dùng trong diagrams

👉 Ví dụ:  
- `icons/orleans-logo.png`  
- `icons/rabbitmq.svg`

---

## Convention đặt tên file
- **kebab-case** (chữ thường, ngăn cách bằng `-`)  
- Miêu tả ngắn gọn nội dung file  
- Thêm suffix theo nhóm nếu cần:  
  - `-diagram` (cho sơ đồ)  
  - `
