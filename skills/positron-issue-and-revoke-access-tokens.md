---
name: Issue and revoke Positron access tokens
description: Create a platform user and mint, audit and revoke the access tokens that authenticate calls to the Positron Olivaw inference API.
api: openapi/positron-admin-openapi.yml
operations: [listUsers, getUser, createUser, updateUser, deleteUser, listAccessTokens, getAccessToken, createAccessToken, deleteAccessToken]
generated: '2026-08-02'
method: generated
source: openapi/positron-admin-openapi.yml, authentication/positron-authentication.yml, conventions/positron-conventions.yml
---

# Issue and revoke Positron access tokens

Access tokens minted through the Olivaw Admin API are the credentials presented in the
`authorization` header on every Positron inference call. This is the highest-consequence flow on
the platform: `createAccessToken` mints a working inference credential.

## Before you start

- Admin auth is a bearer API key (root-level `security: [{bearer: [API key]}]`).
- Tokens are **create / read / delete only** — the document declares no update operation, so
  rotation is mint-then-revoke, in that order, with a short overlap.

## Steps

1. **`listUsers`** — `GET /users`. Full list, no pagination. Confirm whether the principal already
   exists before creating one.
2. **`createUser`** — `POST /users/new` with a `User` body. `201` on success, `400` on invalid
   payload. Not idempotent — re-list rather than retry blindly.
3. **`createAccessToken`** — `POST /accessTokens/new` with an `AccessToken` body. `201` returns
   the created token. Capture the secret at this moment; there is no documented re-read of a
   secret value (`getAccessToken` returns the token *object*).
4. **Distribute the key** to the calling application as the `authorization` header value for the
   inference API. Test with `listModels` on the inference document — a working key returns the
   model list rather than a 401.
5. **`listAccessTokens`** — `GET /accessTokens` to audit outstanding credentials.
   `getAccessToken` (`GET /accessTokens/{token}`) inspects one; `404` means it does not exist.
6. **`deleteAccessToken`** — `DELETE /accessTokens/{token}` revokes. Do this only after the
   replacement key is confirmed working. (Note: the published document's `404` description on this
   operation reads "The user was not found." — an apparent copy/paste in the source spec.)
7. **`deleteUser`** — `DELETE /users/{user}` when decommissioning a principal entirely.

## Guardrails

- Treat `createAccessToken` and `deleteAccessToken` as privileged, human-approved operations. The
  recommended agentic execution contracts are in
  `agentic-access/positron-agentic-access.yml`.
- No idempotency key exists — a retried `POST /accessTokens/new` mints a *second* live credential.
  Always `listAccessTokens` before retrying.
- No `401`/`403` responses are documented on the admin API; do not depend on a structured body for
  auth failures.

## Related

- `authentication/positron-authentication.yml`
- `skills/positron-manage-models-and-nodes.md`
- `errors/positron-problem-types.yml`
