# Observability and SLOs

## Three common pillars
- **Logs:** event details with timestamp, severity, request/trace ID and safe context.
- **Metrics:** time-series indicators such as request rate, error rate, latency and saturation.
- **Traces:** the path of a request across services and dependencies.

## Useful signals
- Traffic: requests per second and queue arrival rate
- Errors: failed requests, provider errors, job failures
- Latency: p50/p95/p99, dependency latency, time to first token
- Saturation: CPU, memory, event-loop delay, connection pools, queue depth
- Data: replication lag, slow queries, backup status
- AI: tokens, cost estimates, quality scores, safety events

## SLI, SLO and SLA
- SLI: the measured indicator.
- SLO: the target for that indicator over a defined window.
- SLA: an external commitment with consequences.

Do not label a target an SLA unless it is an actual agreed commitment.

## Alerting
Alert on user impact and actionable conditions, not every noisy metric. Define severity, owner, runbook and escalation path. Protect logs from secrets and unnecessary sensitive content.
