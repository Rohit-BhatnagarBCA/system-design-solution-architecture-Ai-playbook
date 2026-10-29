# Case Study: High-Traffic Commerce Application

## Core domains
- Identity and customer profiles
- Catalogue and search
- Cart
- Orders
- Inventory
- Payment integration
- Notifications
- Analytics

## Starting architecture
A modular monolith may be appropriate if team size and release requirements are modest. Keep domain boundaries explicit. Use a queue for suitable asynchronous work such as notifications.

## Data integrity
- Store prices in minor units with currency.
- Treat payment provider callbacks as untrusted until signature and state checks pass.
- Use idempotency for order/payment operations.
- Model inventory reservation and order state transitions explicitly.
- Keep audit history for important state changes.

## Scaling path
Measure catalogue reads, search load, checkout writes and inventory contention separately. Cache suitable catalogue data; do not blindly cache stock or payment state. Extract services only when domain ownership or workload evidence justifies it.

## AI feature example
An AI shopping assistant may search catalogue data, but availability, price, eligibility and checkout actions must be verified by trusted backend services at execution time.
