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
- **Columns:**
  - Generation: Fuel Type, Available Capacity, Net Generation, Contingency Reserve
  - Transmission: Area, Flow (MW)

```
Current Supply Demand Report

Last Update : Feb 02, 2026 23:32

Alberta Total Net Generation,11468
Net Actual Interchange,1085
Alberta Internal Load (AIL),10383

COGENERATION,6137,4837,52
WIND,5684,3035,0
COMBINED CYCLE,3974,2477,10

British Columbia,939
Montana,-5
Saskatchewan,151
TOTAL,1085
```

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
- **Headers:** Api-Key
- **Notes:** Pool Price Report with begin_datetime_utc

## Fuel Types

| Code | Description |
|------|-------------|
| ENERGY STORAGE | Energy storage |
| GAS | Gas |
| COGENERATION | Cogeneration |
| COMBINED CYCLE | Combined cycle |
| GAS FIRED STEAM | Gas fired steam |
| SIMPLE CYCLE | Simple cycle |
| COAL | Coal |

## Notes
- Transmission: MW (negative for imports, positive for exports)
- MST timezone for historical data

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/aeso.rb)
- [gridstatus.io](https://github.com/gridstatus/gridstatus/blob/main/gridstatus/aeso/aeso.py)
