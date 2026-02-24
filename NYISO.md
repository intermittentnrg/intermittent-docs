# NYISO Data Source

**Quick Facts:**
- **Region:** New York State, USA - `US-NY`
- **Website:** http://mis.nyiso.com/
- **Timezone:** America/New_York (UTC-5/-4 with DST)
- **Data Format:** CSV (ZIP)
- **Units:** MW
- **Resolution:** Hourly
- **Availability:** Real-time daily ZIP files

## Endpoints

### Real-time Fuel Mix
**Quick Facts:**
- **URL:** `http://mis.nyiso.com/public/csv/rtfuelmix/{YYYYMMDD}rtfuelmix_csv.zip`
- **Notes:** 
  - ZIP file containing CSV
  - Time format: `%m/%d/%Y %H:%M:%S`
- **Columns:**
  - Time Stamp
  - Time Zone
  - Fuel Category
  - Gen MW

## Notes
- Time format: `%m/%d/%Y %H:%M:%S` (Time Stamp column)
- Skip rows with missing Time Stamp, Fuel Category, or Gen MW values

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/nyiso.rb)
- [gridstatus.io](https://github.com/gridstatus/gridstatus/blob/main/gridstatus/nyiso.py)
