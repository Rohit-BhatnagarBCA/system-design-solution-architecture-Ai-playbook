# Node.js Backend Project Structure

This is a maintainable starting point for a modular Node.js API. Adjust it to the chosen framework and project size.

```text
src/
├── app.js
├── server.js
├── config/
│   ├── env.js
│   └── logger.js
├── modules/
│   ├── users/
│   │   ├── users.routes.js
│   │   ├── users.controller.js
│   │   ├── users.service.js
│   │   ├── users.repository.js
│   │   ├── users.validation.js
│   │   └── users.test.js
│   ├── products/
│   └── conversations/
├── ai/
│   ├── gateway/
│   ├── providers/
│   ├── prompts/
│   ├── workflows/
│   ├── rag/
│   ├── tools/
│   ├── guardrails/
│   ├── evaluation/
│   └── observability/
├── infrastructure/
│   ├── database/
│   ├── cache/
│   ├── queue/
│   └── storage/
├── middleware/
├── shared/
│   ├── errors/
│   ├── validation/
│   └── utils/
└── tests/
```

## Responsibility of each layer

- **Routes:** map HTTP paths to middleware and controllers.
- **Controllers:** translate HTTP input/output; keep business rules out.
- **Services:** enforce use cases and business rules.
- **Repositories:** encapsulate database queries.
- **Infrastructure:** implement database, cache, queue and storage integrations.
- **AI gateway/providers:** isolate model vendor APIs.
- **Validation:** validate request shape and domain constraints.
- **Middleware:** authentication, authorization, rate limits, request IDs and error handling.

## Example request flow

`HTTP request -> route -> auth/validation middleware -> controller -> service -> repository/provider -> response`

## Guardrails
- Validate environment variables at startup.
- Never commit `.env` or credentials.
- Use explicit API versioning.
- Return consistent error shapes without stack traces in production.
- Add request IDs and structured logs.
- Set timeouts for all outbound network calls.
- Avoid blocking the Node.js event loop with CPU-heavy synchronous work.
- Use worker threads or separate workers for CPU-heavy tasks where appropriate.
- Do not make database queries directly inside controllers.
