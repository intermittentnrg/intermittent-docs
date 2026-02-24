# Eskom Data Source

**Quick Facts:**
- **Region:** South Africa - `ZA`
- **Website:** https://www.eskom.co.za/
- **Data Portal:** https://www.eskom.co.za/dataportal/
- **Timezone:** Africa/Johannesburg (UTC+2, no DST)
- **Data Format:** CSV
- **Units:** MW
- **Resolution:** Hourly
- **Availability:**
  - Current data: 7-day build-up available
  - Historical data: 5 years via request form
  - Supports HTTP conditional requests via If-Modified-Since

## Endpoints

### Demand Data
**Quick Facts:**
- **URL:** `https://www.eskom.co.za/dataportal/wp-content/uploads/%Y/%m/System_hourly_actual_and_forecasted_demand.csv`
- **Notes:** Hourly national electricity demand; Key column: RSA Contracted Demand (MW)

### Generation Data
**Quick Facts:**
- **URL:** `https://www.eskom.co.za/dataportal/wp-content/uploads/%Y/%m/Station_Build_Up.csv`
- **Notes:** Hourly generation by production type

**Production Type Mapping:**
- Thermal_Gen_Excl_Pumping_and_SCO → fossil_coal
- Nuclear_Generation → nuclear
- Eskom_Gas_Generation → fossil_gas
- Eskom_OCGT_Generation + Dispatchable_IPP_OCGT → fossil_oil
- Hydro_Water_Generation → hydro
- Pumped_Water_Generation + Pumped_Water_SCO_Pumping → hydro_pumped_storage
- Wind → wind
- PV → solar
- CSP → solar_thermal
- Other_RE → other_renewable

### Historical Data Request
**Quick Facts:**
- **URL:** `https://www.eskom.co.za/dataportal/data-request-form/`
- **Notes:** POST form for bulk historical CSV downloads; Requires fields: name, email, institution, purpose, date range, and checkboxes for desired data columns

## Notes

- Current data time format: `%Y-%m-%d %H:%M:%S` (24h, e.g., 2024-01-15 14:30:00)
- Historical data time format: `%Y-%m-%d %I:%M:%S %p` (12h AM/PM, e.g., 2024-01-15 02:30:00 PM)
- All timestamps are local Johannesburg time (SAST), converted to UTC (-2h)
- International imports/exports data present but not processed
- Load shedding (MLR) data present but not processed

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/eskom.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/ESKOM.py)
