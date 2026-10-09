---
name: instill-ai-knowledge-base-rag
description: Create a knowledge base in Instill Artifact, upload files, wait for processing, and run semantic chunk search for RAG.
api: Instill Core API
operations:
- ArtifactPublicService_CreateKnowledgeBase
- ArtifactPublicService_ListKnowledgeBases
- ArtifactPublicService_CreateFile
- ArtifactPublicService_GetFile
- ArtifactPublicService_ListFiles
- ArtifactPublicService_ReprocessFile
- ArtifactPublicService_ListChunks
- ArtifactPublicService_SearchChunks
generated: '2026-10-09'
method: generated
---

# Create a knowledge base in Instill Artifact, upload files, wait for processing, and run semantic chunk search for RAG.

## Steps
1. Create a knowledge base with `ArtifactPublicService_CreateKnowledgeBase` (`parent` = the namespace), or reuse one from `ArtifactPublicService_ListKnowledgeBases`.
2. Add documents with `ArtifactPublicService_CreateFile` (POST `/v1alpha/{parent}/files`).
3. Check the processing status with `ArtifactPublicService_GetFile` or `ArtifactPublicService_ListFiles`. Retry a failed file with `ArtifactPublicService_ReprocessFile`.
4. Inspect the chunks with `ArtifactPublicService_ListChunks`.
5. Retrieve context with `ArtifactPublicService_SearchChunks` (POST `/v1alpha/{parent}/search-chunks`), then pass the results to a model or pipeline.

## Rules
- Auth: send `Authorization: Bearer instill_sk_***` on every call (securityDefinitions.Bearer). Host: `api.instill-ai.com`.
- Resource names are hierarchical (`namespaces/{ns}/pipelines/{id}`), and many paths take the full resource `name` as a path parameter.
- The spec declares no idempotency keys. Do not blindly retry create or trigger calls; list first to avoid duplicates.
- The `Instill-Requester-Uid` header (optional) runs a request on behalf of an organization namespace.
- Reference: https://docs.instill-ai.com/reference. Docs MCP: https://docs.instill-ai.com/mcp
