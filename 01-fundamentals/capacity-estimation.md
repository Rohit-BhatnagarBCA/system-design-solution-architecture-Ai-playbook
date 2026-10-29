# Capacity Estimation

Capacity estimates are hypotheses to test—not promises.

## 1. Web/API traffic

Definitions:
- Registered users: all accounts created.
- DAU: unique active users in a day.
- Concurrent users: users active at the same time.
- RPS: requests per second.
- Peak factor: peak traffic divided by average traffic.

Formula:

`Average RPS = (DAU × requests per active user per day) / 86,400`

`Peak RPS = Average RPS × peak factor`

Example:
- 80,000 DAU
- 60 API requests per active user per day
- Peak factor 5

Average RPS = 80,000 × 60 / 86,400 ≈ 55.6  
Estimated peak RPS ≈ 278

This is an aggregate estimate. Different endpoints have different costs; separate reads, writes, uploads, search and AI requests.

## 2. Replica estimate

A starting formula:

`Required replicas ≈ ceil(Peak RPS / tested sustainable RPS per replica)`

Then add appropriate headroom for:
- Failure of one replica or availability zone
- Deployment rolling capacity
- Traffic burstiness
- CPU, memory, event-loop lag and downstream connection limits

Do not use an assumed per-replica RPS without benchmarking the real application and dependencies.

## 3. Storage estimate

A rough first-pass model:

`Annual raw storage ≈ records per day × average bytes per record × 365`

Then account for:
- Index overhead
- Replicas and backups
- Retention and deletion policies
- Logs, attachments and generated files
- Growth and migration overhead

## 4. AI workload

Model AI independently from normal API traffic:
- AI requests per DAU per day
- Average and p95 input/output tokens
- Peak request concurrency
- Provider RPM/TPM limits
- Timeouts and streaming duration
- Retries and failed requests
- Queue wait time for asynchronous tasks

Estimate monthly cost using the current provider's actual pricing and the chosen model mix. Pricing changes; verify it before approving a budget.

## 5. Validate the model

1. Build a representative workload profile.
2. Load-test with realistic data and payloads.
3. Measure sustainable throughput before latency or error SLOs degrade.
4. Test a dependency slowdown and replica failure.
5. Compare predicted and observed CPU, memory, database connections and latency.
6. Record assumptions and update the estimate.
