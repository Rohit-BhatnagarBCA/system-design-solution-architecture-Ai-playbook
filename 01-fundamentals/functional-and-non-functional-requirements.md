# Requirements: Functional and Non-Functional

## Functional requirements template

For each capability, define:
- Actor
- Trigger
- Preconditions
- Main success path
- Failure and edge cases
- Authorization rule
- Data created or changed
- Audit requirement

Example: `POST /api/v1/ai/answers`
- Actor: authenticated user
- Trigger: submits a question
- Preconditions: account is active and quota is available
- Success: a validated answer or accepted asynchronous job is returned
- Failure: request validation, quota, provider timeout or policy rejection
- Data: conversation metadata, usage record and permitted audit metadata
- Authorization: user can access only their own conversation

## Non-functional requirements checklist

| Area | Questions |
|---|---|
| Availability | What downtime is acceptable? |
| Latency | Which percentile and endpoint are measured? |
| Throughput | Average and peak RPS? |
| Durability | Which data loss window is acceptable? |
| Consistency | Strong, eventual or read-your-writes? |
| Security | Authentication, authorization, encryption, audit? |
| Privacy | Which data is sensitive and how long is it retained? |
| Scale | Which dimensions are expected to grow? |
| Operability | Who deploys, monitors and responds to incidents? |
| Cost | What is the budget per user, request or month? |
| AI quality | What is an acceptable answer-quality threshold? |
| AI safety | Which actions and outputs are prohibited? |

## Avoid vague requirements

Instead of “the API must be fast,” define an endpoint, workload and percentile:
“Under the agreed test profile, p95 latency for `GET /products` must remain below 250 ms at 500 requests/second.”

Instead of “AI must be accurate,” define a representative evaluation dataset, scoring rubric, minimum threshold and human-review process for high-impact use cases.
