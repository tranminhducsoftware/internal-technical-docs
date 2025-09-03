# 🗒️ Work Logs

## Mục tiêu
- Ghi lại **lịch sử công việc hằng ngày** của từng thành viên.  
- Mỗi ngày 1 file `YYYY-MM-DD.md`.  
- Giúp team sync nhanh trong daily standup và retrospective.

## Cấu trúc 1 file log
Mỗi thành viên trả lời 3 câu:
1. Hôm qua tôi đã làm gì?  
2. Hôm nay tôi sẽ làm gì?  
3. Có vướng mắc gì không?

👉 Giữ ngắn gọn, tập trung vào **tiến độ & blocker**.


# 📅 Work Log — 2025-09-04

## Đức
- Hôm qua: 
  - Viết ADR 0005 (Idempotency Keys).
  - Fix bug refresh token rotation trong auth service.
- Hôm nay:
  - Viết runbook `redis-timeout.md`.
  - Bắt đầu integration test cho OrderGrain.
- Blocker: cần review ADR 0005 từ team.

---

## Lan
- Hôm qua:
  - Thêm unit test cho PricingService.
  - Update onboarding `setup-guide.md`.
- Hôm nay:
  - Viết feature spec `order-history.md`.
- Blocker: chưa có thông tin rõ từ BA về API order history.

---

## Nam
- Hôm qua:
  - Cấu hình Prometheus scrape Orleans metrics.
- Hôm nay:
  - Tạo Grafana dashboard cho Order latency.
- Blocker: chưa có quyền access vào staging cluster.
