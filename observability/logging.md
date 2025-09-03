
---

# 9) `observability/logging.md` + `tracing.md` + `metrics.md`

```markdown
# 📊 Logging (Serilog)
- Output: JSON; enrich: `TraceId`, `SpanId`, `UserId`, `ClientId`, `App`, `Env`.
- MinimumLevel: Information (Prod), Debug (Dev).
- Sensitive fields: mask (password, token, card…).

