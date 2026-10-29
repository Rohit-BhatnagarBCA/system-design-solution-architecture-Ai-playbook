# Modular Monolith

A modular monolith is one deployable application with explicit internal boundaries.

## Suggested structure

```text
src/
  app.js
  server.js
  modules/
    users/
      users.routes.js
      users.controller.js
      users.service.js
      users.repository.js
      users.validation.js
    orders/
      orders.routes.js
      orders.controller.js
      orders.service.js
      orders.repository.js
      orders.validation.js
    ai/
      ai.routes.js
      ai.controller.js
      ai.service.js
  infrastructure/
    database/
    cache/
    queue/
  shared/
    errors/
    logging/
  config/
```

## Boundary rules
- A module owns its domain logic and data-access operations.
- Other modules use public service interfaces, not private repository internals.
- Shared code must remain small and genuinely generic.
- Avoid circular dependencies.
- Do not let controllers contain business rules.
- External providers are wrapped behind adapters.

## Testing
- Unit-test domain logic.
- Test module contracts.
- Run integration tests against real or representative infrastructure.
- Add architecture tests or lint rules for import boundaries when the project grows.

## When to split a module
Split a module into a separate deployable service only after documenting the need, data ownership, communication contract, rollout plan and failure behavior.
