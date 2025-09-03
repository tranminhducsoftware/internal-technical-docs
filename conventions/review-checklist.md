# ✅ Code Review Checklist

## 1. Code Quality
- [ ] Tuân thủ **Coding Style** ([coding-style.md](./coding-style.md))
- [ ] Không có **code smell** (duplicated, dead code, magic number…)
- [ ] Đặt tên biến/hàm/class **rõ ràng**, dễ hiểu
- [ ] Tách logic phức tạp thành hàm nhỏ, có unit test

## 2. Architecture & Design
- [ ] Đúng **Clean Architecture** (Api → Application → Domain → Infrastructure)
- [ ] Không vi phạm dependency rule (ví dụ: Application không tham chiếu Infrastructure)
- [ ] Nếu có quyết định kiến trúc mới → ADR đã được thêm hoặc cập nhật

## 3. Testing
- [ ] Đã có **Unit Test** cho logic mới/thay đổi
- [ ] Đã có **Integration Test** nếu liên quan DB, Redis, RabbitMQ, Orleans
- [ ] Test **pass** trong CI pipeline
- [ ] Coverage ở mức chấp nhận được (≥ 80% Application layer)

## 4. Security
- [ ] Không hardcode **secrets/connection string**
- [ ] API mới tuân thủ **AuthN/AuthZ** ([ADR 0012](../adr/0012-authz-model.md))
- [ ] Input validation đầy đủ (FluentValidation, DTO validation)
- [ ] Không log dữ liệu nhạy cảm (password, token, PII)

## 5. Observability
- [ ] Có **logging** đủ context (traceId, userId, clientId)
- [ ] Có **metrics/tracing** nếu thêm endpoint/flow quan trọng
- [ ] Error handling chuẩn (`ProblemDetails` response)

## 6. Documentation
- [ ] PR có mô tả rõ ràng, dễ hiểu
- [ ] Update docs (README, features, ops) nếu thay đổi liên quan
- [ ] Update **ADR** nếu có quyết định kiến trúc mới
- [ ] Nếu ảnh hưởng setup → update [onboarding/setup-guide.md](../onboarding/setup-guide.md)

## 7. Git & Workflow
- [ ] Branch name đúng convention (`feature/*`, `bugfix/*`)
- [ ] Commit message theo chuẩn ([commit-conventions.md](./commit-conventions.md))
- [ ] Không commit file build/output
- [ ] PR nhỏ, scope rõ ràng, không “tất cả trong một”

---

📌 **Nguyên tắc review**:
- Review code, **không review cá nhân**  
- Nếu phát hiện bug/issue → ghi rõ lý do, gợi ý cách fix  
- Nếu chỉ là style/preference → comment nhẹ, không block merge  
