# 📘 Feature Specifications

## Mục tiêu
- Ghi lại **cách thiết kế** và **yêu cầu chi tiết** của từng tính năng.  
- Tránh việc dev mới chỉ hiểu qua code → phải có tài liệu mô tả business context, API contract, data model.  
- Là cầu nối giữa **Business Analyst ↔ Dev ↔ QA**.

---

## Cấu trúc 1 file Feature Spec

Mỗi tính năng nên có 6 phần:

1. **Title + ID**
   - Ví dụ: `Feature: User Authentication (FEAT-001)`
   - Giúp trace trong backlog / issue tracker.

2. **Business Context**
   - Mục tiêu tính năng, vì sao cần.
   - Ai là người dùng (persona).
   - Giá trị nghiệp vụ.

3. **Requirements**
   - Functional: API, flow, business rules.
   - Non-functional: performance, security, compliance.

4. **API Contract**
   - REST/GraphQL/gRPC spec.
   - Request/Response JSON + status codes.
   - Error cases.

5. **Flow Diagram**
   - Sequence diagram (Mermaid).
   - State machine (nếu có state chuyển đổi).

6. **Data Model**
   - Entity/ERD diagram.
   - Mapping sang DB table/Grain/Redis key.

---

## Best Practices
- **Ngắn gọn, đủ ý**, không lan man.
- Viết **use-case cụ thể** thay vì chung chung.
- Dùng **Mermaid** để vẽ flow cho dễ đọc trong GitHub.
- Link sang:
  - [ADR liên quan](../adr/README.md)
  - [Ops Runbook](../ops/runbooks/)
  - [Testing Guidelines](../testing/)

---

## Ví dụ
- [auth-login.md](./auth-login.md)  
- [order-placement.md](./order-placement.md)  
