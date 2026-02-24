# EIA Data Source

**Quick Facts:**
- **Region:** United States - Regional balancing authorities
  - Balancing Authority Codes: `US48` (Continental US total), `CISO` (California ISO), `ERCOT`, `PJM`, `NYIS`, etc.
- **Website:** https://www.eia.gov/
- **API Documentation:** https://www.eia.gov/docs/opendata/documentation-v2.pdf
- **Timezone:** UTC (all timestamps)
- **Data Format:** JSON
- **Units:** MW (load, generation, interchange)
- **Resolution:** Hourly
- **Availability:** 
  - Historical data available
  - Max 5000 rows per request (use pagination with `offset`)
  - Requires API key

## Endpoints

### Load (Region Data)
**Quick Facts:**
- **URL:** `https://api.eia.gov/v2/electricity/rto/region-data/data/`
- **Parameters:** 
  - `frequency`: hourly
  - `start`/`end`: YYYY-MM-DD
  - `facets[type][]`: D (demand)
  - `facets[respondent][]`: balancing authority code
  - `offset`: pagination (max 5000 rows per request)
- **Response Fields:** `period`: YYYY-MM-DDTHH (hour beginning), `respondent`: Balancing authority code, `value`: Demand in MW

### Generation (Fuel Type Data)
**Quick Facts:**
- **URL:** `https://api.eia.gov/v2/electricity/rto/fuel-type-data/data/`
- **Parameters:** 
  - `frequency`: hourly
  - `facets[fueltype][]`: fuel type code
  - `facets[respondent][]`: balancing authority code
- **Notes:** Generation by fuel type

### Interchange (Transmission)
**Quick Facts:**
- **URL:** `https://api.eia.gov/v2/electricity/rto/interchange-data/data/`
- **Parameters:** 
  - `frequency`: hourly
  - `facets[fromba][]`: from balancing authority
  - `facets[toba][]`: to balancing authority
- **Notes:** Values are inverted (export measured as drain on from_area)

## Authentication

API key required:
- Environment variable: `EIA_TOKEN`
- Obtain API key from https://www.eia.gov/opendata/register/

## Production Type Mapping

| EIA Code | Production Type |
|----------|----------------|
| BAT | battery |
| COL | fossil_hard_coal |
| GEO | geothermal |
| NG | fossil_gas |
| NUC | nuclear |
| OIL | fossil_oil |
| OES | storage |
| OTH | other |
| PS | hydro_pumped_storage |
| SNB | solar_with_battery |
| SUN | solar |
| UES | unknown_storage |
| WAT | hydro |
| WND | wind |
| WNB | wind_with_battery |
| UNK | unknown |

## Notes

- API input time format: `%Y-%m-%d` (YYYY-MM-DD)
- API output time format: `%Y-%m-%dT%H` (YYYY-MM-DDTHH)
- Hour is "hour beginning" - subtract 1 hour to get interval end time
- Max 5000 rows per request requires pagination with `offset`

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/eia.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/EIA.py)
- [gridstatus.io](https://github.com/gridstatus/gridstatus/blob/main/gridstatus/eia.py)
