# ERCOT Data Source

**Note:** API is geoblocked (US-only). Proxy API exists but requires API key.

**Quick Facts:**
- **Region:** Texas, USA - `ERCOT` or `US-TX`
- **Website:** https://www.ercot.com/
- **Timezone:** America/Chicago (UTC-6/-5 with DST)
- **Data Format:** JSON
- **Units:** MW
- **Resolution:** Hourly
- **Availability:** Real-time; geoblocked (US-only)

## Endpoints

### Official ERCOT API
**Quick Facts:**
- **URL:** `https://www.ercot.com/api/1/services/read/dashboards/fuel-mix.json`
- **Documentation:** https://www.ercot.com/api-docs/
- **Notes:** Geoblocked (US-only). Alternative data sources exist.

## Production Type Mapping

| ERCOT Code | Production Type |
|-----------|----------------|
| Coal and Lignite | fossil_coal |
| Hydro | hydro |
| Nuclear | nuclear |
| Other | other |
| Power Storage | storage |
| Solar | solar |
| Wind | wind |
| Natural Gas | fossil_gas |

## Notes
- Time format: `%Y-%m-%d %H:%M:%S`
- Data structure:
```json
{
  "data": {
    "2024-01-15": {
      "2024-01-15 14:00:00": {
        "Natural Gas": {"gen": 12345.6},
        "Wind": {"gen": 5000.0}
      }
    }
  }
}
```

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/ercot.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/US_ERCOT.py)
- [gridstatus.io](https://github.com/gridstatus/gridstatus/blob/main/gridstatus/ercot.py)
