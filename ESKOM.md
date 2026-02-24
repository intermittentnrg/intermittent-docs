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
- **Columns:**
  - Thermal_Gen_Excl_Pumping_and_SCO
  - Nuclear_Generation
  - Eskom_Gas_Generation
  - Eskom_OCGT_Generation
  - Dispatchable_IPP_OCGT
  - Hydro_Water_Generation
  - Pumped_Water_Generation
  - Pumped_Water_SCO_Pumping
  - Wind
  - PV
  - CSP
  - Other_RE

```
Date Time Hour Beginning,Thermal Generation,Nuclear Generation,Eskom Gas Generation,Eskom OCGT Generation,Hydro Water Generation,Pumped Water Generation,Dispatchable IPP OCGT,Wind,PV,CSP,Other RE
2021-04-01 12:00:00 AM,21352.0,920.0,0.0,1.0,0.0,0.0,0.0,705.691,0.0,0.0,17.147
```

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
