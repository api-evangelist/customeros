# CustomerOS (customeros)

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

CustomerOS (formerly Openline) is an open-source go-to-market / revenue platform for B2B SaaS. Its core open-source application server, customer-os-api, exposes a single GraphQL endpoint (POST /query) covering organizations, contacts, opportunities, contracts, invoices, interactions, and timeline events. The commercial cloud (customeros.ai) adds a documented REST "Customerbase" API and a JavaScript website visitor tracker, with broader access granted on a per-request basis.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/customeros/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/customeros/refs/heads/main/apis.yml)

## Tags

- CRM
- Revenue
- Go-To-Market
- GraphQL
- Open Source

## Timestamps

- **Created:** 2026-06-20
- **Modified:** 2026-06-20

## APIs

### CustomerOS GraphQL Core API

Single-endpoint GraphQL API (POST /query) served by the open-source customer-os-api server. Exposes Query and Mutation operations across organizations, contacts, opportunities, contracts, invoices, interactions, and timeline events, authenticated per tenant with an API key. A GraphQL playground is exposed at /playground when enabled.

- **Human URL:** [https://github.com/openline-ai/openline-customer-os](https://github.com/openline-ai/openline-customer-os)
- **Base URL:** `https://api.customeros.ai/query`

#### Tags

- GraphQL
- Organizations
- Contacts
- Opportunities

#### Properties

- [Documentation](https://docs.customeros.ai)
- [GitHub](https://github.com/openline-ai/openline-customer-os)
- [GraphQL](graphql/customeros-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [OpenAPI](openapi/customeros-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/customeros.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/customeros.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CustomerOS Organizations API

GraphQL queries and mutations for company / organization records - organization, organizations, organization_Save, organization_Merge, subsidiaries, domains, social media, and onboarding status - over the customer-os-api /query endpoint.

- **Human URL:** [https://docs.customeros.ai/data-structure](https://docs.customeros.ai/data-structure)
- **Base URL:** `https://api.customeros.ai/query`

#### Tags

- GraphQL
- Organizations
- Companies

#### Properties

- [Documentation](https://docs.customeros.ai/data-structure)
- [GraphQL](graphql/customeros-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [OpenAPI](openapi/customeros-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/customeros.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/customeros.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CustomerOS Contacts API

GraphQL queries and mutations for contacts (people) - contact, contacts, contact_ByEmail, contact_ByLinkedIn, contact_Create, contact_CreateForOrganization, job roles, emails, phone numbers, and social profiles - over the customer-os-api /query endpoint.

- **Human URL:** [https://docs.customeros.ai/contacts](https://docs.customeros.ai/contacts)
- **Base URL:** `https://api.customeros.ai/query`

#### Tags

- GraphQL
- Contacts
- People

#### Properties

- [Documentation](https://docs.customeros.ai/contacts)
- [GraphQL](graphql/customeros-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [OpenAPI](openapi/customeros-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/customeros.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/customeros.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CustomerOS Opportunities API

GraphQL queries and mutations for sales opportunities and renewals - opportunity, opportunities_LinkedToOrganizations, opportunity_Save, opportunity_Archive, and renewal likelihood / forecast updates - over the customer-os-api /query endpoint.

- **Human URL:** [https://github.com/openline-ai/openline-customer-os](https://github.com/openline-ai/openline-customer-os)
- **Base URL:** `https://api.customeros.ai/query`

#### Tags

- GraphQL
- Opportunities
- Pipeline

#### Properties

- [GitHub](https://github.com/openline-ai/openline-customer-os)
- [GraphQL](graphql/customeros-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [OpenAPI](openapi/customeros-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/customeros.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/customeros.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CustomerOS Interactions API

GraphQL queries and mutations for interaction events, interaction sessions, meetings, notes, log entries, issues, and the per-organization timeline of touchpoints - over the customer-os-api /query endpoint.

- **Human URL:** [https://github.com/openline-ai/openline-customer-os](https://github.com/openline-ai/openline-customer-os)
- **Base URL:** `https://api.customeros.ai/query`

#### Tags

- GraphQL
- Interactions
- Timeline

#### Properties

- [GitHub](https://github.com/openline-ai/openline-customer-os)
- [GraphQL](graphql/customeros-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [OpenAPI](openapi/customeros-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/customeros.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/customeros.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### CustomerOS Customerbase REST API

Documented synchronous REST API on the customeros.ai cloud (api.customeros.ai/customerbase/v1), authenticated with the X-CUSTOMER-OS-API-KEY header. Includes organization endpoints such as POST /organizations. Access to each endpoint group is granted on a per-request basis by the CustomerOS team.

- **Human URL:** [https://docs.customeros.ai/api-overview](https://docs.customeros.ai/api-overview)
- **Base URL:** `https://api.customeros.ai/customerbase/v1`

#### Tags

- REST
- Customerbase
- Organizations

#### Properties

- [Documentation](https://docs.customeros.ai/api-overview)
- [API Reference](https://docs.customeros.ai/api-descriptions)

### CustomerOS Website Tracker

Client-side JavaScript tracker, installed via a script tag behind a customer-hosted reverse-proxy CNAME, that captures page views and custom events and matches visitor IPs to companies. It is a script integration rather than a public REST/GraphQL endpoint; custom events are emitted from the browser.

- **Human URL:** [https://docs.customeros.ai/website-tracker](https://docs.customeros.ai/website-tracker)
- **Base URL:** `https://docs.customeros.ai/tracker`

#### Tags

- Tracking
- Visitor Identification
- JavaScript

#### Properties

- [Documentation](https://docs.customeros.ai/website-tracker)
- [Documentation](https://docs.customeros.ai/tracker/custom-events)

## Common Properties

- [GitHub Organization](https://github.com/openline-ai)
- [GitHub Organization](https://github.com/customeros)
- [LinkedIn](https://www.linkedin.com/company/customeros)
- [Website](https://customeros.ai)
- [Documentation](https://docs.customeros.ai)
- [Plans](plans/customeros-plans-pricing.yml)
- [Rate Limits](rate-limits/customeros-rate-limits.yml)
- [Fin Ops](finops/customeros-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
