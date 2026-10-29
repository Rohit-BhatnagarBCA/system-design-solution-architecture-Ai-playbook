# Reference Architecture: Node.js RAG Platform

## Ingestion pipeline

```text
Upload / Connector
    -> Authentication + file limits + malware scanning
    -> Text extraction / OCR
    -> Normalize and chunk
    -> Generate embeddings
    -> Store vectors + metadata + document state
```

## Query pipeline

```text
Question
  -> Authenticate and authorize
  -> Retrieve only permitted chunks
  -> Optional hybrid search / reranking
  -> Build bounded context
  -> AI gateway / model
  -> Validate response and source references
  -> Return answer with citations where supported
```

## Components
- API service for upload/query and access control
- Worker pool for ingestion and embedding
- Queue for backpressure and retries
- Object storage for source documents
- Relational database for metadata, permissions and job state
- Vector index for embeddings
- Model provider adapter
- Evaluation dataset and telemetry

## Critical concerns
- Tenant/document access filters must apply during retrieval.
- File type, size and content must be validated.
- Retrieved text is untrusted and may contain prompt injection.
- Re-indexing and deletion must cover vectors, chunks, caches and derived data.
- Measure retrieval quality and answer groundedness.
- Use a queue with bounded concurrency to respect provider quotas.
