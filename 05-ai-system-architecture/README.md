# AI System Architecture

## Suggested learning path
1. `ai-system-overview.md`
2. `ai-gateway-and-providers.md`
3. `prompt-management.md`
4. `rag-architecture.md` (when source-grounded answers are required)
5. `agents-tools-and-guardrails.md` (when model-driven tool use is required)
6. `evaluation-observability-cost.md`
7. `ai-failure-handling.md`

## Principle
Keep business authorization and data access in trusted application code. Treat model output, user content and retrieved content as untrusted. Add only the AI patterns required by the use case.
