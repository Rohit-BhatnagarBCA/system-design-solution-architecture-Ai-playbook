# Reference Architecture: Node.js Microservices

## Example boundaries

```text
Client -> API Gateway
            |
     +------+------------------+
     |      |                  |
 Identity  Catalogue          AI API
 Service   Service             |
     |      |                  +--> Provider adapters
   DB A    DB B                +--> RAG/retrieval (if needed)
                                  |
                              Queue/Workers

Events -> Broker -> Notifications / Indexing / Analytics consumers
```

## Rules
- Each service owns its data and migrations.
- API/event contracts are versioned and tested.
- Use service identity and least-privilege permissions.
- Set deadlines, timeouts and bounded retries.
- Make consumers idempotent.
- Trace requests across services.
- Monitor each service and its dependencies.
- Define deployment ownership and on-call responsibility.

## Avoid
- Shared writable tables across services.
- Synchronous call chains with no deadline budget.
- Creating a service for every table.
- Assuming a broker automatically guarantees exactly-once business effects.
- Sending sensitive data to AI providers without approved policy.
