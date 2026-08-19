---
name: customeros-build-outbound-flow
description: Build a CustomerOS outbound flow end to end — create the flow, add a sequence and its steps, attach senders, set the sending schedule and opt-out config, enrol contacts, then enable it and read the stats.
api: openapi/customeros-flow-api-openapi.yml
operations:
  - POST /flows
  - GET /flows
  - GET /flows/{flow_id}
  - PATCH /flows/{flow_id}
  - POST /flows/{flow_id}/sequences
  - POST /flows/{flow_id}/sequences/{sequence_id}/steps
  - POST /flows/{flow_id}/senders
  - PUT /flows/{flow_id}/schedule
  - PUT /flows/{flow_id}/config
  - POST /flows/{flow_id}/sequences/{sequence_id}/contacts
  - POST /flows/{flow_id}/sequences/{sequence_id}/enable
  - GET /flows/{flow_id}/enable
  - GET /flows/{flow_id}/stats
  - GET /flows/{flow_id}/sequences/{sequence_id}/stats
generated: '2026-08-13'
method: generated
source: openapi/customeros-flow-api-openapi.yml
---

# Build a CustomerOS outbound flow

The Flow API is the largest published CustomerOS surface — 34 operations over `/flows` and its
nested `sequences`, `steps`, `senders`, `contacts`, `schedule` and `config` resources. It has no
`operationId`s, so steps address operations by **method + path**.

Server is templated: `https://api.customeros.ai/flow/{version}`, `version` defaults to `v1`.

## Before you start

Resolve `api.customeros.ai` — as of 2026-08-13 it has no DNS address record. Send
`X-CUSTOMER-OS-API-KEY` on every call.

**Order matters.** Create the container before its children, and enable last. Enabling a flow
before its senders, schedule and opt-out config exist will send unconfigured email.

## Step 1 — Create the flow

`POST /flows` with `FlowCreate` — `name` and `status` are required, `status` is `active` or
`draft`.

**Create it as `draft`.** That is the whole point of the two-state model: build the flow while it
cannot send.

Keep the returned `id`; it is the `{flow_id}` in every step below.

## Step 2 — Add a sequence

`POST /flows/{flow_id}/sequences` with `SequenceCreate` — `name` required, plus optional
`description`, `personas[]`, and `status` (`enabled` / `disabled`).

`personas[]` is how a sequence is aimed at a buying-committee role. It is a free array of
strings; there is no enumerated persona vocabulary in the spec.

## Step 3 — Add steps to the sequence

`POST /flows/{flow_id}/sequences/{sequence_id}/steps` with `StepCreate`. Required: `type`,
`order`, `details`, `waitTime`.

`type` selects which `details` shape you must send — the spec models this as `oneOf`:

| `type` | `details` schema | Fields |
|---|---|---|
| `email` | `EmailStepDetails` | `subject`, `body` |
| `linkedin` | `LinkedInStepDetails` | `actionType` (`connection request` \| `message`), `message`, `linkedinUrl` |
| `manual` | `ManualStepDetails` | `title`, `body` |

`waitTime` is `{duration, unit}` where unit is `minutes`, `hours` or `days` — the delay *before*
this step runs. `order` is an integer you assign; the API does not renumber for you, so keep your
own sequence counter.

Repeat for each step.

## Step 4 — Attach senders

`POST /flows/{flow_id}/senders` with `SenderCreate` — `name` and `email` required. Optional and
worth setting: `replyTo`, `bcc`, `dailySendLimit`, `warmingStatus` (`build` | `maintain`) and
`emailSignature`.

`warmingStatus: build` is for a mailbox that is still warming; `maintain` is for an established
one. If you provisioned the mailbox through the Mailstack API, see
`customeros-manage-mailstack-domains`.

## Step 5 — Set the schedule

`PUT /flows/{flow_id}/schedule` with `ScheduleUpdate`. The schedule object controls:

- `activeDays[]` — monday…sunday
- `activeTimeWindow` — `{start, end}` as times
- `pauseOnHolidays` (boolean)
- `respectRecipientTimezone` (boolean)
- `rules.minutesDelayBetweenEmails`
- `limits.emailsPerMailboxPerHour` and `limits.emailsPerMailboxPerDay`

Those `limits` are **your sending throttle**, not the CustomerOS API rate limit. CustomerOS
publishes no API rate limits at all.

## Step 6 — Set the config

`PUT /flows/{flow_id}/config` with `ConfigUpdate`:

- `optOut.enabled` and `optOut.text` — set these. An outbound email sequence without an opt-out is
  a compliance problem, and the API defaults nothing.
- `analytics.trackEmailOpens`
- `analytics.trackLinkClicks.{enabled, useCustomDomain, customDomain}`

If you enable link tracking with a custom domain, that domain has to be one you control — the
same reverse-proxy-on-your-own-domain pattern the website tracker uses.

## Step 7 — Enrol contacts

`POST /flows/{flow_id}/sequences/{sequence_id}/contacts` with `ContactCreate` — `email` required,
plus `firstName`, `lastName`, `company`, and `status` (`active` | `paused`).

**Verify addresses first** with `GET /verify/v1/email` — see `customeros-enrich-and-verify`.
Sending to unverified addresses is the fastest way to damage the sender reputation you configured
in step 4.

Enrolled contacts report `status` (`active` | `paused` | `completed` | `unsubscribed`) and
`currentStep`.

## Step 8 — Enable, in the right order

1. `POST /flows/{flow_id}/sequences/{sequence_id}/enable` — enable the sequence.
2. `GET /flows/{flow_id}/enable` — enable the flow.

Note the asymmetry, it is real and it will trip you: **sequence** enable/disable are `POST`,
**flow** enable/disable are `GET`. A `GET` that mutates state is unusual; do not let a caching
layer or a link prefetcher touch `/flows/{flow_id}/enable` or `/disable`.

To stop: `GET /flows/{flow_id}/disable`, or `PATCH /flows/{flow_id}` with
`status: draft`.

## Step 9 — Read the results

- `GET /flows/{flow_id}/stats`
- `GET /flows/{flow_id}/sequences/{sequence_id}/stats`

Both return a free-form `object` in the published spec — no properties are declared, so treat the
shape as unstable and do not hard-code field names.

## Rules that apply to every step

- **No idempotency key.** Every `POST` here creates. A retried step creation adds a second step at
  the same `order`. Keep a client-side ledger keyed on your own request id.
- **Pagination is declared but not usable.** List responses carry
  `{totalCount, page, perPage, totalPages}`, and no list operation declares a page or cursor
  *query parameter*. Expect the first page only.
- **Errors:** the Flow spec declares no `4xx` responses at all — not even `401`. Treat any non-2xx
  as opaque, read `message` and `requestId` from the body if present, and retry only `5xx`.
- **Deletes are hard deletes.** `DELETE` on a flow, sequence, step, schedule or config returns
  `204` and the spec documents no undo.
