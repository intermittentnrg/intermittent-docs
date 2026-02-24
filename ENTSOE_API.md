# ENTSO-E API Data Source

**Quick Facts:**
- **Region:** European Union + associated countries (35+ bidding zones)
  - Full country code list in documentation below
- **Website:** https://transparency.entsoe.eu/
- **API Documentation:** https://documenter.getpostman.com/view/7009892/2s93JtP3F6
- **Timezone:** UTC (all timestamps)
- **Data Format:** XML
- **Units:** MWh (hourly) or MW (quarterly), €/MWh (prices)
- **Resolution:** PT60M (hourly) or PT15M (15-minute)
- **Availability:** 
  - Historical data from 2014-01-01
  - 1-year max range recommended per request
  - Requires API token

## Endpoints

### Actual Generation per Production Type (A75)
**Quick Facts:**
- **URL:** `https://web-api.tp.entsoe.eu/api`
- **Documentation:** https://transparency.entsoe.eu/api-documentation
- **Parameters:** 
  - `documentType`: A75
  - `processType`: A16 (Realised)
  - `in_Domain`: Bidding zone EIC code
  - `periodStart`/`periodEnd`: `%Y%m%d%H%M` format
- **Notes:** Aggregated generation per production type

### Actual Generation per Generation Unit (A73)
**Quick Facts:**
- **URL:** `https://web-api.tp.entsoe.eu/api`
- **Parameters:** 
  - `documentType`: A73
  - `processType`: A16 (Realised)
  - `in_Domain`: Bidding zone EIC code
  - `periodStart`/`periodEnd`: `%Y%m%d%H%M` format
- **Notes:** Unit-level data

### Actual Total Load (A65)
**Quick Facts:**
- **URL:** `https://web-api.tp.entsoe.eu/api`
- **Parameters:** 
  - `documentType`: A65
  - `processType`: A16 (Realised)
  - `outBiddingZone_Domain`: Bidding zone EIC code
  - `periodStart`/`periodEnd`: `%Y%m%d%H%M` format
- **Notes:** National electricity demand

### Energy Prices (A44)
**Quick Facts:**
- **URL:** `https://web-api.tp.entsoe.eu/api`
- **Parameters:** 
  - `documentType`: A44
  - `in_domain`/`out_Domain`: Bidding zone EIC code
  - `periodStart`/`periodEnd`: `%Y%m%d%H%M` format
- **Units:** €/MWh (stored as cents/MWh, ×100)
- **Notes:** Day-ahead market prices; filter by `contract_MarketAgreement.type=A01` and `classificationSequence_AttributeInstanceComponent.position=1`

### Cross-Border Physical Flows (A11)
**Quick Facts:**
- **URL:** `https://web-api.tp.entsoe.eu/api`
- **Parameters:** 
  - `documentType`: A11
  - `out_Domain`: From bidding zone EIC code
  - `in_Domain`: To bidding zone EIC code
  - `periodStart`/`periodEnd`: `%Y%m%d%H%M` format
- **Notes:** Transmission between bidding zones

## Authentication

API requires security token:
- Environment variable: `ENTSOE_TOKEN`
- Token is passed as `securityToken` parameter
- Obtain token from ENTSO-E Transparency Platform registration

## Country/Bidding Zone Codes

EIC codes for countries and bidding zones:

| Code | Region | Code | Region |
|------|--------|------|--------|
| AL | Albania | BE | Belgium |
| AT | Austria | BG | Bulgaria |
| BA | Bosnia | CH | Switzerland |
| CZ | Czech Republic | CY | Cyprus |
| DE | Germany | DE-LU | Germany-Luxembourg |
| DK | Denmark | DK1 | Western Denmark |
| DK2 | Eastern Denmark | EE | Estonia |
| ES | Spain | FI | Finland |
| FR | France | GB | Great Britain (exited 2021) |
| GE | Georgia | GR | Greece |
| HR | Croatia | HU | Hungary |
| IE | Ireland | IE(SEM) | Ireland SEM |
| IT | Italy | IT-BR | Italy BR |
| IT-CA | Italy CA | IT-CNO | Italy CNO |
| IT-CSO | Italy CSO | IT-FO | Italy FO |
| IT-NO | Italy NO | IT-PR | Italy PR |
| IT-SAR | Italy Sardinia | IT-SIC | Italy Sicily |
| IT-SO | Italy SO | LT | Lithuania |
| LU | Luxembourg | LV | Latvia |
| MD | Moldova | ME | Montenegro |
| MK | North Macedonia | NL | Netherlands |
| NO | Norway | NO1 | Norway NO1 |
| NO2 | Norway NO2 | NO3 | Norway NO3 |
| NO4 | Norway NO4 | NO5 | Norway NO5 |
| PL | Poland | PT | Portugal |
| RO | Romania | RS | Serbia |
| SE | Sweden | SE1 | Sweden SE1 |
| SE2 | Sweden SE2 | SE3 | Sweden SE3 |
| SE4 | Sweden SE4 | SI | Slovenia |
| SK | Slovakia | UA | Ukraine |
| XK | Kosovo | | |

## Process Types

| Code | Type |
|------|------|
| A01 | Day-ahead |
| A16 | Realised |
| A18 | Current |
| A40 | Intraday |

## PSR (Power System Resource) Types

Production type codes (B01-B20):

| Code | Production Type |
|------|----------------|
| B01 | Biomass |
| B02 | Fossil Brown coal/Lignite |
| B03 | Fossil Coal-derived gas |
| B04 | Fossil Gas |
| B05 | Fossil Hard coal |
| B06 | Fossil Oil |
| B07 | Fossil Oil shale |
| B08 | Fossil Peat |
| B09 | Geothermal |
| B10 | Hydro Pumped Storage |
| B11 | Hydro Run-of-river and poundage |
| B12 | Hydro Water Reservoir |
| B13 | Marine |
| B14 | Nuclear |
| B15 | Other renewable |
| B16 | Solar |
| B17 | Waste |
| B18 | Wind Offshore |
| B19 | Wind Onshore |
| B20 | Other |

## Notes

- API params: `%Y%m%d%H%M` format for periodStart/periodEnd
- Response time format: `%Y-%m-%dT%H:%M%z`
- Resolution: PT60M (hourly) or PT15M (quarterly)
- Gap-filling supported with curveType=A03
- Position-based time series (1-indexed)
- 1-year max range recommended per request

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/entsoe_api.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/ENTSOE.py)
