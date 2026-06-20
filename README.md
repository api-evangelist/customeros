# CustomerOS (customeros)

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
