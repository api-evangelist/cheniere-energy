# Cheniere Energy (cheniere-energy)

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

Cheniere Energy, Inc. is an international energy company headquartered in Houston, Texas, and the leading producer and exporter of liquefied natural gas (LNG) in the United States, operating the Sabine Pass terminal in Louisiana and the Corpus Christi terminal in Texas. It also owns two FERC-regulated interstate natural gas pipelines, Cheniere Creole Trail Pipeline and Cheniere Corpus Christi Pipeline. Cheniere runs no developer program and publishes no API documentation, yet it does operate one public, unauthenticated JSON API: the LNG Connection informational-postings API at lngconnectionapi.cheniere.com, serving the pipeline capacity, transactional reporting, Index of Customers, gas quality, imbalance and notice postings that FERC 18 CFR 284.13 requires, in the NAESB Wholesale Gas Quadrant data model.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/cheniere-energy/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cheniere-energy/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Producing
- **Access:** 3rd-Party

## Tags

- Corpus Christi
- Energy
- Export
- FERC
- Houston
- Informational Postings
- LNG
- Liquefaction
- NAESB
- Natural Gas
- Open Data
- Pipelines
- Regasification
- Sabine Pass
- Texas

## Timestamps

- **Created:** 2026-03-21
- **Modified:** 2026-09-06

## APIs

### Cheniere Energy Website

Cheniere Energy's corporate website. It carries no developer documentation and no API reference; supplier and contractor integration is handled through a dedicated portal. The company's one public API is described in the separate LNG Connection entry.

- **Human URL:** [https://www.cheniere.com](https://www.cheniere.com)
- **Base URL:** `https://www.cheniere.com`

#### Tags

- Energy
- Export
- LNG
- Natural Gas

#### Properties

- [Website](https://www.cheniere.com)
- [Supplier Portal](https://www.cheniere.com/about/resources/suppliers-and-contractors)
- [Operations](https://www.cheniere.com/about/where-we-work)

### Cheniere LNG Connection Pipeline Informational Postings API

The public, unauthenticated JSON API behind Cheniere's LNG Connection site, which publishes the FERC-mandated informational postings for Cheniere Creole Trail Pipeline, L.P. (tspNo 200) and Cheniere Corpus Christi Pipeline, L.P. (tspNo 400). It serves operationally available and unsubscribed capacity by NAESB nomination cycle, firm and interruptible transactional reporting, the quarterly Index of Customers, daily and comingled gas quality, posted imbalances, operational notices, and the location, station and contact reference data. 35 operations, all data operations read-only, no credential of any kind. Cheniere publishes no OpenAPI and no documentation for it; the specification in this repository was derived by API Evangelist from the provider's own client bundle plus live anonymous probes on 2026-09-06 and is labelled as derived.

- **Human URL:** [https://lngconnection.cheniere.com](https://lngconnection.cheniere.com)
- **Base URL:** `https://lngconnectionapi.cheniere.com`

#### Tags

- Natural Gas
- Pipelines
- FERC
- NAESB
- Capacity
- Gas Quality
- Informational Postings
- Open Data
- Energy

#### Properties

- [OpenAPI](openapi/cheniere-energy-lng-connection.yml)
- [Overlay](overlays/cheniere-energy-lng-connection-overlay.yaml)
- [MCP Server](mcp/cheniere-energy-mcp.yml)
- [Tool Crosswalk](mcp/cheniere-energy-tool-crosswalk.yml)
- [Authentication](authentication/cheniere-energy-authentication.yml)
- [Error Catalog](errors/cheniere-energy-problem-types.yml)
- [Conventions](conventions/cheniere-energy-conventions.yml)
- [Data Model](data-model/cheniere-energy-data-model.yml)
- [Conformance](conformance/cheniere-energy-conformance.yml)
- [Lifecycle](lifecycle/cheniere-energy-lifecycle.yml)
- [Rate Limits](rate-limits/cheniere-energy-rate-limits.yml)
- [Plans](plans/cheniere-energy-plans-pricing.yml)
- [Agent Skills](skills/_index.yml)
- [Website](https://lngconnection.cheniere.com)

## Common Properties

- [Domain Security](security/cheniere-energy-domain-security.yml)
- [LinkedIn](https://www.linkedin.com/company/cheniere-energy-inc)
- [Website](https://www.cheniere.com)
- [Supplier Portal](https://www.cheniere.com/about/resources/suppliers-and-contractors)
- [Investor Relations](https://www.cheniere.com/investors)
- [Careers](https://www.cheniere.com/careers)
- [Contact Us](https://www.cheniere.com/contact-us)
- **Operations:** Sabine Pass LNG Terminal, Corpus Christi LNG Terminal, Cheniere Marketing, Creole Trail Pipeline, Corpus Christi Pipeline
- **Services:** LNG Liquefaction, LNG Vessel Loading, Regasification, Natural Gas Marketing, Long-Term LNG Sales and Purchase Agreements
- **Use Cases:** International LNG Export, Long-Term LNG Supply Contracts, Spot LNG Cargo Sales, Energy Security, Natural Gas Liquefaction Services
- [Sustainability](https://www.cheniere.com/our-responsibility)
- [Newsroom](https://www.cheniere.com/newsroom)
- [Operations](https://www.cheniere.com/about/where-we-work)
- [OpenAPI](openapi/cheniere-energy-lng-connection.yml)
- [Overlay](overlays/cheniere-energy-lng-connection-overlay.yaml)
- [MCP Server](mcp/cheniere-energy-mcp.yml)
- [Tool Crosswalk](mcp/cheniere-energy-tool-crosswalk.yml)
- [Authentication](authentication/cheniere-energy-authentication.yml)
- [Error Catalog](errors/cheniere-energy-problem-types.yml)
- [Conventions](conventions/cheniere-energy-conventions.yml)
- [Data Model](data-model/cheniere-energy-data-model.yml)
- [Conformance](conformance/cheniere-energy-conformance.yml)
- [Lifecycle](lifecycle/cheniere-energy-lifecycle.yml)
- [Rate Limits](rate-limits/cheniere-energy-rate-limits.yml)
- [Plans](plans/cheniere-energy-plans-pricing.yml)
- [Packages](packages/cheniere-energy-packages.yml)
- [Agent Skills](skills/_index.yml)
- [llms.txt](llms/cheniere-energy-llms.txt)
- [Privacy Policy](https://www.cheniere.com/about/resources/privacypolicy)
- [Terms of Service](https://www.cheniere.com/about/resources/disclaimer)
- [Investor Relations](https://cqpir.cheniere.com/)
- [Support](https://www.cheniere.com/letstalk)

## Maintainers

**FN:** Kin Lane  
**Email:** kin@apievangelist.com
