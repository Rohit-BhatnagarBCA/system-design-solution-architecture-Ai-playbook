# AI Failure Handling

## Common failure modes
- Provider timeout or outage
- Rate limit or quota exceeded
- Invalid or truncated model output
- Model returns an answer unsupported by retrieved sources
- Tool call fails or returns stale data
- Queue backlog
- Token budget exceeded
- Provider behavior changes after a model update

## Recommended controls
- Explicit timeouts and an overall deadline budget
- Bounded retries with exponential backoff and jitter for retryable errors
- No retries for permanent validation or authorization errors
- Circuit breaker or temporary suppression when a dependency is failing
- Per-user/tenant quotas and global provider limits
- Output schema validation and safe fallback responses
- Queue backpressure and dead-letter handling for asynchronous jobs
- Idempotency for side effects
- Human review for high-impact or uncertain outcomes
- Monitoring and runbooks

## Fallback strategy
A fallback can be:
- Return a safe, clear temporary-unavailable response.
- Offer a non-AI feature or cached, clearly labeled information.
- Queue the task for later processing.
- Use an approved alternate model only if privacy, quality and cost policies allow it.

Never invent an answer just because the provider failed. Do not silently downgrade to a model whose behavior has not been evaluated.
