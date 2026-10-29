# Case Study: AI Document Search

## Goal
Allow authorized users to ask questions over a document collection and receive answers with traceable sources.

## Architecture
- Upload/API service
- Object storage for source files
- Ingestion worker and queue
- Text extraction/chunking
- Embedding provider adapter
- Vector/hybrid search
- Metadata and access-control store
- AI gateway
- Evaluation and telemetry

## Critical design decisions
- Which file types are allowed?
- What are upload and extraction size limits?
- How is malware scanning handled?
- How are document permissions represented in metadata?
- How are deleted or replaced documents re-indexed?
- What is the freshness requirement?
- How will answer citations be verified?

## Key risk
Retrieval must enforce access control before content is passed to the model. A correct answer generated from unauthorized context is still a security failure.
