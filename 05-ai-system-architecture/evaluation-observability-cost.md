# AI Evaluation, Observability and Cost

## Evaluation
Build a versioned dataset of representative tasks before launch. Include:
- Common cases
- Edge cases
- Ambiguous questions
- Incorrect or missing source data
- Prompt-injection attempts
- Unauthorized-resource requests
- Long inputs and output-format failures

Use task-specific scoring. Automated evaluators can help but may be biased or inconsistent; calibrate them against human review.

Track:
- Task success / rubric score
- Groundedness and citation correctness for RAG
- Structured-output validity
- Refusal correctness
- Tool-call success and authorization failures
- Latency and cost per successful task

## Observability
Useful metrics:
- Request count and success/error rate
- Provider/model latency and timeouts
- Time to first token and total response time
- Input/output tokens
- Estimated cost by model, feature, tenant and environment
- Retry/fallback rate
- Queue depth and oldest job age
- Evaluation score and user feedback

Avoid logging raw sensitive prompts by default. Use redaction, access controls and retention policies.

## Cost model

For each model:
`Estimated cost = input token units × input price + output token units × output price`

Use the provider's current pricing units and rates; verify prices before budgeting. Include retries, failed requests, embeddings, reranking, storage, observability and worker compute.

## Cost controls
- Select a model appropriate to the task.
- Bound input and output token counts.
- Avoid repeatedly sending unnecessary conversation history.
- Cache only when safe and semantically appropriate.
- Apply quotas and alerts.
- Use asynchronous processing for suitable non-interactive jobs.
- Measure cost per successful task, not only cost per request.
- Review model changes against quality and safety thresholds.
