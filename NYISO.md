# NYISO Data Source

**Quick Facts:**
- **Region:** New York State, USA - `US-NY`
- **Website:** http://mis.nyiso.com/
- **Data Portal:** http://mis.nyiso.com/public/csv/rtfuelmix/ (browse available files)
- **Timezone:** America/New_York (UTC-5/-4 with DST)
- **Data Format:** CSV (direct) or ZIP (monthly archive)
- **Units:** MW
- **Resolution:** 5-minute intervals
- **Availability:** Real-time; last 7 days as direct CSV, older data in monthly ZIP archives

## Endpoints

### Real-time Fuel Mix (Generation)
**Quick Facts:**
- **URL (recent ≤7 days):** `http://mis.nyiso.com/public/csv/rtfuelmix/{YYYYMMDD}rtfuelmix.csv`
- **URL (historical >7 days):** `http://mis.nyiso.com/public/csv/rtfuelmix/{YYYYMMDD}rtfuelmix_csv.zip`
- **Notes:**
  - Recent data available as direct CSV
  - Historical data requires monthly ZIP archive (contains all days in month)
  - Time format: `%m/%d/%Y %H:%M:%S`
- **Columns:**
  - Time Stamp
  - Time Zone
  - Fuel Category
  - Gen MW

### Load
**Quick Facts:**
- **URL (recent ≤7 days):** `http://mis.nyiso.com/public/csv/pal/{YYYYMMDD}pal.csv`
- **URL (historical >7 days):** `http://mis.nyiso.com/public/csv/pal/{YYYYMMP}pal_csv.zip`
- **Notes:**
  - Total load and zonal load data
- **Columns:**
  - Time Stamp
  - Time Zone
  - Name
  - Load

### Load Forecast
**Quick Facts:**
- **URL:** `http://mis.nyiso.com/public/csv/isolf/{YYYYMMDD}isolf.csv`
- **Notes:**
  - Day-ahead load forecast
- **Columns:**
  - Time Stamp
  - Time Zone
  - Name
  - Forecast

### Real-time LMP (Locational Marginal Pricing)
**Quick Facts:**
- **URL:** `http://mis.nyiso.com/public/csv/realtime/{YYYYMMDD}realtime.csv`
- **Notes:**
  - 5-minute LMP data by location
- **Columns:**
  - Time Stamp
  - Time Zone
  - Name
  - LBMP
  - Loss
  - Congestion
  - Energy

### Day-Ahead LMP
**Quick Facts:**
- **URL:** `http://mis.nyiso.com/public/csv/damlbmp/{YYYYMMDD}damlbmp.csv`
- **Notes:**
  - Hourly day-ahead LMP data
- **Columns:**
  - Time Stamp
  - Time Zone
  - Name
  - LBMP
  - Loss
  - Congestion
  - Energy

## Notes
- Time format: `%m/%d/%Y %H:%M:%S` (Time Stamp column)
- Skip rows with missing Time Stamp, Fuel Category, or Gen MW values
- ZIP archives for historical data contain all CSV files for the entire month, not just the requested date
- Recent data (≤7 days old) available as direct CSV for faster single-day queries

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/nyiso.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/US_NY.py)
- [gridstatus.io](https://github.com/gridstatus/gridstatus/blob/main/gridstatus/nyiso.py)
