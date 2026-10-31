# Positron

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Positron AI is a US-based generative-AI hardware company founded in 2023 and headquartered in Reno, Nevada, building purpose-built Transformer inference accelerators as an alternative to GPU-based inference infrastructure. Its shipping product, Atlas, is a rack inference appliance built on eight in-house Archer accelerators (256 GB HBM) and dual AMD EPYC Genoa processors, with the next-generation Asimov silicon and Titan system slated for 2027. Positron exposes its inference fleet through "Olivaw", a serving and administration layer that publishes two documented HTTP APIs: an OpenAI-compatible completions API (models, chat completions, text completions, with server-sent-event streaming) so existing OpenAI client code can be repointed at a Positron endpoint, and an administrative API for managing models, service nodes, users, and access tokens on an appliance or hosted cluster. The company raised a $230M Series B in February 2026 at a valuation above $1B from ARENA, Jump Trading, Unless, the Qatar Investment Authority, Arm, Helena, DFJ Growth, Atreides, Valor, Resilience Reserve, Flume Ventures and 1517 Fund.

**Areas:** Artificial Intelligence · Inference · inference-hardware · AI Accelerators · LLM · Transformers · OpenAI-Compatible · Machine Learning · Semiconductors · Data Center · llm-serving · Model Hosting

## Positron on APIs.io

Everything profiled for Positron is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/positron/](https://apis.io/providers/positron/)** — or go straight to one of the APIs or properties below.

### APIs (5)

- [Positron Access Tokens API](https://apis.io/apis/positron/positron-access-tokens-api/) — The access_tokens API from Positron — 3 operation(s) for access_tokens.
- [Positron Completion API](https://apis.io/apis/positron/positron-completion-api/) — The completion API from Positron — 2 operation(s) for completion.
- [Positron Models API](https://apis.io/apis/positron/positron-models-api/) — The models API from Positron — 5 operation(s) for models.
- [Positron Service Nodes API](https://apis.io/apis/positron/positron-service-nodes-api/) — The service_nodes API from Positron — 2 operation(s) for service_nodes.
- [Positron Users API](https://apis.io/apis/positron/positron-users-api/) — The users API from Positron — 3 operation(s) for users.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [positron-mcp.yml](https://apis.io/servers/positron/positron-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Positron Agentic Access](https://apis.io/agentic-access/positron/positron-agentic-access/)

#### Collections (7)

Postman and Open Collection request collections.

- [Olivaw Admin Access Tokens API](https://apis.io/collections/positron/open-positron-access-tokens-api/)
- [Olivaw Admin API](https://apis.io/collections/positron/open-positron-admin/)
- [Olivaw OpenAI Completion API](https://apis.io/collections/positron/open-positron-completion-api/)
- [Olivaw OpenAI API](https://apis.io/collections/positron/open-positron-inference/)
- [Positron Models API](https://apis.io/collections/positron/open-positron-models-api/)
- [Olivaw Admin Service Nodes API](https://apis.io/collections/positron/open-positron-service-nodes-api/)
- [Olivaw Admin Users API](https://apis.io/collections/positron/open-positron-users-api/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Positron Admin Overlay](https://apis.io/overlays/positron/positron-admin-overlay/)
- [Positron Inference Overlay](https://apis.io/overlays/positron/positron-inference-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Positron Authentication](https://apis.io/security/positron/positron-authentication/)
- [Positron Domain Security](https://apis.io/security/positron/positron-domain-security/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.positron.ai/)
- [Documentation](https://support.positron.ai/api-documentation)
- [Getting started](https://support.positron.ai/user-guide)
- [API reference](https://support.positron.ai/api-documentation)
- [Support](https://www.positron.ai/contact-sales)
- [Changelog](https://support.positron.ai/release-notes)
- [GitHub](https://github.com/positron-ai)

## API Evangelist rating

**Kin Score 32.7** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 79.5 |
| Contract quality | 44.8 |
| Contract governance | 4.5 |
| Operational transparency | 18.4 |
| Developer ergonomics | 56.5 |
| Access clarity | 0.0 |

**Agent readiness 23.9** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 15.5** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/positron/](https://apis.io/providers/positron/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Positron: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/positron/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
