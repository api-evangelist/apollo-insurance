# APOLLO Insurance

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

APOLLO Insurance (APOLLO Insurance Agency Ltd., apollocover.com) is a Vancouver-founded Canadian digital insurance brokerage and MGA-style distribution platform that sells personal and small-commercial coverage entirely online — tenant and student tenant insurance in every province, homeowner, condo and townhouse, landlord and pet insurance on the personal side, and general liability, professional liability and directors and officers coverage on the business side. APOLLO does not underwrite; it distributes on a commission basis on behalf of A+ to A- rated Canadian carriers, and it sits in the thin digital-broker layer of a Big-Few Canadian market dominated by Intact, Definity, Co-operators and Desjardins. Its distinctive business is embedded tenant insurance for REITs and property managers: automated resident enrolment at lease signing, renewal handling, and real-time building-level compliance tracking, delivered through a Yardi Systems integration and its CoverTrack compliance product. Unusually for the Canadian insurance sector, APOLLO publishes a genuine, publicly readable developer portal at docs.apollocover.com — a Stoplight workspace with three public projects and downloadable OpenAPI definitions covering quote and application (pre-fill) for tenant insurance and compliance-status lookup for partner properties. The surface is real but partner-scoped: every call needs an affiliateId (a co-branded APOLLO subdomain) and an x-api-key token that APOLLO issues by hand to affiliates and property-manager partners, so there is no self-serve credential path and no consumer-facing API. Canada has no open-insurance mandate — OSFI supervises prudentially, the provinces (FSRA, AMF) supervise market conduct, and Consumer-Driven Banking excludes insurance entirely — so nothing forces this disclosure; APOLLO published it as a distribution strategy. No ACORD, AL3, IVANS or agency-management-system reference appears anywhere in its public site or documentation.

**Areas:** Insurance · Canada · Insurtech · Brokerage · Embedded Insurance · Property and Casualty · Tenant Insurance · Quoting · Distribution · Compliance

## APOLLO Insurance on APIs.io

Everything profiled for APOLLO Insurance is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/apollo-insurance/](https://apis.io/providers/apollo-insurance/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [APOLLO Insurance Affiliates API](https://apis.io/apis/apollo-insurance/apollo-insurance-affiliates-api/) — The Affiliates API from APOLLO Insurance — 2 operation(s) for affiliates.
- [APOLLO Insurance Compliance API](https://apis.io/apis/apollo-insurance/apollo-insurance-compliance-api/) — The Compliance API from APOLLO Insurance — 3 operation(s) for compliance.
- [APOLLO Insurance Quote API](https://apis.io/apis/apollo-insurance/apollo-insurance-quote-api/) — The Quote API from APOLLO Insurance — 1 operation(s) for quote.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Apollo Insurance Covertrack Webhooks](https://apis.io/asyncapis/apollo-insurance/apollo-insurance-covertrack-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [apollo-insurance](https://apis.io/servers/apollo-insurance/apollo-insurance/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Apollo Insurance Agentic Access](https://apis.io/agentic-access/apollo-insurance/apollo-insurance-agentic-access/)

#### Collections (3)

Postman and Open Collection request collections.

- [Affiliates API](https://apis.io/collections/apollo-insurance/open-apollo-insurance-affiliates/)
- [Public API - Affiliates](https://apis.io/collections/apollo-insurance/open-apollo-insurance-affiliates-legacy/)
- [CoverTrack API's](https://apis.io/collections/apollo-insurance/open-apollo-insurance-covertrack/)

#### Overlays (3)

OpenAPI overlays, including conversational phrasing for each operation.

- [Apollo Insurance Affiliates Legacy Overlay](https://apis.io/overlays/apollo-insurance/apollo-insurance-affiliates-legacy-overlay/)
- [Apollo Insurance Affiliates Overlay](https://apis.io/overlays/apollo-insurance/apollo-insurance-affiliates-overlay/)
- [Apollo Insurance Covertrack Overlay](https://apis.io/overlays/apollo-insurance/apollo-insurance-covertrack-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Apollo Insurance Authentication](https://apis.io/security/apollo-insurance/apollo-insurance-authentication/)
- [Apollo Insurance Domain Security](https://apis.io/security/apollo-insurance/apollo-insurance-domain-security/)
- [Apollo Insurance Trust Center](https://apis.io/security/apollo-insurance/apollo-insurance-trust-center/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://apollocover.com/)
- [Documentation](https://docs.apollocover.com/docs/public-affiliate-api/27500feeac1b7-introduction)
- [Getting started](https://docs.apollocover.com/docs/public-affiliate-api/27500feeac1b7-introduction)
- [API reference](https://docs.apollocover.com/docs/public-affiliate-api/a8a7ea17b0889-affiliates-api)
- [Support](https://help.apollocover.com/en/)
- [Blog](https://apollocover.com/magazine)
- [Compliance](https://apollocover.com/security)
- [Terms of service](https://apollocover.com/terms-conditions/)
- [Privacy policy](https://apollocover.com/privacy-policy)

## API Evangelist rating

**Kin Score 52.4** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 79.5 |
| Contract quality | 57.7 |
| Contract governance | 18.2 |
| Operational transparency | 18.4 |
| Developer ergonomics | 66.1 |
| Access clarity | 43.4 |

**Agent readiness 24.4** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | derived (partial credit) |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | — |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | — |

**Regulatory alignment 26.3** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/apollo-insurance/](https://apis.io/providers/apollo-insurance/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for APOLLO Insurance: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/apollo-insurance/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
