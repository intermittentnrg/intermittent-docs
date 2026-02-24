# AEMO WEM Data Source

**Quick Facts:**
- **Region:** Western Australia (SWIS: South West Interconnected System) - `WEM`
- **Website:** https://aemo.com.au/
- **Data Portal:** https://data.wa.aemo.com.au
- **Timezone:** Etc/GMT-8 (AWST, UTC+8, no DST)
- **Data Format:** CSV/JSON
- **Units:** MWh per interval (generation), $/MWh (price)
- **Resolution:** 30-minute (pre-reform), 5-minute (post-reform, 2023+)
- **Availability:** 
  - Pre-reform: Balancing market with 30-minute settlement
  - Post-reform: Wholesale Electricity Market Design (WEMDE) with 5-minute dispatch
  - Real-time and historical

## Endpoints

### Facility SCADA (Post-reform)
**Quick Facts:**
- **URL:** `https://data.wa.aemo.com.au/public/public-data/datafiles/facility-scada/`
- **Resolution:** 30-minute
- **Notes:** Monthly CSV files `facility-scada-%Y-%m.csv`; columns: Trading Date, Interval Number, Trading Interval, Participant Code, Facility Code, Energy Generated (MWh)

### Facility SCADA JSON (Daily)
**Quick Facts:**
- **URL:** `http://data.wa.aemo.com.au/public/market-data/wemde/facilityScada/previous/`
- **Resolution:** 5-minute
- **Units:** MWh per interval
- **Notes:** Post-reform format (2023+); JSON structure: `facilityScadaDispatchIntervals` array with `dispatchInterval` (ISO timestamp), `code` (facility identifier), `quantity` (MWh)

### Operational Demand (Daily JSON)
**Quick Facts:**
- **URL:** `http://data.wa.aemo.com.au/public/market-data/wemde/operationalDemandWithdrawal/dailyFiles/`
- **Notes:** Real-time operational demand; JSON structure: `dispatchInterval` (ISO timestamp), `operationalDemand` (MW)

### Reference Trading Price (Daily JSON)
**Quick Facts:**
- **URL:** `http://data.wa.aemo.com.au/public/market-data/wemde/referenceTradingPrice/previous/`
- **Units:** $/MWh
- **Notes:** Trading prices post-reform

### Live Balancing (Real-time CSV)
**Quick Facts:**
- **URL:** `https://wa.aemo.com.au/aemo/data/wa/infographic/distributed-pv_opdemand/distributed-pv_opdemand.csv`
- **Notes:** Single CSV with latest data; columns: Trading Interval, Estimated DPV Generation, Operational Demand

### Balancing Summary (Pre-reform)
**Quick Facts:**
- **URL:** `https://data.wa.aemo.com.au/datafiles/balancing-summary/`
- **Resolution:** 30-minute
- **Units:** $/MWh (price)
- **Notes:** Pre-2023 market reform data; columns: Trading Date, Interval Number, Trading Interval, Load Forecast, Forecast As At, Scheduled Generation, Non-Scheduled Generation, Total Generation, Final Price

### Distributed PV (Archive)
**Quick Facts:**
- **URL:** `https://data.wa.aemo.com.au/public/public-data/datafiles/distributed-pv/`
- **Resolution:** 30-minute
- **Notes:** Annual CSV with estimated DPV generation

## Notes
- CSV time format: `%Y-%m-%d %H:%M:%S`
- JSON time format: `%Y-%m-%dT%H:%M:%S%:z` (ISO 8601 with offset)
- Filename format: `%Y-%m-%d` or `%Y%m%d`
- Timezone conversion: AWST (+8) to UTC
- Different parsers handle pre-reform and post-reform data formats
- Negative values for: battery charging, pumped storage charging

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/aemo_wem.rb)
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/aemo_wem_archive.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/OPENNEM.py)
