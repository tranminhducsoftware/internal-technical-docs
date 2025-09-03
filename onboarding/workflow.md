
---

## 3. `workflow.md`
```markdown
```
# 🔄 Workflow Làm Việc

## Branching
- `main`: production ready
- `develop`: integration branch
- Feature branch: `feature/<name>`
- Bugfix branch: `bugfix/<ticket-id>`

## Git Convention
- Commit: `<type>(<scope>): <message>`
  - feat(order): add cancel order command
  - fix(auth): refresh token rotation bug
- PR cần có reviewer khác duyệt.

## CI/CD
- Push → GitHub Actions build + test
- Image push → Registry
- ArgoCD sync → Dev/Staging/Prod

## Code Review Checklist
- Đúng coding style (editorconfig)
- Có unit test/integration test
- Logging, error handling đầy đủ
- ADR updated nếu có quyết định mới
