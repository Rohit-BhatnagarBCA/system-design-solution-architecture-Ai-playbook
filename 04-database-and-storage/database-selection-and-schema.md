# Database Selection and Schema Design

## Choose by access patterns and requirements

| Need | Common option to evaluate | Questions |
|---|---|---|
| Relational business data and transactions | PostgreSQL / another relational DB | Constraints, joins, consistency, operational expertise? |
| Flexible document data | Document database | Are access patterns document-centric? How are consistency and schema evolution handled? |
| Fast ephemeral data, cache, quotas | Redis or equivalent | Eviction, persistence, availability and cost? |
| Search over text | Search engine or database search | Ranking, filtering, language and freshness requirements? |
| Semantic retrieval | Vector capability in a database or vector database | Scale, filtering, hybrid search, access control and operational cost? |
| Files and large objects | Object storage | Upload limits, signed URLs, retention, encryption and lifecycle? |

Avoid selecting a database based only on popularity.

## Example relational schema

A simplified commerce-like example:

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email TEXT NOT NULL UNIQUE,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE products (
  id UUID PRIMARY KEY,
  sku TEXT NOT NULL UNIQUE,
  name TEXT NOT NULL,
  description TEXT,
  price_minor_units BIGINT NOT NULL CHECK (price_minor_units >= 0),
  currency CHAR(3) NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE orders (
  id UUID PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES users(id),
  status TEXT NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE order_items (
  id UUID PRIMARY KEY,
  order_id UUID NOT NULL REFERENCES orders(id),
  product_id UUID NOT NULL REFERENCES products(id),
  quantity INTEGER NOT NULL CHECK (quantity > 0),
  unit_price_minor_units BIGINT NOT NULL CHECK (unit_price_minor_units >= 0)
);

CREATE INDEX orders_user_created_idx ON orders(user_id, created_at DESC);
CREATE INDEX order_items_order_idx ON order_items(order_id);
```

Prices are stored in minor currency units to avoid floating-point money calculations. Production schemas need domain-specific constraints, migrations, audit rules and retention decisions.

## AI data model considerations

Depending on the product, separate:
- Conversation metadata
- Messages and role/type
- Model/provider/version metadata
- Prompt/template version
- Token usage and cost estimate
- Feedback and evaluation results
- Document metadata and ingestion state
- Embeddings or vector references
- Tool execution audit records

Do not store every raw prompt forever by default. Define purpose, consent, access control, retention, deletion and sensitive-data handling.

## Scaling path

1. Start with a correctly indexed schema and measured query plans.
2. Tune slow queries and connection pooling.
3. Add caching only for measured hot reads and define invalidation.
4. Add read replicas if read workload and consistency requirements fit.
5. Partition large tables when evidence justifies it.
6. Consider sharding only after simpler options are insufficient and routing/operations are understood.
