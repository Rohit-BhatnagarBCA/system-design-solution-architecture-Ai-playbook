# AI Gateway and Provider Adapters

## Purpose

Keep provider-specific API details out of business logic. A gateway can centralize policy, while provider adapters implement vendor-specific calls.

## Example TypeScript-like interface (conceptual)

```ts
export type GenerateInput = {
  model: string;
  systemPrompt: string;
  userPrompt: string;
  maxOutputTokens: number;
  timeoutMs: number;
};

export type GenerateOutput = {
  text: string;
  provider: string;
  model: string;
  inputTokens?: number;
  outputTokens?: number;
};

export interface ModelProvider {
  generate(input: GenerateInput): Promise<GenerateOutput>;
}
```

This is an interface example, not a complete production implementation. Adapt it to the chosen SDK and its supported capabilities.

## Responsibilities
- Select only approved providers/models.
- Apply request and output limits.
- Set explicit timeouts.
- Use bounded retries only for retryable failures.
- Apply user/tenant budgets and provider quotas.
- Normalize errors without hiding important operational context.
- Capture latency, request IDs and token usage.
- Keep API keys in a secret manager or protected environment configuration.
- Support safe model/provider rollout and evaluation.

## Failover cautions

Failing over to another provider may change model quality, behavior, latency, data processing terms and cost. Define approved fallback models and evaluate them before use. Do not automatically send sensitive data to a new provider without policy approval.

## What should not be in the gateway?
- Product-specific authorization decisions that belong to the use case.
- Unrestricted tools or database access.
- Hidden, unbounded retry loops.
- Raw secret logging.
- A hard-coded assumption that every provider supports the same features.
