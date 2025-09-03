# 💾 Backup & Restore SOP
- SQL: nightly full + 15-min log backups. Restore drill hàng quý.
- Redis: snapshot (RDB) cho config; data cache không restore.
- RabbitMQ: policy/definitions export (not queue data).
