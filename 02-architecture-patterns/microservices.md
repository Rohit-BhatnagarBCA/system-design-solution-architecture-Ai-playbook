# Microservices

Microservices split a system into independently deployable services aligned to business capabilities or bounded contexts.

## Benefits
- Independent release and scaling
- Clear service ownership
- Potential fault isolation
- Different technology choices when genuinely required

## Costs
- Network calls fail and add latency
- Data is distributed; cross-service transactions become harder
- Requires tracing, centralized logs, deployment automation and service authentication
- Contract compatibility and versioning become critical
- Local development and testing can become more complex

## Design rules
1. Define service boundaries around business capabilities, not tables.
2. Each service should own its data; avoid shared writable databases across services.
3. Use timeouts and bounded retries for remote calls.
4. Make retried commands idempotent.
5. Use an outbox or equivalent reliable event-publishing strategy when database writes and event publication must stay consistent.
6. Define API/event contracts and compatibility policy.
7. Instrument trace IDs across service boundaries.
8. Plan degraded behavior when dependencies are unavailable.

## Do not start here automatically

A team that lacks CI/CD, observability, operational ownership and mature testing may gain little from an early microservices split. First establish modular boundaries and automation.
