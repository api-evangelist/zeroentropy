---
name: zeroentropy-search-collection
description: Index documents into a ZeroEntropy collection and run relevance queries over them.
generated: '2026-07-21'
method: generated
api: ZeroEntropy API
source: openapi/zeroentropy-openapi.json
operations:
- add_collection_collections_add_collection_post
- add_document_documents_add_document_post
- get_document_info_list_documents_get_document_info_list_post
- top_documents_queries_top_documents_post
- top_snippets_queries_top_snippets_post
---

# Search a ZeroEntropy Collection

Build a retrieval index and query it with ZeroEntropy's pipeline.

## Auth
Send `Authorization: Bearer <your-api-key>` on every call. Base URL `https://api.zeroentropy.dev/v1` (or `https://eu-api.zeroentropy.dev/v1` for EU). All calls below are POST with a JSON body.

## Steps
1. **Create a collection** — `POST /collections/add-collection` (`add_collection_collections_add_collection_post`) with `{ "collection_name": "..." }`. A 409 means it already exists — safe to continue.
2. **Add documents** — `POST /documents/add-document` (`add_document_documents_add_document_post`) with the `collection_name`, a unique `path`, and content. A 409 means that path already exists; update it instead of re-adding.
3. **Verify indexing** — `POST /documents/get-document-info-list` (`get_document_info_list_documents_get_document_info_list_post`). Page with `limit` plus the `path_gt` keyset cursor to walk large collections.
4. **Query** — `POST /queries/top-documents` (`top_documents_queries_top_documents_post`) with `collection_name`, `query`, and `k`. Use `top_snippets_queries_top_snippets_post` when you want passage-level hits instead of whole documents.

## Errors
Errors are FastAPI JSON with a `detail` field (422 returns `detail[]` of field errors). Handle 404 (unknown collection/path) and 409 (already exists) explicitly. See `errors/zeroentropy-problem-types.yml`.
