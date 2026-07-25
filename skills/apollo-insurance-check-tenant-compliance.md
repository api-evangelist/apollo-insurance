---
name: Check tenant insurance compliance across a property portfolio
description: >-
  Read tenant-insurance compliance status for a whole property or a single tenant through the
  APOLLO CoverTrack API, interpret the status enum and third-party carrier policy detail, and
  quote a tenant who is out of compliance.
api: openapi/apollo-insurance-covertrack.yml
operations:
  - get-compliance-partnerId-propertyId
  - get-compliance-status
  - post-quote-tenant-partnerId
generated: '2026-07-25'
method: generated
---

# Check tenant insurance compliance

CoverTrack is APOLLO's compliance product for REITs and property managers. It answers one
question — *does this tenant currently carry tenant insurance?* — for tenants insured by APOLLO
**and** for tenants who uploaded proof of a third-party carrier's policy.

## Prerequisites

- `partnerId` (the partner name), `propertyId` (the property ID / "P-Code") and `tenantId`
  (the tenant ID / "T-Code"), all issued by APOLLO. In Yardi-embedded deployments these are the
  Yardi property code and tcode / residentId.
- An `x-api-key` header token. The spec declares no `securitySchemes` block, but **every path
  carries an explicit `x-api-key` header parameter** — send it.

| Environment | Host |
|---|---|
| Test | `https://api.covertrack-dev.ca` |
| Production | `https://api.covertrack.ca` |

## Step 1 — sweep a property

`get-compliance-partnerId-propertyId`

```
GET /compliance/{partnerId}/{propertyId}
x-api-key: <token>
```

Returns a JSON **array** of `ComplianceStatus` records, one per tenant.

**There is no pagination.** No cursor, no offset, no limit, no page parameter, no envelope. A
large property returns whole in a single response — budget memory and timeout accordingly, and
do not build a paging loop that will never terminate.

## Step 2 — read one tenant

`get-compliance-status`

```
GET /compliance/{partnerId}/{propertyId}/{tenantId}
x-api-key: <token>
```

A **404 "User Not Found"** means that partner/property/tenant triple is unknown — it does **not**
mean the tenant is uninsured. Do not report a 404 as non-compliance; check the identifiers first.

## Step 3 — interpret the record

```
partnerId, propertyId, tenantId, status, updatedAt
policy: { startDate, endDate, policyNumber, provider, liability }   # optional
links:  { upload }
```

`status` is a string with four documented values:

| Status | Meaning | What to do |
|---|---|---|
| `ACTIVE` | Coverage is in force | Nothing |
| `PENDING` | Submitted, not yet confirmed | Wait; re-check |
| `NOT_SUBMITTED` | No proof of insurance on file | Chase — surface `links.upload`, or quote them (step 4) |
| `DECLINED` | Submitted proof was rejected | Chase — the tenant must submit acceptable coverage |

Two things to get right:

- **`policy` describes the THIRD-PARTY carrier's policy**, not an APOLLO policy. `provider` is the
  other carrier's name and `policyNumber` is that carrier's number. APOLLO exposes no
  APOLLO-issued policy resource anywhere in its public API. Never present `policyNumber` as an
  APOLLO policy.
- **`policy` is optional.** Its absence is normal for `NOT_SUBMITTED`; do not treat a missing
  `policy` object as an error.

Surface `links.upload` to a tenant who needs to submit proof.

## Step 4 — quote a non-compliant tenant

`post-quote-tenant-partnerId`

```
POST /quote/tenant/{partnerId}
x-api-key: <token>
Content-Type: application/json

{ "propertyId": "...", "tenantId": "...", "contents": 0, "ale": 0,
  "liability": 0, "deductible": 0, "water": true }
```

Returns `link` (a URL to complete the application), `annual`, `monthly` and `monthlyPayment`.
Quoting creates nothing — `POST` is used for payload size only, so this is safe to call
autonomously. Hand the `link` to the tenant; do not complete it for them.

Note this is a **different contract** from the Affiliates quote operation: it is keyed on
partner/property/tenant with coverage limits, not on the full tenant question set.

## Staying current without polling

APOLLO documents one outbound callback — it POSTs a full `ComplianceStatus` snapshot to a
partner-supplied destination when a relevant policy event occurs. It is configured out of band
(there is no subscription API), it sends `x-api-key` only as "recommended", and it carries **no
HMAC signature, no timestamp, no retry policy and no delivery id**. See
`asyncapi/apollo-insurance-covertrack-webhooks.yml`.

Because the payload is a full state snapshot keyed on partner/property/tenant, replays are
naturally convergent — upsert on that triple rather than trying to deduplicate.

If you cannot host a destination, poll step 1 on a schedule instead.

## Rules

- **All three read operations are safe** for an agent to call. Nothing here mutates state.
- **Compliance status is a legal-adjacent fact.** Report exactly what `status` says; never infer
  "insured" from a missing record or a 404.
- **You are reading tenant PII and carrier policy numbers.** Do not log records; do not expose one
  tenant's record to another.
- No rate limit, no 429 and no 5xx response is published. Back off politely on your own schedule.
