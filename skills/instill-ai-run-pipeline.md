---
name: instill-ai-run-pipeline
description: Find, validate and trigger an Instill Core pipeline synchronously, by stream, or asynchronously with polling of the long-running operation.
api: Instill Core API
operations:
- PipelinePublicService_ListPipelines
- PipelinePublicService_GetPipeline
- PipelinePublicService_ValidatePipeline
- PipelinePublicService_TriggerPipeline
- PipelinePublicService_TriggerPipelineWithStream
- PipelinePublicService_TriggerAsyncPipeline
- PipelinePublicService_GetOperation
- PipelinePublicService_ListPipelineRuns
generated: '2026-10-09'
method: generated
---

# Find, validate and trigger an Instill Core pipeline synchronously, by stream, or asynchronously with polling of the long-running operation.

## Steps
1. List pipelines in the namespace with `PipelinePublicService_ListPipelines` (`parent` = `namespaces/{namespace}`), and pick one with `PipelinePublicService_GetPipeline`.
2. Optionally check the recipe with `PipelinePublicService_ValidatePipeline`.
3. Trigger it:
   - short jobs: `PipelinePublicService_TriggerPipeline` (POST `/v1beta/{name}/trigger`), with the inputs in `body`;
   - incremental output: `PipelinePublicService_TriggerPipelineWithStream`;
   - long jobs: `PipelinePublicService_TriggerAsyncPipeline`, which returns an operation. Poll `PipelinePublicService_GetOperation` until `done`.
4. Inspect the history with `PipelinePublicService_ListPipelineRuns`.

## Rules
- Auth: send `Authorization: Bearer instill_sk_***` on every call (securityDefinitions.Bearer). Host: `api.instill-ai.com`.
- Resource names are hierarchical (`namespaces/{ns}/pipelines/{id}`), and many paths take the full resource `name` as a path parameter.
- The spec declares no idempotency keys. Do not blindly retry create or trigger calls; list first to avoid duplicates.
- The `Instill-Requester-Uid` header (optional) runs a request on behalf of an organization namespace.
- Reference: https://docs.instill-ai.com/reference. Docs MCP: https://docs.instill-ai.com/mcp
