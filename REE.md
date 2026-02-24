# REE Data Source

**Quick Facts:**
- **Region:** Canary Islands, Spain - `ES-CN-FVLZ` (Fuerteventura/Lanzarote zone)
- **Website:** https://demanda.ree.es/
- **Timezone:** Atlantic/Canary (UTC+0, no DST)
- **Data Format:** JSON (wrapped in callback function)
- **Units:** MW
- **Resolution:** Hourly
- **Availability:** Real-time; fetches 30 hours of data per request (6 hours before to 24 hours after)

## Endpoints

### Generation Data
**Quick Facts:**
- **URL:** `https://demanda.ree.es/WSvisionaMovilesCanariasRest/resources/demandaGeneracionCanarias`
- **Notes:** 
  - `curva`: "LZ_FV5M" (curve identifier)
  - `fecha`: YYYY-MM-DD (date)
  - `system`: "Canarias"

Hourly generation data for the Canary Islands.

## Production Type Mapping

| REE Code | Production Type | Notes |
|----------|----------------|-------|
| die | fossil_oil | Diesel |
| gas | fossil_gas | Natural gas |
| eol | wind_onshore | Wind |
| fot | solar | Photovoltaic |
| hid | hydro_pumped_storage | Pumped hydro |
| cc | - | Ignored (combined cycle) |
| vap | - | Ignored (vapor/steam) |
| gnhd | - | Ignored (hydro generation) |
| turb | - | Ignored (pumping turbine) |
| conb | - | Ignored (pumping consumption) |
| efl | - | Ignored (exchange) |
| dem | - | Ignored (demand) |

## Notes
- API returns JSON wrapped in a callback function (stripped before parsing)
- Only 5 production types are currently mapped and stored
- Time format: `%Y-%m-%d %H:%M`
- Leap second notation: `1A` (normal 01:00) and `1B` (during leap second) both converted to 01:00

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/ree.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/ES.py)
