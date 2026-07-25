# APOLLO Insurance (apollo-insurance)

APOLLO Insurance (APOLLO Insurance Agency Ltd., apollocover.com) is a Vancouver-founded Canadian digital insurance brokerage and MGA-style distribution platform that sells personal and small-commercial coverage entirely online — tenant and student tenant insurance in every province, homeowner, condo and townhouse, landlord and pet insurance on the personal side, and general liability, professional liability and directors and officers coverage on the business side. APOLLO does not underwrite; it distributes on a commission basis on behalf of A+ to A- rated Canadian carriers, and it sits in the thin digital-broker layer of a Big-Few Canadian market dominated by Intact, Definity, Co-operators and Desjardins. Its distinctive business is embedded tenant insurance for REITs and property managers: automated resident enrolment at lease signing, renewal handling, and real-time building-level compliance tracking, delivered through a Yardi Systems integration and its CoverTrack compliance product.

Unusually for the Canadian insurance sector, APOLLO publishes a genuine, publicly readable developer portal at [docs.apollocover.com](https://docs.apollocover.com/) — a Stoplight workspace with three public projects and downloadable OpenAPI definitions covering quote and application (pre-fill) for tenant insurance and compliance-status lookup for partner properties. The surface is real but partner-scoped: every call needs an `affiliateId` (a co-branded APOLLO subdomain) and an `x-api-key` token that APOLLO issues by hand to affiliates and property-manager partners, so there is no self-serve credential path and no consumer-facing API. Canada has no open-insurance mandate — OSFI supervises prudentially, the provinces (FSRA, AMF) supervise market conduct, and Consumer-Driven Banking excludes insurance entirely — so nothing forces this disclosure; APOLLO published it as a distribution strategy. No ACORD, AL3, IVANS or agency-management-system reference appears anywhere in its public site or documentation.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/apollo-insurance/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/apollo-insurance/refs/heads/main/apis.yml)

## Tags

- Insurance
- Canada
- Insurtech
- Broker
- Embedded Insurance
- Property and Casualty
- Tenant Insurance
- Quoting
- Distribution
- Compliance

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## APIs

### APOLLO Affiliates API

The current APOLLO Affiliate API. Two partner-scoped POST operations — quote an application and create an application — scoped by `affiliateId` (the partner's co-branded APOLLO subdomain) and `insuranceType` (currently only `tenant`). Creating an application returns a `quoteLink` into the affiliate's co-branded APOLLO launchpad with the customer's responses pre-filled. Authenticated with an `x-api-key` header token issued by an APOLLO contact; separate tokens for the test and production servers, plus a Stoplight mock server for prototyping.

- **Human URL:** [https://docs.apollocover.com/docs/public-affiliate-api/a8a7ea17b0889-affiliates-api](https://docs.apollocover.com/docs/public-affiliate-api/a8a7ea17b0889-affiliates-api)
- **Base URL:** `https://fpl95knwc1.execute-api.ca-central-1.amazonaws.com/1_0_0`

#### Tags

- Insurance
- Quoting
- Embedded Insurance
- Tenant Insurance
- Affiliate

#### Properties

- [Documentation](https://docs.apollocover.com/docs/public-affiliate-api/27500feeac1b7-introduction)
- [API Reference](https://docs.apollocover.com/docs/public-affiliate-api/a8a7ea17b0889-affiliates-api)
- [OpenAPI](openapi/apollo-insurance-affiliates.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### APOLLO Public API - Affiliates

The earlier APOLLO public affiliate surface, still published in its own Stoplight project. Two POST operations fixed to the tenant line — generate a quote (returning contents, ALE, liability and add-on premium components with a policy expiry date) and create an application. Same AWS ca-central-1 test and production hosts as the current Affiliates API; the project also carries a Webhooks page, which is present but empty.

- **Human URL:** [https://docs.apollocover.com/docs/affiliate-api/18a87d4863056-public-api-affiliates](https://docs.apollocover.com/docs/affiliate-api/18a87d4863056-public-api-affiliates)
- **Base URL:** `https://fpl95knwc1.execute-api.ca-central-1.amazonaws.com/1_0_0`

#### Tags

- Insurance
- Quoting
- Tenant Insurance
- Affiliate

#### Properties

- [Documentation](https://docs.apollocover.com/docs/affiliate-api/18a87d4863056-public-api-affiliates)
- [API Reference](https://docs.apollocover.com/docs/affiliate-api/18a87d4863056-public-api-affiliates)
- [OpenAPI](openapi/apollo-insurance-affiliates-legacy.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### APOLLO CoverTrack API

CoverTrack is APOLLO's tenant-insurance compliance product for REITs and property managers, served from its own `api.covertrack.ca` host. Three real operations plus one documented callback — read a single tenant's compliance status (`ACTIVE`, `PENDING`, `NOT_SUBMITTED` or `DECLINED`, with optional policy detail including the third-party carrier's policy number and provider), read compliance status for every tenant of a property, and generate a tenant insurance quote for a partner. The fourth path is an example specification of a partner destination callback that APOLLO POSTs when a relevant policy event occurs — the only event-driven surface APOLLO documents.

- **Human URL:** [https://docs.apollocover.com/docs/covertrack-api/fu18p9wlkzenb-cover-track-api-s](https://docs.apollocover.com/docs/covertrack-api/fu18p9wlkzenb-cover-track-api-s)
- **Base URL:** `https://api.covertrack.ca`

#### Tags

- Insurance
- Compliance
- Tenant Insurance
- Property Management
- Quoting

#### Properties

- [Documentation](https://docs.apollocover.com/docs/covertrack-api/fu18p9wlkzenb-cover-track-api-s)
- [API Reference](https://docs.apollocover.com/docs/covertrack-api/fu18p9wlkzenb-cover-track-api-s)
- [OpenAPI](openapi/apollo-insurance-covertrack.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [Website](https://apollocover.com/)
- [Developer Portal](https://docs.apollocover.com/)
- [Documentation](https://docs.apollocover.com/docs/public-affiliate-api/27500feeac1b7-introduction)
- [Partners](https://apollocover.com/partnerships)
- [Support Center](https://help.apollocover.com/)
- [Customer Portal](https://policy-portal.apollocover.com/)
- [Blog](https://apollocover.com/magazine)
- [Privacy Policy](https://apollocover.com/privacy-policy)

## API Posture

- **Developer portal:** `https://docs.apollocover.com/` — HTTP 200, Stoplight-hosted, publicly readable, no login wall.
- **OpenAPI harvested:** 3 definitions, verbatim, from Stoplight's own export URLs. See `review.yml` for full provenance.
- **ACORD posture:** No ACORD reference found. ACORD, AL3, ACORD XML, NGDS, IVANS, agency download, Applied Epic and Vertafore AMS360 all return zero matches across the public site, the docs portal and all three definitions. The only named third-party integration is Yardi Systems, a property-management platform.
- **Insurance verbs:** QUOTE yes; BIND partial (creates a pre-filled application and hands off to a hosted web funnel — it does not bind machine-to-machine); ISSUE no; FNOL/claims no.
- **Auth:** static `x-api-key` header token, provisioned manually by an APOLLO contact, separate keys per environment. No OAuth2, no OIDC discovery, no mTLS, no scopes.
- **Webhooks:** no AsyncAPI and no event catalog — only an example partner-destination policy-event callback specified inside the CoverTrack definition, and an empty "Webhooks" documentation page.
- **Lines exposed:** tenant (renter) only. None of APOLLO's homeowner, condo, landlord, pet, general liability, professional liability or D&O products have an API.
- **Home market:** Canada — no open-insurance mandate; OSFI prudential, provincial market conduct (FSRA, AMF); Consumer-Driven Banking excludes insurance.

## Maintainers

- Kin Lane — kin@apievangelist.com
