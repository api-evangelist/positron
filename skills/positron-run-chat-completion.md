---
name: Run a chat completion on Positron
description: Pick an available model on a Positron Olivaw endpoint and generate a chat completion, with or without streaming, handling rate limiting and capacity errors correctly.
api: openapi/positron-inference-openapi.yml
operations: [listModels, getModel, createChatCompletion]
generated: '2026-08-02'
method: generated
source: openapi/positron-inference-openapi.yml, conventions/positron-conventions.yml, errors/positron-problem-types.yml
---

# Run a chat completion on Positron

Positron's Olivaw inference endpoint is OpenAI API-compatible. If you already have OpenAI client
code, point its `base_url` at the Positron endpoint and supply a Positron key — the request and
response shapes below are the same ones the OpenAI SDKs expect.

## Before you start

- **Base URL.** The endpoint is deployment-scoped. The published OpenAPI declares
  `{host}/api/v1`, defaulting to `http://localhost:4000` for an on-premises Atlas appliance; the
  user guide documents hosted endpoints in the form `https://<groupname>-olivaw.fly.dev`.
  Positron's public API host `api.positron.ai` answers 401 on every path — you need a key.
- **Auth.** Send the API key in the `authorization` request header (securityScheme `apiKey`,
  `in: header`, `name: authorization`). Applied globally — every operation requires it.
- **Do not hardcode a model id.** Models vary per appliance; the Atlas v1.1 image ships
  Llama-3.1-8B-instruct-gptq, Llama-3.1-70B-instruct-gptq and Mixtral 8x7B-instruct-gptq, but
  only the 8B model runs on first boot until an operator activates the others.

## Steps

1. **`listModels`** — `GET /models`. Returns `{"object": "list", "data": [Model, ...]}` where each
   `Model` is `{id, object: "model", created, owned_by}`. There is no pagination; the full list
   comes back in one response. Choose an `id` from `data`.
2. **`getModel`** *(optional)* — `GET /models/{model}`. Confirms a specific model id is loaded.
   Returns `404` with the `Error` body if it is not.
3. **`createChatCompletion`** — `POST /chat/completions`. Body is `ChatCompletionRequest` merged
   with `SelectionSettings` (`allOf`):
   - Required: `model` (from step 1) and `messages` — an array of `ChatMessage`
     `{role, content}` where `role` is the `ChatRole` enum.
   - Optional tuning from `SelectionSettings`: `max_tokens`, `temperature` (0–2, default 1),
     `top_p` (0–1), `top_k`, `n`, `stop` (up to 4 sequences), `presence_penalty`,
     `frequency_penalty`, `logprobs`, `seed`, `ignore_eos`, `stream`.
   - **Do not** rely on `functions` / `function_call`: they are present in the schema but the
     published document states the feature is not currently supported.
4. **Read the response.** `ChatCompletion` is `{id, object: "chat.completion", created, model,
   choices[], usage}`. Take `choices[0]`; `usage` (`CompletionUsage`) is your token accounting.

## Streaming

Set `stream: true` and accept `text/event-stream`. The 200 response is then a stream of
`ChatCompletionChunkText` items carrying `ChatCompletionDelta` payloads — accumulate `delta`
content until the finish reason (`ChatFinishReason`) arrives. Keep a read timeout longer than
your `max_tokens` budget; context has primarily been tested to 2048 tokens (prompt + response).

## Error handling

Errors are **not** RFC 9457. Every documented failure returns
`{"object": "error", "type": "client" | "internal error", "message": "..."}`.

- `404` (from `getModel`) — the model is not loaded on this endpoint. Re-run `listModels`.
- `429` — rate limited. No `Retry-After` or `RateLimit-*` headers are published; back off
  exponentially with jitter.
- `503` — the fleet is over capacity. Retry with backoff; an operator can check node health with
  `listServiceNodes` on the admin API.
- There is **no idempotency key**. Completions are not deduplicated server-side, so only retry on
  `429`/`503`, never on an ambiguous timeout you cannot verify.

## Related

- `conventions/positron-conventions.yml` — auth, streaming, versioning, error envelope
- `errors/positron-problem-types.yml` — full error catalog
- `skills/positron-manage-models-and-nodes.md` — the operator-side counterpart
