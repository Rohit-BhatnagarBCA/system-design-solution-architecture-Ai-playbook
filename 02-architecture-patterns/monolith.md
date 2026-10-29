# Monolith

A monolith is deployed as one application unit. It can still have well-organized internal modules.

## Example

```text
Client
  |
Load Balancer
  |
Node.js Application
  |-- Authentication
  |-- Catalogue
  |-- Orders
  |-- AI module
  |
Database / Cache / External APIs
```

## Benefits
- Simple deployment and debugging
- In-process calls are straightforward
- Easier local development and integration tests
- Lower platform and networking overhead

## Risks
- Poor boundaries can produce a tightly coupled codebase
- A deployment affects the entire application
- Different workloads may compete for the same resources
- Scaling one expensive capability may require scaling the whole application

## Good practices
- Keep modules separated by business capability.
- Use service/repository boundaries where they provide value.
- Keep configuration and secrets outside source code.
- Add health checks, structured logs, metrics and tests.
- Avoid importing another module's private internals.

## Evolution path

A monolith can be refactored into a modular monolith without changing deployment. Extract services only when a concrete requirement warrants the operational cost.
