---
name: Embed an Open insurance quote and hand the customer over
description: >-
  Prepare a pre-filled insurance quote with the Open.js browser SDK, redirect the
  customer into Open's hosted (optionally white-labelled) journey, and poll for
  the purchase outcome — the path Open actually supports for quote-to-bind.
api: packages/open-insurance-packages.yml
surface: Open.js browser SDK (no REST equivalent is published)
operations:
  - opensdk.load
  - opensdk.quote.prepare
  - opensdk.quote.portal
  - opensdk.quote.status
  - opensdk.quote.history
  - opensdk.manage.portal
generated: '2026-07-25'
method: generated
source: https://developers.beopen.com/docs/openjs
---

# Embed a quote and hand the customer over

Open does not expose quote, bind, issue, servicing or claims as REST operations.
The supported integration is **client-side**: create and pre-fill a quote with
the browser SDK, hand the customer into Open's hosted journey to price and buy,
then poll for the outcome.

**These are documented Open.js SDK methods, not OpenAPI operations.** There is no
`operationId` to call server-side — do not attempt to reconstruct the underlying
HTTP calls from the minified library.

## 1. Load the library

```html
<script type="text/javascript"
  src="https://opensdk.s3-ap-southeast-2.amazonaws.com/opensdk-1.3.0.min.js"></script>
```

Include it once, in `<head>`, and initialise before calling anything else:

```javascript
opensdk.load("YOUR_API_KEY");            // production
opensdk.load("YOUR_API_KEY", { sandbox: true });  // sandbox
```

`sandbox: true` repoints `apiEndpoint` and `portalUrl` at
`api.sandbox.beopen.com` / the sandbox portal. Defaults to `false` — pin the
script URL to a version, there is no "latest" alias.

The API key is public by necessity (it ships to the browser). It identifies the
partner; it is not the secret. The **secret key never goes near the browser**.

## 2. Prepare a pre-filled quote

```javascript
const quote = await opensdk.quote.prepare("YOUR_PRODUCT_CODE", "YOUR_QUOTE_REF", {
  quote: {
    policy_holder_given_name: "Billy",
    policy_holder_last_name: "Jean",
    policy_holder_dob: "1984-08-22",
    policy_holder_email: "billy.jean@example.com",
    policy_holder_mobile: "0466859434",
    risk_address: "2 MARKET ST, SYDNEY NSW 2000",
    start_date: "2024-10-20",
    frequency: "M"
  }
});
```

- `productCode` is **required** and is issued per partner account.
- `quoteRef` is your own reference — use it to tie the journey to your cart or
  checkout, then poll with it later.
- Everything in `details.quote` is **optional pre-fill**; the customer can change
  it in the journey.
- All properties are per-product. Common: `policy_holder_*`, `start_date`,
  `frequency` (`M` monthly / `U` upfront), `excess`, `risk_address`,
  `cover_type`. Car adds `vehicle`, `kms_estimated`, `exclude_under_25`,
  `finance_type`, `finance_provider`, `policy_holder_licence_*`. Travel adds
  `travel_destination` (ISO 3166-1 alpha-3 list), `trip_start_date`,
  `trip_end_date`. UK mobile adds `device`, `device_date_of_purchase`,
  `device_imei`. Home (legacy shape) nests `policy_holder`, `dwelling` and a
  structured `address`.
- Dates are `YYYY-MM-DD`.

`risk_address` drives the underwriting outcome — it is the overnight parking
address for car, the building address for home, the policy-holder address for
travel. Some addresses decline cover; test with the published sample addresses in
`sandbox/open-insurance-sandbox.yml`.

## 3. Hand the customer over

```javascript
opensdk.quote.portal();  // uses the last quote in opensdk.quote.history
```

The customer completes pricing, purchase and payment inside Open's hosted
journey, which can be served from your own domain (see the domain white-labelling
guide). You never see the premium or take the card — Open does.

`opensdk.quote.history` is an in-memory array of `{product_code, quote_ref}` for
this page load only. **It is cleared on refresh** — persist your own `quoteRef`
if you need it after navigation, and always pass both arguments explicitly rather
than relying on the "last quote" default.

## 4. Poll for the outcome

There are **no webhooks**. No event catalog, no callbacks, no AsyncAPI. Polling
is the documented mechanism:

```javascript
const quote = await opensdk.quote.status("YOUR_PRODUCT_CODE", "YOUR_QUOTE_REF");
// { purchased: Boolean, expired: Boolean, policy_slug: String }

if (quote.expired)        { /* prepare a new quote */ }
else if (quote.purchased) { /* policy_slug is the new policy */ }
else                      { /* still in journey */ }
```

Open publishes no recommended interval or backoff. Poll conservatively on
customer return, not on a tight timer.

## 5. Send an existing customer to policy management

```javascript
opensdk.manage.portal();
```

Defaults to `https://insurance.beopen.com`.

## Deprecated — do not use in new work

Both are marked deprecated verbatim in Open's docs:

- **`opensdk.magiclink(email, redirect)`** — emails the customer a login link.
- **HS256 JWT `authToken`** — a token signed with your secret key, passed to
  `opensdk.load` or as a `jwt` query parameter, unlocking `customer_ref` linking
  and resume-quote. No replacement is published; if you need customer linking,
  raise it with your account manager rather than building on a deprecated path.

## Rules to follow

1. **Never put the secret key in browser code.** It signs tokens server-side
   only. The API key is the public half.
2. **No idempotency contract exists.** Calling `quote.prepare` twice creates two
   quotes. Guard against double-submit in your own UI.
3. **Store your `quoteRef` server-side.** The SDK's history does not survive a
   page reload.
4. **Handle "cover declined" as a normal outcome**, not an error — some risk
   addresses fall outside underwriting guidelines by design.
5. **Card declines surface in Open's journey**, not to you. The published
   `decline_code` vocabulary is in `errors/open-insurance-decline-codes.yml`;
   never show a customer `lost_card` or `stolen_card` as a reason.
