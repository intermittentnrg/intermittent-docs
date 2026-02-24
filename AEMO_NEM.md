# AEMO NEM Data Source

**Quick Facts:**

- **Region:** Eastern Australia (Queensland, NSW, Victoria, South Australia, Tasmania)
  - `QLD1` → Queensland, `NSW1` → New South Wales, `VIC1` → Victoria, `SA1` → South Australia, `TAS1` → Tasmania
- **Website:** https://aemo.com.au/
- **Data Portal:** https://nemweb.com.au
- **Timezone:** Etc/GMT-10 (AEST, UTC+10, no DST)
- **Data Format:** CSV
- **Units:** MW (generation, load, transmission), $/MWh (price)
- **Resolution:** 5-minute (real-time), 30-minute (historical)
- **Availability:**
  - Current Reports: Real-time, 5-minute intervals
  - MMS Historical: Monthly, SQLLoader format

## Endpoints

### Trading Prices
**Quick Facts:**
- **URL:** `https://nemweb.com.au/Reports/Current/TradingIS_Reports/`
- **Units:** $/MWh
- **Resolution:** 5-minute
- **Notes:** RRP (Regional Reference Price) per region; files: `PUBLIC_TRADINGIS_%Y%m%d%H%M_`

### Dispatch (Load & Transmission)
**Quick Facts:**
- **URL:** `https://nemweb.com.au/Reports/Current/DispatchIS_Reports/`
- **Resolution:** 5-minute
- **Notes:**
  - REGIONSUM: Total demand per region
  - INTERCONNECTORRES: Inter-regional flows
  - Files: `PUBLIC_DISPATCHIS_YYYYMMDDhhmm_`
  - Interconnector mappings: NSW1-QLD1/N-Q-MNSP1 (NSW1↔QLD1), VIC1-NSW1 (VIC1↔NSW1), V-SA/V-S-MNSP1 (VIC1↔SA1), T-V-MNSP1 (TAS1↔VIC1)

### Unit SCADA
**Quick Facts:**
- **URL:** `https://nemweb.com.au/Reports/Current/Dispatch_SCADA/`
- **Resolution:** 5-minute
- **Notes:** Per-unit generation (DUID - Dispatchable Unit ID); files: `PUBLIC_DISPATCHSCADA_YYYYMMDDhhmm_`

### Rooftop PV
**Quick Facts:**
- **URL:** `https://nemweb.com.au/Reports/Current/ROOFTOP_PV/ACTUAL/`
- **Resolution:** 5-minute
- **Notes:** Actual measurements per state; files: `PUBLIC_ROOFTOP_PV_ACTUAL_MEASUREMENT_`

### MMS Historical Data (Monthly)
**Quick Facts:**
- **URL:** `https://nemweb.com.au/Data_Archive/Wholesale_Electricity/MMSDM/%Y/MMSDM_%Y_%m/MMSDM_Historical_Data_SQLLoader/DATA/`
- **Resolution:** 30-minute
- **Notes:**
  - SQLLoader format
  - Files: `PUBLIC_DVD_TRADINGPRICE_%Y%m010000.zip`, `PUBLIC_DVD_DISPATCHREGIONSUM_%Y%m010000.zip`, `PUBLIC_DVD_DISPATCHINTERCONNECTORRES_%Y%m010000.zip`, `PUBLIC_DVD_DISPATCH_UNIT_SCADA_%Y%m010000.zip`, `PUBLIC_DVD_DUDETAIL_%Y%m010000.zip`, `PUBLIC_DVD_ROOFTOP_PV_ACTUAL_%Y%m010000.zip`

## Notes
- CSV format: Separator comma, Row separator `\r\n` (Windows), Header C/RECORDTYPE/SUBTYPE/VERSION, Data rows start with D, Time format `%Y/%m/%d %H:%M:%S`
- Filename format: `%Y%m%d%H%M` (12 digits)
- Timezone conversion: GMT+10 to UTC
- Transmission: MW (negative sign convention for flow direction)
- Pump storage and battery charging have negative values (negate values for `hydro_pumped_storage` and `battery_charging`)

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/aemo_nem.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/AEMO.py)
