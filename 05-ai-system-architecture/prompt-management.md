# Prompt Management

## Goals
- Version prompts.
- Review changes.
- Test against representative examples.
- Track which version produced a result.
- Avoid mixing authorization logic into natural-language instructions.

## Suggested layout

```text
ai/prompts/
  registry.js
  templates/
    support-answer.v1.md
    document-summary.v1.md
  evaluations/
    support-answer-cases.jsonl
```

## Prompt change process
1. State the task and expected output.
2. Define input variables and size limits.
3. Include only authorized context.
4. Define output schema when structured data is required.
5. Add adversarial and edge-case tests.
6. Compare candidate prompt with the current version.
7. Review quality, latency, safety and cost.
8. Roll out gradually and monitor.

## Important rules
- Prompt text is not an authorization mechanism.
- Never put API keys or secrets in prompts.
- Treat retrieved documents and user-provided text as untrusted input.
- Validate structured output server-side.
- Record prompt version, not necessarily the full sensitive prompt content.
- Avoid changing prompt, model and retrieval strategy simultaneously unless the experiment is designed to isolate the effect.
