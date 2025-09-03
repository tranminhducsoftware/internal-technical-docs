# 🗃️ Runbook: SQL Deadlock

1) Lấy deadlock graph (XE/DMV).
2) Xác định cặp truy vấn xung đột (update order + read summary?).
3) Biện pháp:
   - Giảm scope transaction; sử dụng snapshot isolation (đã cân nhắc).
   - Thêm index phù hợp; reorder DML để đồng nhất lock order.
   - Retry policy (Polly) 3-5 lần exponential backoff.
