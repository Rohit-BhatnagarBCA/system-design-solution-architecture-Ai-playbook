# Event-Driven Architecture

Components communicate by publishing events that describe facts which have happened, such as `OrderPlaced` or `DocumentUploaded`.

## Common flow

```text
API -> Domain Service -> Database + Outbox
                         |
                         v
                   Outbox Publisher
                         |
                         v
                     Message Broker
                      /         \
                     v           v
               Email Worker   AI Indexing Worker
```

## Benefits
- Producers do not need to know every consumer.
- Work can be processed asynchronously.
- Queues can smooth bursts.
- Multiple consumers can react to the same business event.

## Trade-offs
- Consumers may process messages more than once.
- Ordering may be limited or partition-specific.
- Events introduce eventual consistency.
- Debugging requires correlation IDs and event tracing.

## Reliability checklist
- Define event schema and versioning.
- Use idempotent consumers.
- Configure retries with backoff and jitter.
- Route repeatedly failing messages to a dead-letter queue.
- Monitor queue depth and oldest-message age.
- Decide ordering and retention requirements.
- Avoid publishing secrets or unnecessary personal data in events.
