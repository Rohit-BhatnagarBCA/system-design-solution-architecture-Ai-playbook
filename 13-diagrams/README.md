# Architecture Diagrams

Use diagrams to communicate boundaries and behavior. Mermaid is convenient for diagrams stored in Markdown and reviewed in Git.

## System context

```mermaid
flowchart LR
  User[User] --> App[Application]
  App --> LLM[External AI Provider]
  App --> DB[(Database)]
  App --> Store[(Object Storage)]
```

## Sequence diagram

```mermaid
sequenceDiagram
  participant U as User
  participant API as Node.js API
  participant Auth as Authorization
  participant AI as AI Gateway
  participant LLM as Model Provider
  U->>API: Submit question
  API->>Auth: Check access and quota
  Auth-->>API: Allowed
  API->>AI: Validated use-case request
  AI->>LLM: Provider request
  LLM-->>AI: Model output
  AI-->>API: Normalized result
  API-->>U: Validated response
```

## Diagram checklist
- Show trust boundaries.
- Label synchronous vs asynchronous calls.
- Show data ownership and external dependencies.
- Include failure paths for critical workflows.
- Avoid placing secrets or real personal data in diagrams.
- Keep diagrams aligned with ADRs and implementation.
