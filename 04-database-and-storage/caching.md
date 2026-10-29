# Caching

Caching reduces repeated work, but adds invalidation and consistency complexity.

## Common layers
- Browser/client cache
- CDN cache for suitable static/public content
- Application cache (often Redis)
- Database buffer/cache

## Cache-aside flow

1. Read cache.
2. If present, validate freshness and return.
3. If absent, query source of truth.
4. Store with an appropriate TTL.
5. Return result.

## Design questions
- Is the data safe to share across users/tenants?
- What is the acceptable staleness window?
- What invalidates the cache?
- Can many requests cause a cache stampede?
- What happens when the cache is unavailable?
- Is the cache protected from unbounded key growth?

## AI caching cautions
- Cache deterministic, reusable results only when appropriate.
- Include tenant, authorization scope, prompt/model version and relevant context in cache keys.
- Do not reuse one user's private response for another user.
- Semantic cache matches can be incorrect; define similarity thresholds and evaluate quality.
- Respect data deletion and privacy requirements.
