# ADR 0011: API Versioning & Deprecation Policy
**Status:** Accepted  
**Date:** 2025-09-03  
**Owner:** API Team

## Context
Tránh breaking change cho khách hàng; cần lộ trình deprecate rõ ràng.

## Decision
- Dùng `Asp.Versioning` theo **path** `/api/v{version}/...`.  
- Minimal hỗ trợ 2 version song song (current + previous).  
- Deprecation policy: thông báo ≥ 90 ngày; thêm header:
  - `Deprecation: true`, `Sunset: <date>`, link tới docs.
- Contract-first (OpenAPI) & **contract test** cho endpoints critical.

## Consequences
+ An toàn nâng cấp; khách hàng có thời gian migrate.  
– Tăng chi phí duy trì multi-version.

## Implementation Notes
- Swagger tách theo version; sample requests.  
- Backward-compat ưu tiên cao; tuyệt đối không breaking trong minor.

## Related
- ADR 0014 (Schema evolution — nếu dùng message schemas)
