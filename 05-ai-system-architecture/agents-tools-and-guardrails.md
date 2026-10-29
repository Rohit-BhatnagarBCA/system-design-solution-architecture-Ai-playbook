# AI Agents, Tool Calling and Guardrails

## Tool calling is a request, not permission

A model may propose a tool call. The application must independently validate and authorize it.

## Safer tool flow

```text
Model proposes tool + arguments
           |
Schema validation
           |
Authenticated user / tenant authorization
           |
Business-rule validation
           |
Approval step if consequential
           |
Execute narrow tool
           |
Audit result and return limited output to model
```

## Tool design principles
- Allowlist tools; do not expose arbitrary function execution.
- Use strict schemas and reject unexpected arguments.
- Apply per-tool timeout, rate limit and output-size limits.
- Give each tool only the permissions it needs.
- Separate read-only tools from mutating tools.
- Require explicit confirmation or human approval for consequential actions.
- Use idempotency keys for retried actions.
- Log action metadata and outcome without leaking secrets.

## Prompt injection
User text, web pages, uploaded files and retrieved documents may contain instructions intended to manipulate the model. Treat all such content as data, not trusted policy. Enforce policy in code, scope tool permissions and test adversarial cases.

## Guardrail layers
- Input validation and size limits
- Authentication, authorization and tenant isolation
- Data minimization and redaction
- Prompt construction boundaries
- Output schema validation
- Policy checks and moderation where appropriate
- Tool allowlists and approval gates
- Evaluation and monitoring
- Incident response and rollback

No single guardrail catches every failure. Use defense in depth.
