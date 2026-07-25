---
name: Quote tenant insurance for an affiliate
description: >-
  Price a Canadian tenant (renter) insurance application through the APOLLO Affiliates API and
  read back the premium breakdown, taxes, Stripe fees and totals. Quoting creates nothing and
  has no side effects.
api: openapi/apollo-insurance-affiliates.yml
operations:
  - public-api-affiliates-quote-post
generated: '2026-07-25'
method: generated
---

# Quote tenant insurance for an affiliate

## Before you start

You need two things APOLLO issues by hand — there is no self-serve path:

- an **`affiliateId`** — the partner's co-branded APOLLO subdomain
- an **`x-api-key`** token, with **separate values for test and production**

Pick the host deliberately:

| Environment | Host |
|---|---|
| Test | `https://o73td82enk.execute-api.ca-central-1.amazonaws.com/1_0_0` |
| Production | `https://fpl95knwc1.execute-api.ca-central-1.amazonaws.com/1_0_0` |

A Stoplight hosted mock server also fronts this project if you only need response shapes.
Use the test host for anything that is not a real consumer.

## Step 1 — call the quote operation

`public-api-affiliates-quote-post`

```
POST /api/affiliates/{affiliateId}/{insuranceType}/quote
x-api-key: <token>
Content-Type: application/json
```

- `insuranceType` **must be `tenant`**. The path is parameterised, but the documentation states
  only the tenant insurance type is currently available. Any other value returns 404.
- The body is `{ "insuranceData": { … } }` and `insuranceData` is **required**.
- `insuranceData` is `TenantInsuranceQuoteQuestions`. Four fields are required:
  `businessAddressStreet`, `businessAddressCity`, `businessAddressPostal`, `operations`.
  The `business*` prefixes are an artefact of a shared question engine across APOLLO's personal
  and commercial lines — for tenant insurance they are the **residential** address.
- Coverage-shaping fields worth setting: `personalLiability`, `deductible`,
  `propertyLimitApplicant`, `aleLimitApplicant`, `offPremisesLimitApplicant`, `policyPackage`,
  plus special-limit fields (`jewelryLimit`, `bicyclesLimit`, `computersLimit`) and
  `sewerDisclaimer` / `specialLimitException`.
- Applicant fields: `firstName`, `lastName`, `email`, `phoneNumber`, `birthdate`,
  `ageApplicant`, `buildingAge`.

## Step 2 — read the quote

A 200 returns everything under `data`:

- `premiums` — `contentsPremium`, `alePremium`, `liabilityPremium`, `addonPremium`
- `subtotal`, `stripeFees`, `taxesAndFees`, `total` — each broken out by
  `annual` / `monthly` / `instalment` (`total` also carries `monthlyPayment`, the per-month charge)
- `policyExpiryDate` — an ISO 8601 timestamp

Quote the **`total`**, not the subtotal: APOLLO itemises processing fees separately and the
consumer pays the total. `monthly` is the annualised cost of paying monthly;
`monthlyPayment` is what actually leaves the consumer's account each month. Do not confuse them.

## Step 3 — handle failures

There is no 401 and no 429 in this spec. The three documented failures are:

- **400** — validation error. The body is a proprietary Joi/celebrate envelope, not RFC 9457:
  `message.details[]` each carry `message`, `path[]`, `type` and `context.label` / `context.key`.
  Read `context.key` to know which field to fix, e.g.
  `"body.insuranceData.businessAddressPostal" is required`.
- **403** — bad or wrong-environment `x-api-key`. A production token will not authenticate
  against the test host.
- **404** — bad `affiliateId`, or an `insuranceType` other than `tenant`.

## Rules

- **Quoting is safe.** It creates no record. `POST` is used only because the question set is too
  large for a query string. It is fine for an agent to quote autonomously.
- **Do not retry a 400.** Fix the named field first — retrying the same body loops.
- **You are moving PII.** Name, birthdate, email, phone and home address go in the request.
  Handle it under whatever consent basis your deployment has; do not log the body.
- **Prices are not guaranteed.** APOLLO is a broker distributing on behalf of Canadian carriers
  and states advertised products and prices are not guaranteed. Re-quote before presenting.
- **No pagination, no idempotency, no rate limit is published** for this operation. See
  `conventions/apollo-insurance-conventions.yml`.
