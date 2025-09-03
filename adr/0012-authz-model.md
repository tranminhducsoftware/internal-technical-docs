# ADR 0012: Authorization Model — Roles & Policy Permissions
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** Platform Team

## Context
Cần phân quyền theo vai trò (Admin/Trader/Viewer) nhưng vẫn tinh chỉnh theo permission (vd: `order.place`, `order.cancel`).

## Decision
- Mô hình **Role + Policy-based Permissions**:
  - Role: nhóm coarse (Admin/Trader/Viewer).
  - Permission: claim `perm` đa giá trị; policy check bằng `IAuthorizationHandler`.
- Mapping:
  - Admin → `*`
  - Trader → `order.place`, `order.cancel`, `price.view`
  - Viewer → `price.view`
- Claims trong JWT (hoặc từ user store). Với request nhạy, **re-check** permissions từ DB/Cache (short TTL).

## Consequences
+ Linh hoạt; tách bạch role vs permission.  
– Cần tooling quản trị role/perm & audit thay đổi.

## Implementation Notes
- Cache permission theo userId ở Redis TTL 5m.  
- Endpoint annotate `[Authorize(Policy="CanPlaceOrder")]`.  
- Log quyết định `Denied` kèm `userId`, `perm missing`.

## Related
- ADR 0004 (Rate limit by user/client)  
- ADR 0009 (Secrets/JWT keys)
