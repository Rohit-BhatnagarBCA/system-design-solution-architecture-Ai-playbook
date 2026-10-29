# Scale Scenarios: 100K, 1M, 5M and 10M Registered Users

## Read this first

Registered-user count does not directly determine replica count. A product with 10 million accounts but low activity can have lower traffic than a smaller product with frequent real-time usage.

The table below is only a planning discussion starter. It is **not a sizing recommendation** and must not be used as a production capacity guarantee.

| Registered accounts | Initial architecture to evaluate | What to measure before sizing |
|---:|---|---|
| 100K | Modular monolith; managed relational DB; cache/queue only where useful | DAU, peak RPS, query latency, workload profile |
| 1M | Modular monolith may still fit; separate workers for expensive async tasks if needed | Peak RPS, DB saturation, queue age, availability targets |
| 5M | Evaluate workload isolation, read replicas, cache, partitioning and selected service extraction | Read/write mix, hot keys, storage growth, team ownership |
| 10M | Design from measured bottlenecks; evaluate multiple service/worker pools and database scaling options | Peak concurrency, regional needs, data distribution, recovery objectives |

Do not copy arbitrary replica bands from a user-count table. Size each workload from tested sustainable throughput and failure headroom.

## Required workload sheet

Fill this in for every scenario:
- Registered accounts:
- DAU / MAU:
- Requests per active user per day:
- Average RPS:
- Peak factor:
- Peak RPS:
- Read/write mix:
- Largest payload:
- Data created per day:
- Retention period:
- Availability and latency SLOs:
- Expected concurrent AI requests:
- AI requests per active user:
- Input/output tokens per request:
- Provider RPM/TPM limits:
- Monthly cost ceiling:

## Scaling approach

### Stage 1: Validate fundamentals
Use a modular monolith, correct indexes, security, observability and automated deployment. Load-test representative workflows.

### Stage 2: Scale stateless application capacity
Add replicas based on tested sustainable RPS per replica and failure/deployment headroom. Confirm database and provider limits can handle the added traffic.

### Stage 3: Separate asynchronous work
Move document processing, notifications, reports and other long tasks to queue-backed workers. Apply backpressure and idempotency.

### Stage 4: Optimize persistence
Tune queries, indexes and connection pools. Consider read replicas, partitioning or sharding only with workload evidence.

### Stage 5: Extract services selectively
Extract domains with independent scaling, release, ownership or isolation needs. Record an ADR and migration plan.

### Stage 6: Scale AI separately
Measure model concurrency, provider limits, token throughput, queue age, quality and cost. Separate AI workers/services only when the workload justifies it.

## Replica sizing example (illustrative formula)

If a load test shows one API replica sustainably handles 120 RPS while meeting the chosen latency and error SLOs, and estimated peak is 600 RPS:

`ceil(600 / 120) = 5 replicas`

Then add headroom for failure, deployments and burstiness, and verify dependencies can support the traffic. The 120 RPS figure is just an example—not a default Node.js capacity value.
