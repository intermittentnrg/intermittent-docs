# CAISO Data Source

**Quick Facts:**
- **Region:** California, USA - `CAISO`
- **Website:** https://www.caiso.com/
- **Data Portal:** https://www.caiso.com/outlook/
- **Timezone:** America/Los_Angeles (US/Pacific, UTC-8/-7 with DST)
- **Data Format:** CSV
- **Units:** MW
- **Resolution:** Hourly
- **Availability:**
  - Daily historical CSV files
  - Supports HTTP conditional requests via If-Modified-Since

## caiso.com Endpoints

### Fuel Source (Generation)
**Quick Facts:**
- **URL:** `https://www.caiso.com/outlook/history/%Y%m%d/fuelsource.csv`
- **Date in URL:** `%Y%m%d` format (e.g., 20240115)
- **Time in CSV:** `%H:%M` format combined with date from URL
- **Notes:** Daily CSV with hourly generation by fuel type; generation data includes imports as transmission flows

**Production Type Mapping:**

| Column | Production Type |
|--------|----------------|
| Solar | solar |
| Wind | wind_onshore |
| Geothermal | geothermal |
| Biomass | biomass |
| Biogas | biogas |
| Small hydro | hydro_small |
| Coal | fossil_hard_coal |
| Nuclear | nuclear |
| Natural Gas | fossil_gas |
| Large Hydro | hydro_large |
| Batteries | battery |
| Imports | import (mapped to transmission) |
| Other | other |

### Load Data
**Quick Facts:**
- **URL:** `https://www.caiso.com/outlook/history/%Y%m%d/netdemand.csv`
- **Date in URL:** `%Y%m%d` format (e.g., 20240115)
- **Time in CSV:** `%H:%M` format combined with date from URL
- **Notes:** Daily CSV with hourly demand data; key columns: Current demand (column 2), Hour ahead forecast (column 1), Net demand (column 3)

**Notes:**
- Time format: `%H:%M` (e.g., 14:00) combined with date from URL
- All timestamps are Pacific time, converted to UTC
- Empty responses (HTML content-type) treated as error
- Supports HTTP conditional requests via If-Modified-Since
- Generation data includes imports as transmission flows

## OASIS API Endpoints

**Base URL:** `http://oasis.caiso.com/oasisapi/`
**API Documentation:** https://www.caiso.com/oasis/oasisapi/
**Data Format:** XML inside ZIP file
**Units:** $/MWh
**Timezone:** US/Pacific

### LMP - SP15 Hub (Day Ahead Hourly)
**URL:** `http://oasis.caiso.com/oasisapi/SingleZip?queryname=PRC_LMP&version=12&resultformat=6&market_run_id=DAM&node=TH_SP15_GEN-APND`

**Notes:** Day-ahead market LMP prices for SP15 trading hub; includes LMP, Energy (MCE), Congestion (MCC), and Loss (MCL) components

### LMP - SP15 Hub (Real-Time 15 Min)
**URL:** `http://oasis.caiso.com/oasisapi/SingleZip?queryname=PRC_RTPD_LMP&version=3&resultformat=6&market_run_id=RTPD&node=TH_SP15_GEN-APND`

**Notes:** Real-time pre-dispatch market LMP prices for SP15 trading hub; includes LMP, Energy, Congestion, Loss, and GHG components

### LMP - SP15 Hub (Real-Time 5 Min)
**URL:** `http://oasis.caiso.com/oasisapi/SingleZip?queryname=PRC_INTVL_LMP&version=3&resultformat=6&market_run_id=RTM&node=TH_SP15_GEN-APND`

**Notes:** Real-time dispatch interval LMP prices for SP15 trading hub; includes LMP, Energy, Congestion, Loss, and GHG components

**Notes:**
- Requires specific query parameters: `queryname`, `version`, `resultformat`, `market_run_id`, `node`
- Response format: XML inside ZIP file
- Implements rate limiting; recommended sleep between requests (5 seconds)
- SP15 hub represents Southern California prices (one of three primary trading hubs)
- Available trading hubs: NP15 (Northern), SP15 (Southern), ZP26 (Zonal)

## Daily Renewable Report (Curtailment Data)

**Data Portal:** https://www.caiso.com/outlook/
**URL Pattern:** `https://www.caiso.com/documents/daily-renewable-report-%b-%d-%Y.html`
**Data Format:** HTML with embedded JavaScript arrays
**Units:** MW (curtailment rate), MWh (curtailment energy)
**Resolution:** Hourly, Daily
**Availability:** Historical data available; latest typically previous day (published ~10 AM PT)

### Curtailment Endpoints

**Solar Curtailment Total (Hourly)**
- **JavaScript Variable:** `solar_curtailment_total_hourly`
- **Units:** MWh
- **Notes:** Total solar curtailment energy by hour

**Wind Curtailment Total (Hourly)**
- **JavaScript Variable:** `wind_curtailment_total_hourly`
- **Units:** MWh
- **Notes:** Total wind curtailment energy by hour

**Solar Curtailment Maximum (Hourly)**
- **JavaScript Variable:** `solar_curtailment_maximum_hourly`
- **Units:** MW
- **Notes:** Maximum solar curtailment rate by hour

**Wind Curtailment Maximum (Hourly)**
- **JavaScript Variable:** `wind_curtailment_maximum_hourly`
- **Units:** MW
- **Notes:** Maximum wind curtailment rate by hour

### Curtailment Types and Reasons

| Curtailment Type | Description |
|------------------|-------------|
| Economic Local | Curtailment due to local economic conditions |
| Economic System | Curtailment due to system-wide economic conditions |
| Self Scheduled | Curtailment due to self-scheduling |
| Operator Instruction | Curtailment due to operator dispatch instructions |

| Curtailment Reason | Description |
|--------------------|-------------|
| Local | Local transmission constraints |
| System | System-wide conditions |

### Related Data in Daily Renewable Report

| Data Type | Variable Prefix | Units | Description |
|-----------|-----------------|-------|-------------|
| Solar Generation (RTD) | `solar_generation_caiso_5_min` | MW | Real-time dispatch solar generation |
| Wind Generation (RTD) | `wind_generation_caiso_5_min` | MW | Real-time dispatch wind generation |
| Solar Curtailment (Economic) | `solar_curtailment_econ_*` | MW/MWh | Economic curtailment |
| Wind Curtailment (Economic) | `wind_curtailment_econ_*` | MW/MWh | Economic curtailment |
| Solar Curtailment (Self Scheduled) | `solar_curtailment_ss_*` | MW/MWh | Self-scheduled curtailment |
| Wind Curtailment (Self Scheduled) | `wind_curtailment_ss_*` | MW/MWh | Self-scheduled curtailment |
| Solar Curtailment (Operator) | `solar_curtailment_oi_*` | MW/MWh | Operator instruction curtailment |
| Wind Curtailment (Operator) | `wind_curtailment_oi_*` | MW/MWh | Operator instruction curtailment |

**Notes:**
- Data is extracted from HTML pages containing embedded JavaScript arrays
- Corrected reports available with `-corrected` suffix if data was revised
- Curtailment types include Economic (Local/System), Self Scheduled, and Operator Instruction
- Negative curtailment values may indicate over-generation conditions
- URL date format: `%b-%d-%Y` (e.g., `jan-15-2024`)

## Trading Hub Locations

| Location ID | Description |
|-------------|-------------|
| TH_NP15_GEN-APND | NP15 trading hub (Northern California) |
| TH_SP15_GEN-APND | SP15 trading hub (Southern California) |
| TH_ZP26_GEN-APND | ZP26 trading hub (Zonal) |

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/caiso.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/US_CA.py)
- [gridstatus.io](https://github.com/gridstatus/gridstatus/blob/main/gridstatus/caiso/caiso.py)
