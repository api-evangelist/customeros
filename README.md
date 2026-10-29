# CustomerOS

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

CustomerOS (formerly Openline) is a London-based revenue-intelligence platform for B2B go-to-market teams. It identifies anonymous website visitors, scores them against an ideal customer profile, infers buying stage from page engagement, and attributes content and ad spend to real pipeline. The developer surface spans a first-party JavaScript website tracker installed behind a customer-owned reverse-proxy CNAME, a set of key-authenticated REST APIs published as OpenAPI in the company monorepo (CustomerBASE contacts and organizations, person and organization enrichment, email verification and IP intelligence, Mailstack sending domains and mailboxes, billing invoices, outreach tracking), a 34-operation Flow API for outbound sequencing, and the open-source customer-os-api GraphQL server that predates the pivot. CustomerOS also runs a live anonymous MCP server and serves an A2A agent card from its documentation host.

**Areas:** CRM · Revenue · Go-To-Market · Lead Intelligence · Visitor Identification · Attribution · Email Verification · Data Enrichment · GraphQL · Open Source · A2A

## CustomerOS on APIs.io

Everything profiled for CustomerOS is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/customeros/](https://apis.io/providers/customeros/)** — or go straight to one of the APIs or properties below.

### APIs (11)

- [CustomerOS Website Tracker](https://apis.io/apis/customeros/customeros-website-tracker/) — Client-side JavaScript tracker that captures page views and custom events, exposes window.cos.identify() for attaching identity and properties, and matches…
- [CustomerOS Billing API](https://apis.io/apis/customeros/customeros-billing-api-api/) — The Billing API API from CustomerOS — 1 operation(s) for billing api.
- [CustomerOS CustomerBASE API](https://apis.io/apis/customeros/customeros-customerbase-api-api/) — The CustomerBASE API API from CustomerOS — 6 operation(s) for customerbase api.
- [CustomerOS Domains API](https://apis.io/apis/customeros/customeros-domains-api/) — The Domains API from CustomerOS — 2 operation(s) for domains.
- [CustomerOS Email Verification API](https://apis.io/apis/customeros/customeros-email-verification-api/) — The Email Verification API from CustomerOS — 4 operation(s) for email verification.
- [CustomerOS Enrichment API](https://apis.io/apis/customeros/customeros-enrichment-api-api/) — The Enrichment API API from CustomerOS — 3 operation(s) for enrichment api.
- [CustomerOS Flows API](https://apis.io/apis/customeros/customeros-flows-api/) — The Flows API from CustomerOS — 18 operation(s) for flows.
- [CustomerOS IP Intelligence API](https://apis.io/apis/customeros/customeros-ip-intelligence-api/) — The IP Intelligence API from CustomerOS — 1 operation(s) for ip intelligence.
- [CustomerOS Mailboxes API](https://apis.io/apis/customeros/customeros-mailboxes-api/) — The Mailboxes API from CustomerOS — 1 operation(s) for mailboxes.
- [CustomerOS Outreach API](https://apis.io/apis/customeros/customeros-outreach-api/) — The Outreach API from CustomerOS — 1 operation(s) for outreach.
- [CustomerOS Graph QL API](https://apis.io/apis/customeros/customeros-graph-ql-api/) — Single GraphQL endpoint for all CustomerOS operations.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### GraphQL (1)

GraphQL schemas.

- [CustomerOS GraphQL Schema](https://apis.io/graphqls/customeros/customeros-graphql/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [customer_os_docs](https://apis.io/servers/customeros/customer-os-docs/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Customeros Agentic Access](https://apis.io/agentic-access/customeros/customeros-agentic-access/)

#### Collections (9)

Postman and Open Collection request collections.

- [CustomerOS GraphQL API](https://apis.io/collections/customeros/open-customeros/)
- [CustomerOS API](https://apis.io/collections/customeros/open-customeros-billing/)
- [CustomerOS API](https://apis.io/collections/customeros/open-customeros-customerbase/)
- [CustomerOS API](https://apis.io/collections/customeros/open-customeros-domains/)
- [CustomerOS API](https://apis.io/collections/customeros/open-customeros-enrich/)
- [CustomerOS API](https://apis.io/collections/customeros/open-customeros-flow-api/)
- [CustomerOS GraphQL API](https://apis.io/collections/customeros/open-customeros-graphql-api/)
- [CustomerOS API](https://apis.io/collections/customeros/open-customeros-outreach/)
- [CustomerOS API](https://apis.io/collections/customeros/open-customeros-verify/)

#### Overlays (8)

OpenAPI overlays, including conversational phrasing for each operation.

- [Customeros Billing Overlay](https://apis.io/overlays/customeros/customeros-billing-overlay/)
- [Customeros Customerbase Overlay](https://apis.io/overlays/customeros/customeros-customerbase-overlay/)
- [Customeros Domains Overlay](https://apis.io/overlays/customeros/customeros-domains-overlay/)
- [Customeros Enrich Overlay](https://apis.io/overlays/customeros/customeros-enrich-overlay/)
- [Customeros Flow Api Overlay](https://apis.io/overlays/customeros/customeros-flow-api-overlay/)
- [Customeros Graphql Api Overlay](https://apis.io/overlays/customeros/customeros-graphql-api-overlay/)
- [Customeros Outreach Overlay](https://apis.io/overlays/customeros/customeros-outreach-overlay/)
- [Customeros Verify Overlay](https://apis.io/overlays/customeros/customeros-verify-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Customeros Authentication](https://apis.io/security/customeros/customeros-authentication/)
- [Customeros Domain Security](https://apis.io/security/customeros/customeros-domain-security/)
- [Customeros Trust Center](https://apis.io/security/customeros/customeros-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Customeros Plans Pricing](https://apis.io/plans/customeros/customeros-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Customeros Rate Limits](https://apis.io/rate-limits/customeros/customeros-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Customeros Finops](https://apis.io/finops/customeros/customeros-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://customeros.ai)
- [Documentation](https://docs.customeros.ai)
- [Getting started](https://docs.customeros.ai/quickstart)
- [Pricing](https://customeros.ai/pricing)
- [Changelog](https://customeros.ai/updates)
- [Blog](https://customeros.ai/gtm-guides)
- [Compliance](https://docs.customeros.ai/security-and-compliance)
- [Terms of service](https://customeros.ai/standard-agreement/tos)
- [Privacy policy](https://customeros.ai/policies/privacy-policy)
- [GitHub](https://github.com/customeros)
- [Status](https://status.customeros.ai/)

## API Evangelist rating

**Kin Score 53.4** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 50.6 |
| Contract governance | 4.5 |
| Operational transparency | 26.3 |
| Developer ergonomics | 42.3 |
| Access clarity | 75.0 |

**Agent readiness 32.6** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
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
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 29.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/customeros/](https://apis.io/providers/customeros/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for CustomerOS: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/customeros/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
