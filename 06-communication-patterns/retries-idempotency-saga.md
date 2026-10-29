# Retries, Idempotency and Saga Pattern

## Retries
Use retries only when:
- The error is transient.
- The operation is safe to retry or has idempotency protection.
- The retry fits within the overall deadline.
- The retry policy is bounded and uses backoff/jitter.

Avoid retry storms. Multiple layers each retrying can multiply traffic dramatically.

## Idempotency
An operation is idempotent when repeating the same logical request does not repeat its side effect.

For important write APIs:
- Accept or generate an idempotency key.
- Scope it to caller and operation.
- Store result/state atomically with the operation where possible.
- Reject reuse with a conflicting payload.
- Define key retention.

## Saga
A saga coordinates a multi-step business process across services using local transactions and compensating actions. Compensation is not always a perfect rollback.

Use a saga only when a workflow truly spans independently owned services. A single database transaction is simpler when it fits the requirements.
