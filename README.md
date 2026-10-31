# Open

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

Open Insurance Pty Limited (ABN 23 166 949 444, AFSL 451712), trading as Open, is an Australian insurtech and underwriting agency that packages car, home and contents, landlord and travel cover as an embedded product other brands can sell. Open is not a carrier — it holds a binding authority from the insurer, acts as the insurer's agent to issue, vary, renew and cancel policies and to handle claims, and appoints partner brands as authorised representatives. Huddle Insurance is a business name of Open, and partner programs include Bupa and the SuperSaveClub marketplace; the business also operates in the United Kingdom and New Zealand from its Australian home market. Its API posture is real but narrow and partner-gated. Open runs a public, unauthenticated ReadMe developer hub at developers.beopen.com covering the Open.js browser SDK, the Open.Widget embed and a URL-handover redirect, plus exactly one documented server-side REST operation — POST /v1/policy/coc, Retrieve a Certificate of Currency — for which a real OpenAPI 3.0.3 definition is published. Quote is only prepared and polled through the SDK; bind, issue, policy servicing and claims all happen inside Open's hosted (optionally white-labelled) journey rather than over an API, and there is no public FNOL, webhook, GraphQL or Postman surface. API keys and secrets are issued by Open at partner account creation — there is no self-serve signup — and no ACORD, AL3 or NGDS reference appears anywhere on the site or in the documentation.

**Areas:** Insurance · Australia · Insurtech · Embedded Insurance · Property and Casualty · Travel Insurance · Underwriting · Policy Administration · White Label · Quotes

## Open on APIs.io

Everything profiled for Open is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/open-insurance/](https://apis.io/providers/open-insurance/)** — or go straight to one of the APIs or properties below.

### APIs (2)

- [Open.js Embedded Insurance SDK](https://apis.io/apis/open-insurance/open-js-embedded-insurance-sdk/) — Open's browser JavaScript library for embedding insurance into a partner's web app. Documented methods are opensdk.quote.load, opensdk.quote.prepare,…
- [Open Policy API](https://apis.io/apis/open-insurance/open-insurance-policy-api/) — The Policy API from Open — 1 operation(s) for policy.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [open-insurance-mcp.yml](https://apis.io/servers/open-insurance/open-insurance-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Open Insurance Agentic Access](https://apis.io/agentic-access/open-insurance/open-insurance-agentic-access/)

#### Collections (1)

Postman and Open Collection request collections.

- [Open Insurance API](https://apis.io/collections/open-insurance/open-open-insurance-certificate-of-currency/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Open Insurance Certificate Of Currency Overlay](https://apis.io/overlays/open-insurance/open-insurance-certificate-of-currency-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Open Insurance Authentication](https://apis.io/security/open-insurance/open-insurance-authentication/)
- [Open Insurance Domain Security](https://apis.io/security/open-insurance/open-insurance-domain-security/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.beopen.com/)
- [Documentation](https://developers.beopen.com/docs/welcome)
- [Getting started](https://developers.beopen.com/docs/using-openjs)
- [API reference](https://developers.beopen.com/reference)
- [Support](https://www.beopen.com/contact)
- [Blog](https://www.beopen.com/research)
- [Compliance](https://www.beopen.com/terms/australia)
- [Terms of service](https://www.beopen.com/terms/australia)
- [Privacy policy](https://www.beopen.com/terms/australia)
- [Status](https://developers.beopen.com/docs/check-service-status)

## API Evangelist rating

**Kin Score 40.7** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 41.0 |
| Contract governance | 18.2 |
| Operational transparency | 7.9 |
| Developer ergonomics | 53.0 |
| Access clarity | 42.1 |

**Agent readiness 38.3** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 26.3** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/open-insurance/](https://apis.io/providers/open-insurance/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Open: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/open-insurance/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
