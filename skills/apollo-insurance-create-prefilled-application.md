---
name: Create a pre-filled tenant application and hand off to the launchpad
description: >-
  Quote, then create a pre-filled APOLLO tenant insurance application and return the consumer a
  quoteLink into the affiliate's co-branded launchpad, where they complete purchase and pay.
  Covers both the standard flow and the Yardi embedded resident-enrolment flow.
api: openapi/apollo-insurance-affiliates.yml
operations:
  - public-api-affiliates-quote-post
  - public-api-affiliates-application-post
generated: '2026-07-25'
method: generated
---

# Create a pre-filled tenant application

## Understand what this does before you call it

**Creating an application does not bind a policy.** It returns `data.quoteLink` — a URL into the
affiliate's co-branded APOLLO launchpad with the consumer's answers pre-filled. The consumer
completes purchase and pays there. APOLLO exposes no ISSUE operation and no claims/FNOL
operation; the machine-to-machine surface stops at the handoff.

There is also **no callback**. Nothing tells you whether the consumer completed the purchase.
Treat the `quoteLink` as the end of the API flow and reconcile out of band.

## Prerequisites

- `affiliateId` (the partner's co-branded APOLLO subdomain) and an `x-api-key`, both hand-issued
  by an APOLLO contact. Separate keys for test and production.
- `insuranceType` must be `tenant` — the only line currently available.

## Step 1 — quote first (optional but recommended)

Call `public-api-affiliates-quote-post` as described in
`skills/apollo-insurance-quote-tenant-insurance.md` so you can show a price before creating
anything.

## Step 2 — create the application

`public-api-affiliates-application-post`

```
POST /api/affiliates/{affiliateId}/{insuranceType}/application
x-api-key: <token>
Content-Type: application/json
```

The body has five optional-at-the-schema-level fields, but the combination matters:

| Field | When to send |
|---|---|
| `insuranceData` | **Required for non-embedded applications.** A `TenantInsuranceQuestions` object — same shape as the quote question set. |
| `embeddedOptions` | **Required for embedded applications.** See step 3. |
| `paymentPeriod` | `annual` (default) or `monthly`. |
| `externalId` | Your own unique client ID — **always send this**. See "Preventing duplicates". |
| `leadSource` | `partnerName` (required within the object, e.g. the landlord name) and optional `partnerSubdomain`. |

Required fields inside `insuranceData`: `businessAddressStreet`, `businessAddressCity`,
`businessAddressPostal`, `operations`.

`leadSource.partnerSubdomain` routes the consumer to a sub-launchpad under the partner; leave it
empty to fall back to the partner's default launchpad.

## Step 3 — the Yardi embedded flow

For automated resident enrolment at lease signing, send `embeddedOptions` **instead of**
`insuranceData`:

```json
{
  "embeddedOptions": {
    "embeddedPlatform": "yardi",
    "embeddedType": "start",
    "tenantId": "T12345678",
    "propertyId": "P12345678"
  },
  "externalId": "your-unique-id",
  "leadSource": { "partnerName": "Example Property Group" }
}
```

- `embeddedPlatform` is required and `yardi` is the only value in the published enum — no other
  property-management system is exposed.
- `tenantId` is the Yardi **tcode / residentId**; `propertyId` is the Yardi **property code**.
- These are the same codes CoverTrack keys compliance on, so an embedded application and a
  later compliance lookup line up.

## Step 4 — return the link

A 200 returns:

```json
{ "data": { "quoteLink": "https://apollo.securequotebot.com/tenants?quote=<uuid>" } }
```

Hand that URL to the consumer. Do not scrape it, do not attempt to complete purchase on their
behalf, and do not treat reaching this step as coverage being in force.

## Preventing duplicates

APOLLO's only deduplication contract is the **`externalId` body field**, documented as: *"Customer's
own unique ID. This ID will be included in the APOLLO application to prevent duplicate
applications from being created for the client."*

- There is **no `Idempotency-Key` header**, no replay window, no stored-response semantics and no
  409 conflict status.
- Always send a stable `externalId` derived from your own record for that client, and reuse the
  same value on retry.

## Failures

- **400** — validation error, proprietary Joi/celebrate envelope. Read `message.details[].context.key`
  for the offending field and fix it before retrying. Common cause: sending neither
  `insuranceData` nor `embeddedOptions`.
- **403** — bad or wrong-environment `x-api-key`.
- **404** — bad `affiliateId`, or `insuranceType` other than `tenant`.
- No 401, 409, 429 or 5xx response is documented. Treat anything else as unknown and do not
  blind-retry a write.

## Rules

- **This is a write. Escalate to a human.** It produces a link a real consumer will be sent and
  captures their personal information. Do not let an agent fire it unsupervised.
- **Never invent applicant answers.** Every field must come from the consumer or the property
  system of record. Guessing coverage limits or a birthdate is misrepresentation on an insurance
  application.
- **Test host for anything that is not a real consumer.** Production creates real customer-facing
  applications.
- **Retry only with the same `externalId`.**
