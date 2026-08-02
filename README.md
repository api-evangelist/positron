# Positron

Positron AI builds purpose-built Transformer inference hardware — the Atlas appliance (8x in-house
Archer accelerators, 256 GB HBM, dual AMD EPYC Genoa), with Asimov silicon and the Titan system
slated for 2027. Founded 2023, headquartered in Reno, Nevada; $230M Series B (February 2026) at a
valuation above $1B.

Positron exposes its inference fleet through **Olivaw**, a serving and administration layer that
publishes two documented HTTP APIs:

- **Olivaw OpenAI-Compatible Inference API** — `/models`, `/models/{model}`, `/chat/completions`,
  `/completions`, with server-sent-event streaming. Because it mirrors the OpenAI surface, an
  OpenAI client library works by repointing `base_url`. Documented at
  <https://support.positron.ai/api-documentation>.
- **Olivaw Admin API** — the control plane over the model catalogue, service nodes (Giskard, vLLM
  or OpenAI backends), platform users and access tokens. Published as OpenAPI 3.1.0 in
  <https://github.com/positron-ai/admin-api-docs>.

## Links

- Website — <https://www.positron.ai/>
- Developer portal — <https://support.positron.ai/>
- User guide — <https://support.positron.ai/user-guide>
- Release notes — <https://support.positron.ai/release-notes>
- GitHub — <https://github.com/positron-ai>
- Secondary-market listing — <https://forgeglobal.com/positron_stock/>

## What is in this repository

`apis.yml` is the APIs.json index. Artifacts: `openapi/` (both harvested specs, plus `_original/`),
`overlays/`, `authentication/`, `conventions/`, `errors/`, `data-model/`, `lifecycle/`,
`changelog/`, `conformance/`, `packages/`, `well-known/`, `security/`, `agentic-access/`,
`skills/`, `mcp/`, `llms/`.

Recorded absences (probed 2026-08-02, not gaps in the research): no first-party SDK or CLI, no MCP
server, no A2A agent card, no webhooks/AsyncAPI, no `/.well-known/` documents, no `security.txt`,
no status page, no trust center, no public pricing, terms or privacy pages, and no OAuth/OIDC —
authentication is static API keys only.
