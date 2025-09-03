# 📥 Pull Request Template

## 🔍 Summary
- Mô tả ngắn gọn PR này làm gì, tại sao cần.

## ✅ Checklist

### Code & Testing
- [ ] Code tuân thủ coding style (.editorconfig, conventions).
- [ ] Đã viết **Unit Test** cho logic mới/thay đổi.
- [ ] Đã viết **Integration Test** nếu có I/O (DB, RabbitMQ, Redis, Orleans).
- [ ] Đã chạy **tất cả test** (`dotnet test`, integration suite).
- [ ] Không phá vỡ contract API (Swagger/OpenAPI updated).

### Documentation
- [ ] Cập nhật docs nếu có thay đổi kiến trúc/feature.
- [ ] ADR liên quan được tạo/cập nhật (nếu quyết định mới).
- [ ] README hoặc Onboarding guide updated (nếu ảnh hưởng dev setup).

### Observability
- [ ] Đã thêm log/tracing cho flows quan trọng.
- [ ] Metric mới (nếu có) đã được expose cho Prometheus.

### Security
- [ ] Secrets không bị hardcode.
- [ ] Role/Permission đã cập nhật theo `docs/adr/0012-authz-model.md`.

## 📸 Screenshots / Evidence (nếu cần UI hoặc API response)

## 🧩 Related ADR / Issues / Tickets
- Liên kết ADR hoặc Jira/GitHub issue
