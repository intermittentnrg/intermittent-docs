# OpenNEM Data Source

**Note:** No longer used in favor of direct AEMO data sources.

**Quick Facts:**
- **Region:** Australia - NEM and WEM regions
  - `AUS-NSW` → `NSW1`, `AUS-QLD` → `QLD1`, `AUS-SA` → `SA1`, `AUS-TAS` → `TAS1`, `AUS-VIC` → `VIC1`, `AUS-WA` → `WEM`
- **Website:** https://opennem.org.au/
- **Timezone:** Varies by region (AEST: UTC+10, AWST: UTC+8)
- **Data Format:** JSON
- **Units:** MW
- **Resolution:** 5min or 30min
- **Availability:** Real-time and historical

## Endpoints

### Monthly Stats
**Quick Facts:**
- **URL:** `https://api.opennem.org.au/stats/power/network/fueltech/{network}/{region}`
- **Documentation:** https://opennem.org.au/docs/
- **Parameters:** `month`: YYYY-MM-DD

### Weekly Historic Data
**Quick Facts:**
- **URL:** `https://data.opennem.org.au/v3/stats/historic/weekly/{network}/{region}/year/{YYYY}/week/{week}.json`

### Latest Real-time
**Quick Facts:**
- **URL:** `https://data.opennem.org.au/v3/clients/em/latest.json`

## Production Type Mapping

| OpenNEM Code | Production Type |
|--------------|----------------|
| coal_black | fossil_hard_coal |
| coal_brown | fossil_brown_coal/lignite |
| gas_ccgt | fossil_gas_ccgt |
| gas_ocgt | fossil_gas_ocgt |
| gas_recip | fossil_gas_reciprocating |
| gas_steam | fossil_gas_steam |
| gas_wcmg | fossil_gas_coal_mine_waste |
| distillate | fossil_oil_distillate |
| hydro | hydro |
| wind | wind |
| bioenergy_biogas | biogas |
| bioenergy_biomass | biomass |
| solar_utility | solar_utility |
| solar_rooftop | solar_rooftop |
| battery_charging | battery_charging |
| battery_discharging | battery |
| pumps | hydro_pumped_storage |

## Notes
- Replaced by AEMO NEM for Eastern Australia and AEMO WEM for Western Australia

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/opennem.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/OPENNEM.py)
