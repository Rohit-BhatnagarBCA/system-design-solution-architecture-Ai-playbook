# Security and Reliability Checklist

## Identity and access
- Authentication is enforced on protected endpoints.
- Authorization checks the requested resource, not just the user's login state.
- Tenant boundaries are enforced in application queries and retrieval.
- Privileged actions require least privilege and appropriate audit logs.
- Secrets are stored in a secret manager or protected runtime configuration.

## API security
- Validate all inputs and content types.
- Limit request body size, upload size, pagination and execution time.
- Apply per-user and per-IP rate limits where appropriate.
- Use secure headers, TLS and appropriate CORS policy.
- Avoid leaking stack traces or sensitive internal details.
- Keep dependencies patched and scan them.

## AI-specific security
- Treat user input and retrieved documents as untrusted.
- Never use prompts as a substitute for authorization.
- Restrict tool capabilities and validate every argument.
- Redact sensitive data where possible.
- Prevent cross-user and cross-tenant retrieval.
- Apply provider data-handling policies before sending data externally.
- Define retention and deletion for prompts, outputs, embeddings and logs.
- Test prompt injection, data exfiltration and unauthorized tool calls.

## Reliability
- Define timeouts for every network dependency.
- Use bounded retries and idempotency.
- Monitor queue depth and dead-letter messages.
- Have health/readiness checks and graceful shutdown.
- Test backups and restore procedures.
- Define incident ownership and runbooks.
- Practice dependency outage and replica-failure scenarios.

## Privacy by design
Collect only data needed for the feature. Document purpose, access, retention, deletion, export and audit requirements. In regulated or high-impact domains, involve security, privacy and legal specialists early.
