# AI System Architecture Overview

## 1. Treat AI as a dependency, not as the source of authority

LLM output is probabilistic. The application must retain responsibility for identity, authorization, business rules, data integrity and consequential actions.

## 2. Common request flow

```text
Client
  |
API / Authentication / Rate Limit
  |
AI Use Case Service
  |-- Validate input and user permissions
  |-- Apply tenant/user quotas
  |-- Build context from authorized data
  |-- Select prompt/model/policy
  v
AI Gateway
  |-- Timeout and bounded retry policy
  |-- Provider adapter
  |-- Usage and latency telemetry
  v
Model Provider
  |
Output validation / policy checks
  |
Response to client or human-review workflow
```

For long-running work, use a queue and worker instead of holding an HTTP request open indefinitely.

## 3. Main responsibilities

- **Use case/workflow:** coordinates the product-specific task.
- **Gateway:** central policy boundary for provider calls.
- **Provider adapter:** translates a common internal request to a vendor-specific API.
- **Prompt registry:** tracks prompt templates and versions.
- **Retrieval/RAG:** fetches authorized relevant information when needed.
- **Tool layer:** exposes a narrow allowlist of validated application actions.
- **Guardrails:** input/output validation, safety checks and policy enforcement.
- **Evaluation:** measures quality, regressions and failure cases.
- **Observability:** captures latency, errors, token usage and cost without oversharing sensitive data.

## 4. Do not add every AI pattern by default

- Basic text generation may need only a use-case service, gateway and provider adapter.
- RAG is useful when responses need grounding in private or frequently updated documents.
- Tool calling is useful when the model needs to request controlled application actions.
- Agents are appropriate only when multi-step dynamic planning provides enough value to justify complexity.
- Fine-tuning is not the default first step; first test prompting, retrieval and model choice.

## 5. Safety boundary

The model may suggest an action. Trusted server code must validate the caller, authorize the target resource, validate arguments, enforce business rules and record the outcome before performing any consequential operation.

## 6. AI-specific SLOs

Consider:
- End-to-end latency and time-to-first-token
- Provider success/error rate
- Timeout and fallback rate
- Queue age for asynchronous jobs
- Evaluation quality on a representative dataset
- Unsafe-output / policy-violation rate
- Cost per successful task
- User feedback and escalation rate
