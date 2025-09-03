# 🚀 Release vX.Y.Z

**Date:** YYYY-MM-DD  
**Owner:** <Team/Người phụ trách>  

---

## 🆕 Highlights
- Tóm tắt ngắn gọn 2–3 dòng về điểm mới trong phiên bản này.
- Ví dụ: Thêm tính năng Rate Limiting cho API public, cải thiện logging cho Orleans grains.

---

## ✨ Added
- Các tính năng mới.
- Ví dụ:  
  - feat(auth): JWT refresh token rotation  
  - feat(order): hỗ trợ Idempotency-Key trong API đặt lệnh  

---

## 🔄 Changed
- Thay đổi behavior, config, hoặc cải tiến.  
- Ví dụ:  
  - update(api): đổi response format lỗi sang chuẩn ProblemDetails  
  - update(orleans): tối ưu kích thước batch write SQL  

---

## 🐛 Fixed
- Các bug đã được sửa.  
- Ví dụ:  
  - fix(auth): lỗi refresh token bị revoke sai khi user login nhiều device  
  - fix(rabbitmq): consumer không ack message khi timeout  

---

## 🗑️ Removed
- Tính năng bị bỏ hoặc API deprecated.  
- Ví dụ:  
  - remove(api): gỡ endpoint cũ `/api/v1/orders/old`  

---

## ⚠️ Known Issues
- Các vấn đề còn tồn tại chưa fix.  
- Ví dụ: Khi load cao > 10k req/min, API `/pricing/stream` có thể delay 200–300ms.  

---

## 🧭 Migration Notes
- Hướng dẫn cho dev/ops khi upgrade version này.  
- Ví dụ:  
  - Chạy `dotnet ef database update` để apply migration `AddRefreshTokenTable`.  
  - Update Helm values để bật metrics mới `/metrics/prometheus`.  

---

## 🔗 Related
- [Changelog](./changelog.md)  
- ADR liên quan: [0004-rate-limiter-strategy.md](../adr/0004-rate-limiter-strategy.md)  
- PR liên quan: #123, #124  

---
