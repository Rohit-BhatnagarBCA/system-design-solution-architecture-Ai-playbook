# Node.js Module Boundaries

## Purpose

Module boundaries keep business capabilities understandable and reduce accidental coupling.

## Example public interface

An `orders` module may expose:
- `createOrder(command)`
- `getOrderForUser(orderId, userId)`
- `cancelOrder(command)`

It should not expose its internal SQL query helpers or database model to every other module.

## Dependency direction

Prefer:

`Routes/Controllers -> Application Services -> Domain Rules -> Interfaces`

Infrastructure implementations (database, queue, external providers) are injected or called through stable interfaces where practical.

## Rules to document
- Which module owns each entity and table?
- Which module can call which public interface?
- Which events may be published?
- What data may cross a module boundary?
- Which dependencies are forbidden?
- Who reviews changes to shared contracts?

## Warning signs
- Circular imports
- Controllers with complex business logic
- One generic service importing every domain
- Multiple modules updating the same entity without ownership rules
- Shared utilities becoming a dumping ground
