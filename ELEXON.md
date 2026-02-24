# ELEXON Data Source

**Quick Facts:**
- **Region:** Great Britain (England, Scotland, Wales) - `GB`
- **Website:** https://bmrs.elexon.co.uk/api-documentation
- **Timezone:** UTC (all timestamps)
- **Data Format:** JSON
- **Units:** MW
- **Resolution:** 30-minute settlement periods, 5-minute unit-level
- **Availability:** 
  - Real-time (FUELINST)
  - Historical (AGPT, ATL): 7-day max range per request
  - Unit-level (B1610): 5 business days delayed

## Endpoints

### Fuel Instant (FUELINST) - Generation & Transmission
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/datasets/FUELINST`
- **Documentation:** https://bmrs.elexon.co.uk/api-documentation
- **Parameters:** `settlementDateFrom`/`settlementDateTo`: YYYY-MM-DD
- **Notes:** Real-time generation by fuel type and international transmission

**Interconnectors:**
- INTELE/INTELEC → FR (France)
- INTEW/INTGRNL/INTIRL → IE (Ireland)
- INTFR → FR (France)
- INTIFA2 → FR (France - IFA2)
- INTNED → NL (Netherlands)
- INTNEM → BE (Belgium)
- INTNSL → NO (Norway)
- INTVKL → DK (Denmark)

### Actual Generation Per Type (AGPT)
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/datasets/AGPT`
- **Parameters:** `publishDateTimeFrom`/`publishDateTimeTo`: YYYY-MM-DD HH:MM
- **Notes:** Historic generation per type for GB_B1620 area; 7-day maximum range

### Actual Total Load (ATL)
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/demand/actual/total`
- **Parameters:** `from`/`to`: YYYY-MM-DD
- **Notes:** National electricity demand; 7-day maximum range

### Generation Unit Output (B1610)
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/datasets/B1610`
- **Parameters:** `settlementDate`: YYYY-MM-DD, `settlementPeriod`: 1-50
- **Notes:** Unit-level generation data; 5 business days delayed; iterate through all 50 settlement periods per day

### Installed Generation Capacity (IGCA)
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/datasets/IGCA`
- **Resolution:** Yearly (P1Y)
- **Notes:** Yearly installed capacity per production type for GB_B1620

### Unit Capacity (IGCPU)
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/datasets/IGCPU`
- **Notes:** Unit-level installed capacity with commissioning/decommissioning dates

## Production Type Mapping

| ELEXON Code | Production Type |
|-------------|----------------|
| BIOMASS | biomass |
| CCGT | fossil_gas_ccgt |
| COAL | fossil_hard_coal |
| NPSHYD | hydro |
| NUCLEAR | nuclear |
| OCGT | fossil_gas_ocgt |
| OIL | fossil_oil |
| OTHER | other |
| PS | hydro_pumped_storage |
| WIND | wind |

## Notes
- Settlement periods: 30-minute intervals (1-50 per day)
- Timestamp format: `%Y-%m-%dT%H:%M:%SZ` (ISO 8601 UTC)
- Date format: `%Y-%m-%d`
- Datetime format: `%Y-%m-%d %H:%M`
- FUELINST provides both generation and transmission data
- B1610 unit data requires iterating through all 50 settlement periods per day

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/elexon.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/ELEXON.py)

