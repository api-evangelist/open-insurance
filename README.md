# Open (open-insurance)

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
