# Taipower Data Source

**Quick Facts:**
- **Region:** Taiwan - `TW`
- **Website:** https://www.taipower.com.tw/
- **Real-time Data:** https://www.taipower.com.tw/2764/2826/2829/2830/25090/
- **Historical Data:** https://www.taipower.com.tw/2764/2826/2829/2832/25093/normalPost
- **Timezone:** Asia/Taipei (UTC+8, no DST)
- **Data Format:** JSON
- **Units:** MW
- **Resolution:** 10-minute
- **Availability:** 
  - Real-time via SQS queue consumption
  - Historical data only available as 24-hour averages on website
  - Data collected via separate fetcher script and archived to: https://github.com/intermittentnrg/intermittent-taipower-sns-sqs

## Data Collection

**Data Flow:**
1. Fetcher retrieves JSON snapshots from Taipower API
2. Publishes to AWS SNS topic
3. SQS queue receives messages
4. This importer consumes from SQS (configured via `TAIPOWER_QUEUE_URL` env var)

## Production Type Mapping

| Taipower Code | Production Type | Notes |
|--------------|----------------|-------|
| NUCLEAR | nuclear | |
| COAL | fossil_coal | |
| COGEN | cogeneration | |
| IPPCOAL | fossil_coal | Independent Power Producer coal |
| LNG | fossil_gas | |
| IPPLNG | fossil_gas | Independent Power Producer LNG |
| OIL | fossil_oil | |
| DIESEL | fossil_oil_diesel | |
| HYDRO | hydro | |
| WIND | wind_onshore / wind_offshore | Detected via unit name |
| SOLAR | solar | |
| PUMPINGGEN | hydro_pumped_storage | |
| OTHERRENEWABLEENERGY | other_renewable | |
| ENERGYSTORAGESYSTEM | hydro_pumped_storage / battery | Detected via unit name |
| ENERGYSTORAGESYSTEMLOAD | storage | |

## Unit-Level Classification

Units are further classified by inspecting unit names:
- Contains "Geothermal" → geothermal
- Contains "Biofuel" → biomass

## Notes

- Time format: `%Y-%m-%d %H:%M`
- Generation aggregates: Sum of units grouped by production type (rows with "Subtotal" in unit_id)
- Unit-level data: Individual power plant outputs
- Duplicate detection by timestamp
- Unit IDs may contain remarks in parentheses (stripped)
- Data provided at both generation aggregate and unit-level granularity

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/taipower.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/TAIPOWER.py)
