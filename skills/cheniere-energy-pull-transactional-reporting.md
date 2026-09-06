---
method: generated
generated: '2026-09-06'
source: >-
  Authored by API Evangelist against operationIds in openapi/cheniere-energy-lng-connection.yml,
  each probed live on 2026-09-06. Cheniere publishes no skills or AGENTS.md.
name: cheniere-pull-transactional-reporting
description: >-
  Pull FERC-required transactional reporting and the quarterly Index of Customers for a Cheniere
  interstate pipeline — contracts, shippers, affiliate flags and rates — from the public
  informational-postings API.
api: Cheniere LNG Connection — Pipeline Informational Postings API
base_url: https://lngconnectionapi.cheniere.com
authentication: none
operations:
  - getFirmTransactionalReport
  - getInterruptibleTransactionalReport
  - listIndexOfCustomersQuarters
  - getIndexOfCustomers
  - getActiveSummaryNotices
---

# Pull transactional reporting from a Cheniere pipeline

This is the FERC 18 CFR 284.13(b) and (c) data: who holds capacity, on what contract, at what rate,
and whether they are an affiliate of the pipeline. It is public because the regulator requires it
to be. No credential.

## Firm transportation

    GET /api/Transactional/GetFirm?tspNo=200&beginDate=2026-09-01&endDate=2026-09-05

Returns the report envelope: `{ "report": [...], "beginDate": "...", "endDate": "..." }`.

Fields worth reading:

- `contractHolderName`, `contractHolderProp` — the shipper and its DUNS-based id
- `serviceRequesterContract` — the contract number
- `contractBeginDate`, `contractEndDate`
- `ctrMDQ` — contract maximum daily quantity
- `ctrLocMDQ` — the portion of that MDQ at THIS location
- `rateSchedule` (e.g. `FTS`), `rateCharged`, `maxTariffRate`
- `mktBasedRateInd`, `ngtdRateInd` — market-based and negotiated rate indicators
- `affil` — **the analytically interesting field.** Marks whether the shipper is affiliated with
  the pipeline. A value of `TSP` means Cheniere is moving gas for its own affiliate rather than a
  third party.

## Interruptible transportation

    GET /api/Transactional/GetInteruptible?tspNo=200&beginDate=2026-09-01&endDate=2026-09-05

Same shape. The single-`r` spelling in the path is the provider's own — reproduce it exactly.

## Capacity release is broken

    GET /api/Transactional/GetCapacityRelease?tspNo=200&beginDate=...&endDate=...

Returns HTTP 500. The one-parameter form the provider's own client calls returns 404. Observed
2026-09-06. Do not report an empty capacity-release set as "no releases" — the endpoint is not
answering.

## Index of Customers

Always list the quarters first. Do not construct the date.

    GET /api/IndexOfCustomers/Quarter
    GET /api/IndexOfCustomers/Get?firstDayOfQuarter=7/1/2026&tspNo=200

The response is the NAESB row structure, not a flat record: `header.row1` is the pipeline header
(indicator `H`, with the FERC pipeline id and reporting quarter), `header.row2` is shipper detail
(indicator `D`, with rate schedule, contract number, effective dates, days to expiry, MDQ and a
negotiated-rate indicator), `header.row3` is the agent (indicator `A`), and `section` carries
rollups. Roughly 24 quarters of history were available when probed.

## Counting contracts correctly

Transactional rows are **one row per contract per location**. A single contract fans out across
every point it touches, repeating `ctrMDQ` while `ctrLocMDQ` varies. Deduplicate on
`serviceRequesterContract` before you count contracts or you will overstate them badly.

## Check notices before drawing conclusions

    GET /api/Notice/GetActiveSummaryNotices?companyId=200

Operational notices (`description` is `Critical` or `Non-Critical`) explain gaps and anomalies in
the posting data. Note this endpoint names the parameter `companyId`, not `tspNo` — same value.

## Conventions

- Field casing differs between endpoints: `tspNo` here, `tsP_NO` on capacity rows, `companyId` on
  notices. Normalize keys before joining.
- Dates go in as `YYYY-MM-DD` or `M/D/YYYY`; they come back as local ISO date-times with no
  timezone offset. The gas-day convention applies and the offset is not stated in the payload.
- No pagination, no versioning, no rate-limit headers, no caching.
- The Index of Customers header carries a named human contact and phone number. It is published by
  regulation, but do not extract, store or redistribute it — take the posting data, leave the
  contact.
