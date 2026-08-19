---
name: customeros-manage-mailstack-domains
description: Register a sending domain with CustomerOS Mailstack, configure its DNS, create mailboxes on it, and hand those mailboxes to an outbound flow as senders.
api: openapi/customeros-domains-openapi.yml
operations:
  - GET /domains
  - POST /domains
  - POST /domains/configure
  - GET /domains/{domain}/mailboxes
  - POST /domains/{domain}/mailboxes
generated: '2026-08-13'
method: generated
source: openapi/customeros-domains-openapi.yml
---

# Manage Mailstack domains and mailboxes

Mailstack is the cold-email infrastructure surface: CustomerOS registers a sending domain for you,
configures its DNS, and provisions mailboxes on it. Five operations, no `operationId`s — address
them by **method + path**.

Note this surface is **unversioned**: paths are `/domains`, not `/domains/v1`. Every other
CustomerOS REST surface carries a version segment. There is no published policy explaining the
difference, so pin nothing to the path shape.

## Before you start

Resolve `api.customeros.ai` — as of 2026-08-13 it has no DNS address record. Send
`X-CUSTOMER-OS-API-KEY` on every call.

## Step 1 — See what you already have

`GET /domains` lists active domains as `restmailstack.DomainsResponse`. Each
`restmailstack.DomainRecord` carries `domain`, `createdDate`, `expiredDate` and `nameservers`.

Check `expiredDate` before doing anything else — an expired sending domain fails silently at the
mail layer, not at the API layer.

## Step 2 — Register a domain

`POST /domains`

Two failure modes matter, and they are distinct:

- **`409 Conflict`** — the domain is already registered. Not an error for you; go to step 3.
- **`406 Not Acceptable`** — the TLD is not supported, or the domain is premium. Terminal. Pick a
  different domain; retrying will not help.

## Step 3 — Configure DNS

`POST /domains/configure` with `restmailstack.ConfigureDomainRequest`.

This is the step that sets up the records a cold-email domain needs. `500` here is documented as
"Configuration failed or service unavailable" — the one place in this API where a `500` is
plausibly transient and worth retrying with backoff.

Do not create mailboxes before this succeeds.

## Step 4 — Create mailboxes

`POST /domains/{domain}/mailboxes` returns a `restmailstack.MailboxRecord`:

```
email, forwardingEnabled, forwardingTo, webmailEnabled, password
```

**Handle `password` carefully.** The mailbox record includes the mailbox credential. Any client
that logs responses verbatim, echoes them into a trace, or forwards them to an LLM context will
leak a working mailbox password. Redact this field at your HTTP layer before anything else sees
the response.

`409` means the mailbox already exists on that domain.

## Step 5 — List mailboxes

`GET /domains/{domain}/mailboxes` returns `restmailstack.MailboxesResponse`. `404` means the
domain is not found *or* not owned by your tenant — the spec collapses both into one status.

## Step 6 — Hand the mailboxes to a flow

Use each mailbox address as a sender:

`POST /flows/{flow_id}/senders` with `{name, email, dailySendLimit, warmingStatus}`.

Set `warmingStatus: build` on a freshly provisioned mailbox and give it a low `dailySendLimit`.
See `customeros-build-outbound-flow`.

## Rules that apply to every step

- **No idempotency key.** Domain registration and mailbox creation are both `POST` with no key.
  `409` is your only duplicate protection.
- **No pagination** on either list operation.
- **Errors:** `{status, message, requestId}` as `application/json`; no machine-readable codes.
- **Retry `5xx` only.** `400`, `401`, `404`, `406`, `409` are terminal. No `429` is declared and
  no rate limits are published.
