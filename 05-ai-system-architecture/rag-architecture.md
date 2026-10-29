# Retrieval-Augmented Generation (RAG)

RAG retrieves relevant source material and supplies it as context to a model. It can improve grounding in private or changing information, but does not guarantee correctness.

## Ingestion flow

```text
Upload / Source Connector
        |
File type + size + malware checks
        |
Text extraction / OCR if needed
        |
Normalization and chunking
        |
Embedding generation
        |
Vector + metadata storage
```

## Query flow

```text
User Question
     |
Authentication + authorization
     |
Query normalization / optional rewrite
     |
Retrieve authorized chunks
     |
Optional reranking
     |
Build bounded context with source identifiers
     |
LLM response
     |
Validate / attach citations / return
```

## Key design choices
- Chunk size and overlap based on document type and evaluation.
- Embedding model and vector dimensions.
- Metadata filters for tenant, document, permissions and freshness.
- Hybrid keyword + vector retrieval where useful.
- Reranking only if it improves quality enough to justify latency/cost.
- Context window budget and source attribution.
- Re-indexing and deletion workflows.
- Evaluation set containing normal, ambiguous and adversarial questions.

## Security
- Apply document-level authorization before context reaches the model.
- Treat retrieved content as untrusted; it can contain prompt injection.
- Do not let retrieved instructions override application policy.
- Prevent cross-tenant retrieval leakage.
- Make deletion propagate to source files, chunks, vectors, caches and derived indexes.
- Restrict document ingestion by file size/type and scan uploaded files.

## Evaluation
Measure retrieval recall/precision where labels exist, answer groundedness, citation correctness, refusal behavior, latency and cost. Human review is important for high-impact use cases.
