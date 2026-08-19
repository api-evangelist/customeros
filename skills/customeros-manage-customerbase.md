---
name: customeros-manage-customerbase
description: Create organizations and contacts in CustomerBASE, link them to a CRM record, and import contacts in bulk from JSON or CSV — including the partial-success cases the bulk endpoints return.
api: openapi/customeros-customerbase-openapi.yml, openapi/customeros-billing-openapi.yml
operations:
  - POST /customerbase/v1/organizations
  - GET /customerbase/v1/organizations/{id}
  - PUT /customerbase/v1/organizations/{id}/links/{externalSystem}/primary
  - POST /customerbase/v1/contacts
  - POST /customerbase/v1/contacts/bulk
  - POST /customerbase/v1/contacts/import
  - GET /billing/v1/organizations/{id}/invoices
generated: '2026-08-13'
method: generated
source: openapi/customeros-customerbase-openapi.yml, openapi/customeros-billing-openapi.yml
---

# Manage CustomerBASE organizations and contacts

CustomerBASE is the record-of-truth surface: organizations, the contacts attached to them, and
the links back to the CRM the organization came from. No operation declares an `operationId`, so
steps address operations by **method + path**.

## Before you start

Resolve `api.customeros.ai` first — as of 2026-08-13 it has no DNS address record. Authenticate
with `X-CUSTOMER-OS-API-KEY` on every call.

## Step 1 — Create an organization

`POST /customerbase/v1/organizations`

Body is `customerbase.CreateOrganizationRequest`. The returned
`customerbase.OrganizationRecord` carries three identifiers — `id`, `cosId` and your own
`customId` — plus `icpFit`, `stage`, `relationship` and `leadSource`.

**`409 Conflict` is expected and useful.** It means an organization already exists with the
identifiers you supplied. Because this API has no idempotency key, `409` is the only duplicate
suppression you get: treat it as "already created", not as a failure, and follow with step 2 to
fetch the existing record.

## Step 2 — Read an organization

`GET /customerbase/v1/organizations/{id}`

`404` means no organization with that id in your tenant.

## Step 3 — Link it to your CRM

`PUT /customerbase/v1/organizations/{id}/links/{externalSystem}/primary`

Marks one external-system record as primary for this organization. `externalSystem` is the path
segment naming the system (the CRM integrations CustomerOS documents are HubSpot, Salesforce and
Pipedrive). `404` covers both "organization not found" and "external system not found" — the
message string is the only way to tell them apart.

Do this after step 1 whenever the organization originated in a CRM, so subsequent syncs update
rather than duplicate.

## Step 4 — Add contacts

Three shapes, pick by volume:

| Operation | Use when | Watch for |
|---|---|---|
| `POST /customerbase/v1/contacts` | one contact | `201` |
| `POST /customerbase/v1/contacts/bulk` | many contacts as JSON | `206` / `207` |
| `POST /customerbase/v1/contacts/import` | a CSV upload | `415`, `206` / `207` |

A `customerbase.ContactRecord` is thin — `contactId`, `email`, `linkedinUrl`. Enrich it through
`customeros-enrich-and-verify` rather than expecting CustomerBASE to fill it in.

### Handle partial success — this is the trap

The bulk and import operations declare **`206 Partial Content`** and **`207 Multi-Status`**
alongside `201`. Both are 2xx. A client that branches on `response.ok` will record a partially
failed import as a complete one.

Always inspect the body:

- `customerbase.BulkResponse` / `customerbase.BulkResponseMultipleErrors` carry the outcome.
- `customerbase.BulkSummary` gives the counts.
- `customerbase.BulkErrorDetails` names the rows that failed.

Reconcile the summary counts against what you sent before reporting success.

### CSV import specifics

`POST /customerbase/v1/contacts/import` accepts `multipart/form-data` (or a JSON body with a
base64 `file`). A wrong content type returns `415`, and a malformed file returns `400` with
"Invalid file format or data".

Note: this operation's published spec declares its security requirement as `ApiKeyAutl` — a typo
for `ApiKeyAuth` referencing an undefined scheme. Send the normal `X-CUSTOMER-OS-API-KEY` header
anyway; strict spec-driven clients may need the scheme name patched locally. Recorded in
`overlays/customeros-customerbase-overlay.yaml`.

## Step 5 — Read invoices for an organization

`GET /billing/v1/organizations/{id}/invoices`

Returns `billing.InvoicesResponse`. Each `billing.InvoiceRecord` has `amount`, `currency`,
`dueDate`, `invoiceStatus`, `number`, `paymentLink` and `publicUrl`. Also declares `206`, so
apply the partial-success rule here too.

`paymentLink` and `publicUrl` are unauthenticated URLs — do not log or forward them.

## Rules that apply to every step

- **No idempotency key.** Retrying any `POST` here can duplicate. Use `409` and your own
  client-side request ledger.
- **No pagination.** Nothing in these specs declares a page, cursor or limit parameter.
- **Errors:** `{status, message, requestId}` as `application/json`; no error codes. Quote
  `requestId` to support.
- **Retry `5xx` only**, with exponential backoff and jitter. No `429` is declared and no rate
  limits are published.
