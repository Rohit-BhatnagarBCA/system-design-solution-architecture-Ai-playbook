# API Design

## Practical guidelines
- Use resource-oriented paths and consistent HTTP methods.
- Version public APIs when compatibility requires it.
- Validate body, query, path parameters and content types.
- Use authentication and object-level authorization.
- Return consistent error codes and safe messages.
- Paginate collections; avoid unbounded list endpoints.
- Define filtering, sorting and field-selection rules.
- Document schemas and examples with OpenAPI where useful.

## Example

`POST /api/v1/conversations/{conversationId}/messages`

Request body:
```json
{
  "message": "Summarize the uploaded document."
}
```

The server must verify that the authenticated user can access the conversation. Never trust a `userId` supplied in the body to decide ownership.

## AI endpoint considerations
- Apply per-user and per-tenant quotas.
- Limit input size and conversation context.
- Use request idempotency when duplicate submissions could cause cost or side effects.
- Consider streaming for interactive responses and asynchronous jobs for long-running work.
- Record a safe usage event, not necessarily the full raw prompt.
- Define what happens when the model provider times out.
