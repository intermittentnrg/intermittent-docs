# AESO Data Source

**Quick Facts:**
- **Region:** Alberta, Canada - `CA-AB`
- **Website:** https://www.aeso.ca/
- **Timezone:** America/Edmonton (UTC-7/-6 with DST)
- **Data Format:** CSV
- **Units:** MW (generation, transmission), $/MWh (price)
- **Resolution:** Real-time, hourly (historical)
- **Availability:** 
  - Real-time: Current Supply Demand Report
  - Historical: Unit-level data, Pool Price API (requires API key)

## Endpoints

### Current Supply Demand Report
**Quick Facts:**
- **URL:** `http://ets.aeso.ca/ets_web/ip/Market/Reports/CSDReportServlet?beginDate=&endDate=&contentType=csv`
- **Time format:** `"Last Update : %B %d, %Y %H:%M"`
- **Notes:** 
  - Multiple CSV chunks separated by blank lines
  - Format: Header, Last Update timestamp, Summary (Alberta Internal Load), Generation by fuel type, Transmission (interties), Unit-level data by fuel type
  - Dual fuel units mapped to both types
  - Unit names parsed from ASSET column (format: "Name (ID)" → extract ID)

### Historical Unit Data (GenerationHistory)
**Quick Facts:**
- **URL:** CSV file (downloaded from AESO portal)
- **Time format:** `%Y-%m-%d %H:%M` (MST)
- **Resolution:** Hourly
- **Notes:** Columns include Date (MST), Date (MPT), Asset Short Name, Asset Name, Asset Grouping, Volume (generation), Maximum Capability, System Capability, Fuel Type, Sub Fuel Type

### Pool Price (API)
**Quick Facts:**
- **URL:** `https://apimgw.aeso.ca/public/poolprice-api/v1.1/price/poolPrice`
- **Documentation:** https://www.aeso.ca/market/experience-open-data/
- **Time format:** `%Y-%m-%d %H:%M` (UTC)
- **Parameters:** `startDate`/`endDate`: YYYY-MM-DD
- **Headers:** Api-Key (from `AESO_PRIMARY_KEY` env var)
- **Notes:** Pool Price Report with begin_datetime_utc

## Production Type Mapping

| AESO Code | Production Type |
|-----------|----------------|
| ENERGY STORAGE | battery |
| GAS / COGENERATION / COMBINED CYCLE / GAS FIRED STEAM / SIMPLE CYCLE | fossil_gas |
| COAL | fossil_hard_coal |
| Other types | lowercase with underscores |

## Notes
- Transmission: MW (negative for imports, positive for exports)
- MST timezone for historical data

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/aeso.rb)
- [gridstatus.io](https://github.com/gridstatus/gridstatus/blob/main/gridstatus/aeso/aeso.py)
