
---

## 4. `branching-strategy.md`
```markdown
```
# 🌿 Branching Strategy

## Model: Git Flow (simplified)
- `main`: production-ready.
- `develop`: integration branch.
- `feature/*`: tính năng mới.
- `bugfix/*`: sửa lỗi.
- `hotfix/*`: sửa nhanh trên `main`.

## Quy tắc
- Không commit trực tiếp vào `main`.
- PR vào `develop` cần review ≥ 1 người khác.
- Merge → squash commits (lịch sử gọn gàng).
- Tag release từ `main` (v1.0.0).

## Example
```bash
git checkout -b feature/add-order-service
git push origin feature/add-order-service
```