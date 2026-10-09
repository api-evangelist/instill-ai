---
name: instill-ai-manage-api-tokens
description: Create, list, validate and revoke Instill Core API tokens for the authenticated user.
api: Instill Core API
operations:
- MgmtPublicService_GetAuthenticatedUser
- MgmtPublicService_CreateToken
- MgmtPublicService_ListTokens
- MgmtPublicService_GetToken
- MgmtPublicService_ValidateToken
- MgmtPublicService_DeleteToken
generated: '2026-10-09'
method: generated
---

# Create, list, validate and revoke Instill Core API tokens for the authenticated user.

## Steps
1. Confirm the identity with `MgmtPublicService_GetAuthenticatedUser`.
2. Mint a key with `MgmtPublicService_CreateToken` (POST `/v1beta/tokens`). Store it securely, because it is a secret.
3. Audit the keys with `MgmtPublicService_ListTokens` and `MgmtPublicService_GetToken`.
4. Check that a key works with `MgmtPublicService_ValidateToken`.
5. Revoke a key with `MgmtPublicService_DeleteToken`.

## Rules
- Auth: send `Authorization: Bearer instill_sk_***` on every call (securityDefinitions.Bearer). Host: `api.instill-ai.com`.
- Resource names are hierarchical (`namespaces/{ns}/pipelines/{id}`), and many paths take the full resource `name` as a path parameter.
- The spec declares no idempotency keys. Do not blindly retry create or trigger calls; list first to avoid duplicates.
- The `Instill-Requester-Uid` header (optional) runs a request on behalf of an organization namespace.
- Reference: https://docs.instill-ai.com/reference. Docs MCP: https://docs.instill-ai.com/mcp
