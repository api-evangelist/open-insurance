---
name: Retrieve a Certificate of Currency from Open
description: >-
  Validate that an Open (Huddle) insurance policy is in force by retrieving its
  Certificate of Currency as JSON or PDF — the only server-side REST operation
  Open publishes.
api: openapi/open-insurance-certificate-of-currency-openapi.json
operations:
  - coc
generated: '2026-07-25'
method: generated
source: openapi/open-insurance-certificate-of-currency-openapi.json + https://developers.beopen.com/reference/coc
---

# Retrieve a Certificate of Currency

Use this when a lender, lessor, employer or the policy holder needs proof that an
Open-issued policy is currently in force — sum insured, excess, effective dates,
named holders and any noted financial interest.

This is the **only** public REST operation Open publishes. Everything else
(quote, buy, manage, claim) runs through the Open.js browser SDK and Open's
hosted journey. Do not look for a policy-list, policy-read or claims endpoint —
they do not exist.

## Before you start

- You need a partner **`api_key`** and **`api_secret`** pair. They are issued by
  Open at partner account creation (`sales@beopen.com`); there is **no self-serve
  signup**. Each account gets one pair per environment — `sandbox` and
  `production`.
- You need the customer's **`policy_number`** (e.g. `HMCP00001568`).
- Credentials go in the **JSON request body**, not in a header. There is no
  `Authorization` header, no OAuth and no API-key header on this API.

## Operation

`coc` — `POST /v1/policy/coc`

- Production host: `https://api.beopen.com`
- Sandbox host: `https://api.sandbox.beopen.com` (the OpenAPI `servers[]` block
  declares only this one)

### Request body

| field | required | notes |
| --- | --- | --- |
| `api_key` | yes | Partner API key for the environment you are calling |
| `api_secret` | yes | Partner secret for the same environment |
| `policy_number` | yes | The customer's policy number |
| `format` | no | `JSON` (default) or `pdf` |

```bash
curl -X POST https://api.beopen.com/v1/policy/coc \
  -H 'Content-Type: application/json' \
  -d '{
    "api_key": "YOUR_API_KEY",
    "api_secret": "YOUR_API_SECRET",
    "policy_number": "HMCP00001568"
  }'
```

## Reading the response

`200` returns one of two shapes, selected by the product behind the policy — the
spec models them as a `oneOf` with no discriminator, so **branch on the fields
present**, not on a type field.

- **Car**: `vehicle`, `vehilce_rego`, `sum_insured`, `base_excess`.
- **Home**: nested `home { sum_insured, base_excess }` and
  `contents { sum_insured, base_excess }`, plus `landlord`.

Both carry `timestamp`, `premium`, `policy_currency`, `policy_number`,
`policy_issued_date`, `policy_effective_from`, `policy_expires_on`, `policy`,
`policy_holders[]` (`given_name`, `last_name`, `dob`), `address` and
`financial_interest`.

Gotchas that are part of the contract, not bugs you can work around:

- `vehilce_rego` is **misspelled upstream**, in both the schema and the example.
  Read the typo'd key.
- Amounts are **strings** on the car shape (`"589.43"`, `"1000"`) but **integers**
  on the home shape's nested objects. Normalise before arithmetic.
- Timestamps use the non-standard form `2021-10-20T15:59:21Z+1100` — `Z` and an
  offset together. Do not feed them straight into a strict ISO-8601 parser.
- Cover is in force only if now falls between `policy_effective_from` and
  `policy_expires_on`. The response does not carry a boolean "active" flag.

Set `"format": "pdf"` when the requesting party needs a document to file rather
than data to parse.

## Error handling

There is **no RFC 9457 problem+json** here. Errors are a bare HTTP status; the
documented `403` body is the plain string `Attempt Logged.  Access denied.`

| status | meaning | what to do |
| --- | --- | --- |
| `401` | Invalid credentials | Check you are not using sandbox keys against production |
| `403` | Recognised but not entitled — and the attempt is logged | Stop retrying. Contact your Open account manager |
| `405` | Wrong method | This path is POST-only; a GET returns 405 |
| `422` | Velocity rules violation or non-sufficient funds | Back off |
| `500` / `502` / `503` / `504` | Platform-side | Retry with backoff; check the status feed |

Full table: `errors/open-insurance-problem-types.yml`.

## Rules to follow

1. **Never retry a 403.** The docs state the attempt is logged. Repeated denied
   lookups against policy numbers you are not entitled to is enumeration.
2. **There is no idempotency key.** Open documents none. The call is
   semantically a read, so a retry is safe, but do not assume any write
   elsewhere on the platform is replay-safe.
3. **There is no rate-limit signal.** No quota, no `429` in the documented status
   table, no rate-limit headers. Self-throttle and back off on 5xx.
4. **Treat the response as personal information.** It contains named policy
   holders, dates of birth and a residential address. Log the policy number, not
   the body.
5. **Keys belong in a secrets store.** They travel in the request body, so they
   will not be redacted by header-scrubbing proxies — make sure your own logging
   redacts `api_key` and `api_secret`.

## Testing

Use the sandbox key pair and `https://api.sandbox.beopen.com`. Published example
policy numbers are `HMCP00001568`, `PECP00000001` and `PEHXC0000001`. See
`sandbox/open-insurance-sandbox.yml`.
