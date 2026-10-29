# Deployment and Cost Model

## Common deployment shape

```text
Clients
  |
DNS / CDN / WAF (where appropriate)
  |
Load Balancer / API Gateway
  |
Stateless Node.js API replicas
  |                \
  |                 -> Queue -> Background workers
  |
Database / Cache / Object storage
  |
External providers (email, payments, LLM)
```

The diagram is a logical example; a small system may not need every component.

## Environments
- Local development
- Test/CI
- Staging or pre-production
- Production

Use separate credentials and data boundaries. Never use production secrets in local development.

## Deployment practices
- Reproducible builds and dependency lockfiles
- Automated tests, linting and security checks
- Database migrations with rollback/forward-fix plan
- Health/readiness checks
- Graceful shutdown
- Rolling, canary or blue/green deployment as warranted
- Rollback criteria and ownership
- Infrastructure configuration in version control where appropriate

## Cost categories
- API compute and autoscaling
- Database compute, storage, IOPS, backups and replicas
- Cache
- Queue and workers
- Object storage and egress
- CDN/WAF/networking
- Logging, metrics, tracing and retention
- AI model input/output tokens, embeddings and reranking
- Support, security tooling and operational labor

## Cost estimation template
For each component record:
- Unit price and source/date checked
- Quantity and usage assumption
- Monthly estimate
- Scaling driver
- Cost alert/limit
- Confidence level

Pricing and service limits change. Verify current vendor pricing before approval. Avoid estimating cost from registered-user count alone.
