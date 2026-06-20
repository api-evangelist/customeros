# CustomerOS GraphQL Schema

Representative GraphQL schema for the [CustomerOS](https://customeros.ai/) (formerly Openline)
open-source revenue / go-to-market platform. CustomerOS exposes its core developer API as a
single GraphQL endpoint served by the open-source `customer-os-api` server.

- Open-source repository: <https://github.com/openline-ai/openline-customer-os>
- Cloud documentation: <https://docs.customeros.ai>
- GitHub organizations: <https://github.com/customeros> · <https://github.com/openline-ai>

> **Representative schema.** The accompanying [`customeros-schema.graphql`](./customeros-schema.graphql)
> is a representative, trimmed schema distilled from the open-source `customer-os-api`
> schema files (`packages/server/customer-os-api/graphql/schemas/*.graphqls`). It captures
> the real operation names, types, enums, and field shapes for the organization, contact,
> opportunity, and interaction domains, but it is not the complete generated schema (the
> full server schema spans 60+ `.graphqls` files). Type names, query/mutation names, and
> enum values mirror the upstream source as of the review date.

---

## Overview

The `customer-os-api` server is a Go service built on [gqlgen](https://gqlgen.com/). It serves
a single GraphQL endpoint and an optional playground:

| Path | Method | Purpose |
|------|--------|---------|
| `/query` | `POST` | GraphQL operations (queries and mutations) |
| `/playground` | `GET` | GraphQL Playground UI (when enabled) |

Requests are authenticated per tenant with an API key supplied in a request header, and most
fields are protected by `@hasRole(roles: [ADMIN, USER])` and `@hasTenant` directives in the
upstream schema. The self-hosted base path depends on deployment; the CustomerOS cloud serves
it under `https://api.customeros.ai`.

There is no documented public GraphQL **subscription** surface — the schema defines only
`Query` and `Mutation` root types.

---

## Schema file

See [`customeros-schema.graphql`](./customeros-schema.graphql) for the representative schema.

---

## Custom scalars

| Scalar | Purpose |
|--------|---------|
| `Time` | ISO-8601 timestamps |
| `Int64` | 64-bit integers (counts, likelihood rates) |
| `Any` | Arbitrary value (custom field values) |

---

## Core domains

### Organizations
- `Organization` — company / account record; firmographics, domains, locations, social media,
  contracts, opportunities, owner, tags, stage, qualification status, and a timeline of events.
- Queries: `organization`, `organizations`, `organization_ByCustomerOsId`,
  `organization_ByLinkedIn`, `organization_CheckWebsite`.
- Mutations: `organization_Save`, `organization_Merge`, `organization_AddSubsidiary`,
  `organization_AddDomain`, `organization_AddSocial`, `organization_Hide`, `organization_Show`.

### Contacts
- `Contact` — individual person; name, prefix, job roles, emails, phone numbers, social
  profiles, tags, and associated organizations.
- Queries: `contact`, `contacts`, `contact_ByEmail`, `contact_ByLinkedIn`, `contact_ByPhone`.
- Mutations: `contact_Create`, `contact_CreateForOrganization`, `contact_Update`,
  `contact_Merge`, `contact_CreateBulkByEmailV2`, `contact_CreateBulkByLinkedInV2`.

### Opportunities
- `Opportunity` — sales / renewal opportunity linked to an organization; amount, currency,
  internal/external stage, likelihood, and renewal forecast fields.
- Queries: `opportunity`, `opportunities_LinkedToOrganizations`.
- Mutations: `opportunity_Save`, `opportunity_Archive`, `opportunityRenewalUpdate`,
  `opportunityRenewal_UpdateAllForOrganization`.

### Interactions & timeline
- `InteractionEvent` / `InteractionSession` — emails, calls, and other channel events, with
  union participant types (`EmailParticipant`, `ContactParticipant`, `UserParticipant`, etc).
- `Meeting`, `Note`, `LogEntry`, `Issue` — additional timeline event types.
- `Organization.timelineEvents` returns the merged `TimelineEvent` union for an organization.
- Query: `interactionEvent`.

---

## Query examples

### Fetch an organization with opportunities

```graphql
query {
  organization(id: "org-123") {
    metadata { id created lastUpdated source }
    name
    website
    domains
    stage
    opportunities {
      metadata { id }
      name
      amount
      internalStage
      renewalLikelihood
    }
  }
}
```

### List contacts (paginated)

```graphql
query {
  contacts(pagination: { page: 0, limit: 50 }, sort: [{ by: "LAST_NAME", direction: ASC }]) {
    totalElements
    content {
      metadata { id }
      name
      prefix
      primaryEmail { email }
    }
  }
}
```

### Look up a contact by email

```graphql
query {
  contact_ByEmail(email: "buyer@example.com") {
    metadata { id }
    name
    jobRoles { jobTitle }
  }
}
```

---

## Mutation examples

### Save (create or update) an organization

```graphql
mutation {
  organization_Save(input: { name: "Acme Inc", website: "https://acme.com" }) {
    metadata { id }
    name
    website
  }
}
```

### Create a contact for an organization

```graphql
mutation {
  contact_CreateForOrganization(
    organizationId: "org-123"
    input: { name: "Dana Buyer", prefix: "Ms" }
  ) {
    metadata { id }
    name
  }
}
```

### Save an opportunity

```graphql
mutation {
  opportunity_Save(input: {
    opportunityId: null
    name: "Acme Expansion"
    amount: 50000
    internalType: UPSELL
  }) {
    metadata { id }
    name
    amount
    internalStage
  }
}
```
