# APOLLO Insurance (apollo-insurance)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
