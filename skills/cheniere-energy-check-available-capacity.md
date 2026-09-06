---
method: generated
generated: '2026-09-06'
source: >-
  Authored by API Evangelist against operationIds in openapi/cheniere-energy-lng-connection.yml,
  each probed live on 2026-09-06. Cheniere publishes no skills or AGENTS.md.
name: cheniere-check-available-capacity
description: >-
  Find how much unscheduled capacity is operationally available on a Cheniere interstate pipeline
  for a given gas day and nomination cycle, using the public FERC informational-postings API.
api: Cheniere LNG Connection — Pipeline Informational Postings API
base_url: https://lngconnectionapi.cheniere.com
authentication: none
operations:
  - getPages
  - getCycles
  - getCapacityLocations
  - getOperationallyAvailableCapacity
  - getUnsubscribedCapacity
---

# Check available capacity on a Cheniere pipeline

No credential is required. Every call below is an anonymous GET.

## 1. Pick the pipeline

`tspNo` selects the pipeline and is required on nearly every call.

- `200` — Cheniere Creole Trail Pipeline, L.P. (DUNS 800742780, FERC CID C001506)
- `400` — Cheniere Corpus Christi Pipeline, L.P. (DUNS 079841991)

`600` and `800` are routable but returned zero rows when probed. If you want to confirm the
current list rather than trust these values, call `getPages` and read `companies`.

    GET /api/Page/GetPages

## 2. Read the nomination cycles — do not hard-code them

    GET /api/Capacity/GetCycles

Returns the five NAESB cycles. The ids are **not** sequential:
`1` Timely, `10` Evening, `132` Intraday 1, `148` Intraday 2, `166` Intraday 3.

## 3. Resolve a location id

    GET /api/Capacity/GetLocations?tspNo=200&beginDate=2026-09-01&endDate=2026-09-05

Location ids are opaque strings (`CT109413`, `BRGJB`). Never construct one — read it here, or from
`getLocationList` for the full master list including inactive points.

## 4. Ask for the capacity posting

    GET /api/Capacity/GetCapacity?tspNo=200&beginDate=2026-09-05&cycleId=1&locationId=CT109413

This is the FERC 18 CFR 284.13(d) posting. The response is the report envelope — `{ "report": [...],
"beginDate": "..." }`, with no `endDate`, because this is a single-gas-day query.

Read these fields from each row:

- `desigN_OPER_CAP` — design operating capacity
- `opeR_CAP` — current operational capacity
- `scheD_QTY` — quantity already scheduled
- `qtY_AVAIL` — **the answer**: quantity operationally available
- `meaS_BASIS` — the unit. `BZ` means MMBtu.
- `loC_PURP_DESC` / `loC_QTI` — whether this is a receipt or delivery point
- `caP_TYPE_DESC` — confirms this is "Operationally available unscheduled capacity"
- `postinG_DT_TIME` — when the pipeline posted it

## 5. For unsubscribed firm capacity, use a different endpoint

    GET /api/Capacity/GetUnsubscribed?tspNo=200&beginDate=2026-09-01

Different posting class, different shape: a bare array, not the report envelope, with `loC_CAP`
as the capacity figure.

## Conventions that will bite you

- **Field casing is mangled.** `tsP_NO`, `loC_ID`, `efF_DT_FROM`, `qtY_AVAIL`. Match keys
  case-insensitively with underscores stripped; do not compare literals across endpoints.
- **Two response shapes.** `getOperationallyAvailableCapacity` returns the report envelope;
  `getUnsubscribedCapacity` returns a bare array. Handle both.
- **No pagination and no truncation signal.** Window by gas day.
- **No caching.** `Cache-Control: no-cache`, no ETag. Poll no faster than the cycle turns over.
- **Errors are not RFC 9457.** A failure is `{"message": "An error has occurred."}` with no code
  and no request id — there is nothing to quote in a support ticket.
- **An unknown `tspNo` returns 200 with zero rows**, not an error. An empty result does not prove
  there is no capacity; check that your `tspNo` is 200 or 400 first.
