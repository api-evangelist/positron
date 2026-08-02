---
name: Manage Positron models and service nodes
description: Register a service node with the Olivaw admin layer, add or update a model on it, and verify the model is servable through the inference API.
api: openapi/positron-admin-openapi.yml
operations: [listServiceNodes, getServiceNode, createServiceNode, updateServiceNode, deleteServiceNode, listModels, getModel, createModel, updateModel, deleteModel]
generated: '2026-08-02'
method: generated
source: openapi/positron-admin-openapi.yml, https://support.positron.ai/user-guide, conventions/positron-conventions.yml
---

# Manage Positron models and service nodes

The Olivaw Admin API is the control plane behind a Positron Atlas appliance or hosted cluster. It
owns the model catalogue the inference API reads, plus the service nodes that actually serve those
models. This is a privileged surface — treat every write as audited.

## Before you start

- **Auth.** The published document declares a root-level `security` requirement of
  `bearer: [API key]`. It defines no `components.securitySchemes`, so confirm the exact header
  form with your deployment; send the admin key as a bearer credential.
- **No servers[].** The admin API is served per deployment (appliance front panel / hosted
  Olivaw instance). The GUI equivalent authenticates operators via a Google account through Auth0.
- **Service node backends.** A node is a Giskard node, a vLLM instance, or an OpenAI-compatible
  implementation. Olivaw health-checks nodes periodically; the GUI Node Health panel is the same
  data as `listServiceNodes`.

## Steps

1. **`listServiceNodes`** — `GET /serviceNodes`. Returns `{"object": "list", "data": [...]}`
   with each node's id, backend type, JSON configuration, servable models and active flag. No
   pagination.
2. **`createServiceNode`** — `POST /serviceNodes/new` with a `ServiceNode` body. Returns `201`
   with the created node, or `400` (`Error` body) if the payload is invalid. **Not idempotent** —
   no client-supplied key, so a blind retry creates a second node.
3. **`getServiceNode`** — `GET /serviceNodes/{node}` to confirm registration. `404` means Olivaw
   does not know the node.
4. **`createModel`** — `POST /models/new` with a `Model` body (`id`, `object: "model"`,
   `created`, `owned_by`). `201` on success, `400` on invalid payload.
5. **`updateModel`** — `PATCH /models/{model}` to alter model metadata. `400` on an invalid
   update, `404` when the id is unknown.
6. **Verify through the inference API** — call `listModels` (inference document) and confirm the
   id appears; then `getModel`. The two documents share one model id space.
7. **`deleteServiceNode`** / **`deleteModel`** — destructive. Per the user guide, deleting a
   service node "will cause olivaw to forget about the service node". Confirm before calling; both
   return `404` if the target is already gone.

## Operator notes from the published user guide

- The Olivaw GUI exposes a **Sync Models** bulk action that queries a node for the models it can
  serve — the API equivalent is reading the node's model list via `getServiceNode` after a change.
- On an Atlas v1.1 image only Llama 3.1 8B runs on first boot; the other shipped models must be
  activated manually through the admin utility.

## Guardrails

- No idempotency contract exists on any create operation — never auto-retry a `POST /*/new`
  without first re-listing to check whether the object already exists.
- No `401`/`403` responses are documented despite the security requirement; do not assume an
  unauthenticated call fails with a structured body.
- See `agentic-access/positron-agentic-access.yml` for the recommended `x-agentic-access`
  execution contract per operation before exposing any of these to an autonomous agent.

## Related

- `skills/positron-issue-and-revoke-access-tokens.md`
- `data-model/positron-data-model.yml`
- `errors/positron-problem-types.yml`
