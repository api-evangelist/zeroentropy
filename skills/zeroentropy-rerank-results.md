---
name: zeroentropy-rerank-results
description: Improve any search pipeline's relevance by reranking candidate documents with ZeroEntropy's zerank model.
generated: '2026-07-21'
method: generated
api: ZeroEntropy API
source: openapi/zeroentropy-openapi.json
operations:
- rerank_models_rerank_post
- embed_models_embed_post
---

# Rerank Results with ZeroEntropy

Bolt ZeroEntropy's models onto an existing retriever without moving your index.

## Auth
Send `Authorization: Bearer <your-api-key>`. Base URL `https://api.zeroentropy.dev/v1`.

## Steps
1. **Retrieve candidates** with your existing search/vector store to get a shortlist of documents for a query.
2. **Rerank** — `POST /models/rerank` (`rerank_models_rerank_post`) with the `query` and the candidate `documents`. The response scores/orders documents by relevance; take the top of the returned order.
3. **(Optional) Embed** — `POST /models/embed` (`embed_models_embed_post`) to generate `zembed` vectors when you want ZeroEntropy embeddings driving the first-stage retrieval too.

## Notes
- Stateless: rerank and embed do not require creating a collection.
- Errors are FastAPI JSON with a `detail` field; 422 returns per-field `detail[]`. See `errors/zeroentropy-problem-types.yml`.
