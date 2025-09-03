# 🌾 Runbook: Orleans Silo Instability

Symptoms: activation drop, gateway unreachable, grain timeouts.

Steps:
1) Membership table health (SQL) — check `OrleansMembershipTable`.
2) Clock skew của node (NTP).
3) GC pressure (Server GC, Heap fragmentation).
4) Network: K8s service endpoints, HPA autoscale quá nhanh gây churn.
5) Mitigation:
   - Tăng `ResponseTimeout`.
   - Limit parallel silo restarts (rolling update strategy).
   - Persistent grain state provider health.
