# 🧰 Redis Keys

## Namespaces
- `auth:session:{userId}` → JWT/refresh + metadata (TTL 30m)
- `rate:{clientId}:{window}` → counters cho ASP.NET RateLimiter
- `order:read:{orderId}` → read-model snapshot (TTL 5m)
- `dedup:{messageId}` → idempotency (TTL 24h)

## Policies
- Eviction: allkeys-lru
- Maxmemory: 70% instance memory
- Cluster: 3 masters, 3 replicas; Hash slots auto-rebalance.
