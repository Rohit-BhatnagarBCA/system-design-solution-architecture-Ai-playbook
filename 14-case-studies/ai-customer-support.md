# Case Study: AI Customer Support Assistant

## Goal
Help users find answers from approved product/support documentation, with escalation when evidence is missing.

## Initial architecture
A modular Node.js application with a conversation module, AI gateway and RAG pipeline. Document ingestion runs asynchronously.

## Request flow
1. Authenticate user and enforce tenant/account limits.
2. Classify or validate the support request if needed.
3. Retrieve relevant documents the user is permitted to access.
4. Build bounded context with source references.
5. Generate an answer through the approved provider.
6. Validate output and source references.
7. Return citations and an escalation option.
8. Record safe usage/quality telemetry.

## Safety and failure handling
- If retrieval finds no reliable evidence, say so and offer escalation.
- Do not invent product policy.
- Do not expose another tenant's documents.
- Treat uploaded/retrieved text as untrusted.
- Apply quotas and timeouts.
- Keep human support available for sensitive or unresolved cases.

## Success metrics
- Resolution rate with quality checks
- Correctness of cited sources
- Escalation rate
- User satisfaction
- p95 latency
- Cost per successfully resolved request
- Policy violations and data-access incidents
