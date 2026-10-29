# Architecture Pattern Comparison

## Decision summary

| Pattern | Good fit | Strengths | Costs / risks |
|---|---|---|---|
| Monolith | Small product, small team, simple deployment | Lowest operational overhead, straightforward local development | Boundaries can erode; all parts share deployment/runtime |
| Modular monolith | Growing product needing clear domain boundaries | Strong internal structure without distributed-system overhead | Requires discipline and module ownership |
| Microservices | Independent teams/releases/scaling are valuable | Independent deployment and fault isolation when well designed | Network failures, data consistency, tracing, deployment and platform complexity |
| Event-driven | Work can be asynchronous or multiple consumers react to events | Loose temporal coupling, burst smoothing | Eventual consistency, duplicate delivery, ordering and debugging complexity |
| Serverless | Event-driven or bursty workloads with suitable platform constraints | Low server management, elastic execution | Cold starts, limits, vendor coupling, cost unpredictability at some workloads |
| Hybrid | Different workloads need different execution models | Fit each component to its actual needs | More deployment patterns and operational knowledge |

## Recommended default

For many new Node.js products, start with a **modular monolith** unless requirements clearly justify another option.

Use explicit modules, contracts and dependency rules. A modular monolith can later be split by extracting a module with a stable contract and clear data ownership.

## When to consider extracting a service

Consider a separate service when evidence shows one or more of:
- A domain needs independent release cadence.
- A workload has substantially different scaling requirements.
- A team needs clear ownership and autonomous delivery.
- A failure domain must be isolated.
- A distinct security or compliance boundary is required.
- The module has stable APIs and data ownership.

Do not extract services only because the codebase is large or because microservices are fashionable.

## AI-specific decision

An AI module inside a modular monolith is often enough for an early product. Consider an independent AI service or worker pool when AI traffic, provider-specific controls, long-running workflows, GPU inference, isolation or deployment cadence justify it.

## Decision questions

1. Which business capability is changing independently?
2. What measurable pain does a new deployable service remove?
3. Who owns it and its on-call support?
4. What data does it own?
5. How will timeout, retries, versioning and authentication work?
6. What new failure modes and costs are introduced?
7. How will success be measured after migration?
