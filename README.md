# Open (open-insurance)

Open Insurance Pty Limited (ABN 23 166 949 444, AFSL 451712), trading as Open, is an Australian insurtech and underwriting agency that packages car, home and contents, landlord and travel cover as an embedded product other brands can sell. Open is not a carrier — it holds a binding authority from the insurer, acts as the insurer's agent to issue, vary, renew and cancel policies and to handle claims, and appoints partner brands as authorised representatives. Huddle Insurance is a business name of Open, and partner programs include Bupa and the SuperSaveClub marketplace; the business also operates in the United Kingdom and New Zealand from its Australian home market.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/open-insurance/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/open-insurance/refs/heads/main/apis.yml)

## Tags

- Insurance
- Australia
- Insurtech
- Embedded Insurance
- Property and Casualty
- Travel Insurance
- Underwriting
- Policy Administration
- White Label
- Quote

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## APIs

### Open Certificate of Currency API

The single documented server-side REST operation on the Open Platform. `POST /v1/policy/coc` retrieves a Certificate of Currency for an existing policy directly from the insurer to validate cover, returning JSON or PDF. Credentials are an `api_key` / `api_secret` pair passed in the request body, issued by Open at partner account creation. The published OpenAPI 3.0.3 definition declares the sandbox host `https://api.sandbox.beopen.com`; the production host `https://api.beopen.com` answers the same path (GET returns 405, POST only).

- **Human URL:** [https://developers.beopen.com/reference/coc](https://developers.beopen.com/reference/coc)
- **Base URL:** `https://api.beopen.com`

#### Tags

- Insurance
- Policy
- Certificate of Currency
- Australia

#### Properties

- [OpenAPI](openapi/open-insurance-certificate-of-currency-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [API Reference](https://developers.beopen.com/reference/coc)
- [Documentation](https://developers.beopen.com/docs/welcome)
- [Documentation — Keys](https://developers.beopen.com/docs/keys)
- [Documentation — Error codes](https://developers.beopen.com/docs/errors)

### Open.js Embedded Insurance SDK

Open's browser JavaScript library for embedding insurance into a partner's web app. Documented methods are `opensdk.quote.load`, `opensdk.quote.prepare`, `opensdk.quote.portal`, `opensdk.quote.status`, `opensdk.quote.history`, `opensdk.magiclink` and `opensdk.manage.portal`. It creates and pre-fills a quote and polls its status, then hands the customer to Open's hosted portal to complete purchase, manage the policy and claim — bind and issue are not exposed as API calls. Sibling integration surfaces documented in the same hub are Open.Widget and a URL handover redirect.

- **Human URL:** [https://developers.beopen.com/docs/openjs](https://developers.beopen.com/docs/openjs)
- **Base URL:** `https://api.beopen.com`

#### Tags

- Insurance
- Embedded Insurance
- SDK
- Quote

#### Properties

- [API Reference](https://developers.beopen.com/docs/openjs)
- [Documentation — Install Open.js](https://developers.beopen.com/docs/using-openjs)
- [Documentation — Prepare a quote](https://developers.beopen.com/docs/prepare-a-quote)
- [Documentation — Check quote status](https://developers.beopen.com/docs/check-quote-status)
- [Documentation — Retrieve quote history](https://developers.beopen.com/docs/retrieve-quote-history)
- [Documentation — Redirect to portal](https://developers.beopen.com/docs/redirect-to-portal)
- [Documentation — Redirect to policy portal](https://developers.beopen.com/docs/redirect-to-policy-portal)
- [Documentation — Request a magic link](https://developers.beopen.com/docs/request-a-magic-link)
- [Documentation — Authenticating using JWT](https://developers.beopen.com/docs/authenticating-using-jwt)
- [Documentation — Open.Widget](https://developers.beopen.com/docs/embedded-widget)
- [Documentation — URL handover](https://developers.beopen.com/docs/url-handover)
- [Documentation — Domain white-labelling](https://developers.beopen.com/docs/domain-white-labelling)

## API Posture

Open's API posture is real but narrow and partner-gated:

- **Developer portal:** [https://developers.beopen.com/docs/welcome](https://developers.beopen.com/docs/welcome) — HTTP 200, a public and unauthenticated ReadMe.io hub with guides, quickstarts, a sandbox section and an API Reference. Not a login wall.
- **OpenAPI:** one real OpenAPI 3.0.3 definition, harvested verbatim from the ReadMe API registry on 2026-07-25.
- **Quote / bind / issue / FNOL:** quote is prepared and polled through the SDK; bind, issue, policy servicing and claims happen inside Open's hosted (optionally white-labelled) journey rather than over an API. No FNOL or claims API is published.
- **Auth:** API key + secret pair issued per environment at partner account creation — no self-serve signup. A deprecated HS256 JWT signed with the secret key unlocks advanced SDK features. No OAuth2 or OIDC metadata is served.
- **Webhooks / GraphQL / gRPC / Postman:** none published.
- **MCP:** `https://developers.beopen.com/mcp` answers JSON-RPC but rejects anonymous `initialize` with HTTP 401 "Authorization required".
- **ACORD:** no ACORD, AL3, ACORD XML, NGDS, IVANS, Applied Epic or Vertafore reference found anywhere on the site or in the documentation.

> **Disambiguation:** the domain `open.com.au` is *not* this company — it redirects to Radiator Software (formerly Open System Consultants, makers of the Radiator RADIUS/AAA server). Open the insurtech is at [beopen.com](https://www.beopen.com/).

## Links

- [Website](https://www.beopen.com/)
- [Developer Documentation](https://developers.beopen.com/docs/welcome)
- [API Reference](https://developers.beopen.com/reference)
- [llms.txt](https://developers.beopen.com/llms.txt)
- [Customer policy portal](https://insurance.beopen.com/)
- [Contact](https://www.beopen.com/contact)
- [Terms (Australia)](https://www.beopen.com/terms/australia)
- [LinkedIn](https://www.linkedin.com/company/beopen)

## Maintainers

- Kin Lane — kin@apievangelist.com
