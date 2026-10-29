# Reference Architecture: Node.js AI Monolith

## Goal
A single Node.js deployable application with clear internal modules and a controlled AI integration boundary.

## Logical design

```text
Web / Mobile Client
        |
     HTTPS API
        |
Authentication + Validation + Quotas
        |
Use Case / Business Modules
        |
        +---- Domain Database
        |
        +---- AI Module
                 |
              AI Gateway
                 |
          Provider Adapter
                 |
          External LLM API

Optional:
- Redis for cache/rate-limit state
- Queue + worker for long-running tasks
- Object storage + ingestion worker for RAG documents
```

## Suggested source structure

```text
src/
  app.js
  server.js
  config/
  modules/
    users/
    conversations/
  ai/
    gateway/
    providers/
    prompts/
    workflows/
    guardrails/
    evaluation/
    observability/
    rag/             # Add only if retrieval is required
    tools/           # Add only if tool use is required
  infrastructure/
    database/
    cache/
    queue/
    storage/
  middleware/
  shared/
  tests/
```

## Key decisions
- Keep authentication and business authorization in trusted server code.
- Hide provider-specific details behind an adapter.
- Use timeouts, bounded retries, usage quotas and safe errors.
- Use a queue for long-running ingestion or batch tasks.
- Add RAG only if private/current source data is needed.
- Use strict tool allowlists and approvals for consequential actions.
- Evaluate quality, safety and cost before model/prompt changes.

## Evolution triggers
Consider separate workers or services when AI traffic requires different scaling, long tasks hurt API latency, provider policy needs isolation, or team/deployment boundaries justify the added complexity.
