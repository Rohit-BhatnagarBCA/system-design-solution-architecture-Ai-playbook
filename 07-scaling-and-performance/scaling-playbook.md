# Scaling and Performance Playbook

## Scale in this order
1. Establish baseline metrics and SLOs.
2. Load-test representative workflows.
3. Fix inefficient queries and algorithmic hot spots.
4. Add indexes and connection pooling based on evidence.
5. Add caching for measured hot reads.
6. Scale API replicas horizontally when the application is stateless and dependencies can handle the load.
7. Move long-running work to bounded background workers.
8. Tune queue concurrency and downstream quotas.
9. Add read replicas or partitioning when measurements justify them.
10. Consider service extraction or sharding only after documenting why simpler options are insufficient.

## Node.js-specific considerations
- Monitor event-loop delay, CPU, memory, garbage collection and open handles.
- Avoid blocking synchronous work in request paths.
- Stream large payloads when appropriate.
- Limit concurrency for expensive outbound calls.
- Use worker threads or external workers for CPU-heavy tasks.
- Set HTTP agent/socket pool limits intentionally.
- Use graceful shutdown and stop accepting work before termination.

## Load test scenarios
- Normal traffic
- Expected peak
- Short burst above peak
- One API replica unavailable
- Database latency elevated
- AI provider rate-limited or unavailable
- Queue consumers slowed
- Large but valid payloads
- Long-lived streaming responses

## Success criteria
A test passes only when agreed latency/error SLOs hold and downstream dependencies remain within safe capacity. Record test data, software version, environment and assumptions.
