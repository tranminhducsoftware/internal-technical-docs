# 📏 API Guidelines (.NET 8)

## Routing
- Minimal API/Controllers theo resource: `/api/v1/orders/{id}`
- Tránh “verbs” trong route: dùng HTTP method để phân biệt.

## Versioning
- `Asp.Versioning` → `/api/v1/*`
- Deprecation header khi retire endpoint.

## Rate Limiting
- **Fixed window** cho public; **token bucket** cho internal.
- Key: clientId hoặc userId (fallback IP).
- 429 trả về `Retry-After` + `traceId`.

## AuthZ (Role/Permission)
- Role coarse (Admin/Trader/Viewer).
- Permission fine-grained (policy-based) dùng `IAuthorizationHandler`.

## Errors
```json
{
  "error": "ValidationError",
  "message": "Price must be > 0",
  "details": [{"field":"price","issue":"min:0"}],
  "traceId": "00-7a...-01"
}
```
## Security
- Tất cả API phải yêu cầu JWT (bearer token).
- Role + Policy-based authorization (xem ADR 0012).
- Không trả error chi tiết về auth (401/403 generic).