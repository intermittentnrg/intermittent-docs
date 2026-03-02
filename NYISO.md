# NYISO Data Source

**Quick Facts:**
- **Region:** New York State, USA - `US-NY`
- **Website:** http://mis.nyiso.com/
- **Data Portal:** http://mis.nyiso.com/public/csv/rtfuelmix/ (browse available files)
- **Timezone:** America/New_York (UTC-5/-4 with DST)
- **Data Format:** CSV or ZIP (archive)
- **Units:** MW
- **Resolution:** 5-minute intervals
- **Availability:** Real-time; recent data as CSV (~14 days) and monthly ZIP archives

## Endpoints

### Real-time Fuel Mix (Generation)
**Quick Facts:**
- **URL:** `http://mis.nyiso.com/public/csv/rtfuelmix/{YYYYMMDD}rtfuelmix.csv` (available ~14 days)
- **URL:** `http://mis.nyiso.com/public/csv/rtfuelmix/{YYYYMM}01rtfuelmix_csv.zip`
- **Notes:**
- Recent data available as CSV or monthly ZIP from 1st of current month
  - Previous months available as monthly ZIP archive only (contains all days in month)
  - Time format: `%m/%d/%Y %H:%M:%S`
- **Columns:**
  - Time Stamp
  - Time Zone
  - Fuel Category
  - Gen MW

### Load
**Quick Facts:**
- **URL:** `http://mis.nyiso.com/public/csv/pal/{YYYYMMDD}pal.csv` (available ~10 days)
- **URL:** `http://mis.nyiso.com/public/csv/pal/{YYYYMM}01pal_csv.zip`
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
- Server sends Last-Modified header but does not support conditional requests with If-Modified-Since

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importers/blob/master/lib/nyiso.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/US_NY.py)
- [gridstatus.io](https://github.com/gridstatus/gridstatus/blob/main/gridstatus/nyiso.py)
