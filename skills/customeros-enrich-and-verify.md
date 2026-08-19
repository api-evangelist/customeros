---
name: customeros-enrich-and-verify
description: Enrich a person or organization from CustomerOS and verify an email address before you send to it, including the asynchronous person-enrichment and bulk-verification paths.
api: openapi/customeros-enrich-openapi.yml, openapi/customeros-verify-openapi.yml
operations:
  - GET /enrich/v1/organization
  - GET /enrich/v1/person
  - GET /enrich/v1/person/results/{id}
  - GET /verify/v1/email
  - POST /verify/v1/email/bulk
  - GET /verify/v1/email/bulk/results/{requestId}
  - GET /verify/v1/email/bulk/results/{requestId}/download
  - GET /verify/v1/ip
generated: '2026-08-13'
method: generated
source: openapi/customeros-enrich-openapi.yml, openapi/customeros-verify-openapi.yml
---

# Enrich and verify with CustomerOS

CustomerOS exposes enrichment and email verification as two small, key-authenticated REST
surfaces. No operation in the published spec declares an `operationId`, so every step below
addresses the operation by **method + path** — that is the only stable identifier the contract
carries.

## Before you start

**Check the host resolves.** As of 2026-08-13 the published server host `api.customeros.ai` has
no DNS address record. Resolve it before assuming a failure is your fault:

```
dig +short api.customeros.ai
```

An empty result means the API is unreachable at the address CustomerOS publishes, and no
credential will change that.

## Authentication

Every operation requires the tenant API key in a header:

```
X-CUSTOMER-OS-API-KEY: <your key>
```

There is no self-serve key issuance. Access to each endpoint group is granted per request by the
CustomerOS team. A missing or wrong key returns `401` with the standard envelope.

## Step 1 — Enrich an organization

`GET /enrich/v1/organization`

Pass **either** `domain` or `linkedinUrl` as a query parameter. The response is
`restenrich.EnrichOrganizationResponse`, which carries industry and location sub-objects.

Synchronous: a `200` means the data is in the body.

## Step 2 — Enrich a person

`GET /enrich/v1/person`

Query parameters: `linkedinUrl`, or `email`, or `firstName` + `lastName`. Set
`includeMobileNumber=true` only if you need it — treat a returned mobile number as personal data
under the CustomerOS DPA.

**This one can be asynchronous.** The operation declares `202` as well as `200`. On `202` you do
not have data yet; you have an id.

## Step 3 — Collect an asynchronous person result

`GET /enrich/v1/person/results/{id}`

Poll with the id from the `202`. `404` here means "result not found", not "person not found".
Back off between polls — no polling interval is published, and no rate-limit headers are returned,
so choose a conservative one (start at 2s, double to a 30s ceiling).

## Step 4 — Verify one email address

`GET /verify/v1/email?address=<email>`

Optional `verifyCatchAll=true` asks CustomerOS to probe catch-all domains, which is slower.
Verify **before** adding an address to an outbound sequence — see
`customeros-build-outbound-flow`.

## Step 5 — Verify a list

1. `POST /verify/v1/email/bulk` — upload the addresses. You get a `requestId`.
2. `GET /verify/v1/email/bulk/results/{requestId}` — poll for results as JSON.
3. `GET /verify/v1/email/bulk/results/{requestId}/download` — pull the same results as `text/csv`.

Use the download path for anything list-shaped; the JSON path is for status checks.

## Step 6 — IP intelligence (optional)

`GET /verify/v1/ip?address=<ip>` returns the IP intelligence record CustomerOS uses to attribute
anonymous website traffic to a company.

## Rules that apply to every step

- **No idempotency key exists.** Nothing in this API accepts one. `POST /verify/v1/email/bulk` is
  the only write here, and a retry after a timeout will submit the batch twice. Track your own
  request ids client-side.
- **Errors are not RFC 9457.** You get `{status, message, requestId}` as `application/json`.
  There is no machine-readable error code — only the HTTP status is reliable. See
  `errors/customeros-problem-types.yml`.
- **Quote `requestId`.** Every response, success or error, carries it. It is the only support
  correlation handle, and it is a body field, not a header.
- **Retry only `5xx`.** `400`, `401`, `404` are terminal. No `429` is declared anywhere in the
  spec and no rate limits are published, so use exponential backoff with jitter and stop on `4xx`.
