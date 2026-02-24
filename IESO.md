# IESO Data Source

**Quick Facts:**
- **Region:** Ontario, Canada - `CA-ON`
- **Website:** https://www.ieso.ca/
- **Data Portal:** https://reports-public.ieso.ca/public/
- **Timezone:** America/Toronto (UTC-5/-4 with DST)
- **Data Format:** CSV/XML
- **Units:** MW (generation, price, intertie), kW (load - note: different unit)
- **Resolution:** 5-minute (real-time), hourly (historical)
- **Availability:** Real-time and historical; real-time files available daily, historical yearly CSVs

## Endpoints

### Real-time Load
**Quick Facts:**
- **URL:** `https://reports-public.ieso.ca/public/RealtimeConstTotals/`
- **Units:** kW
- **Resolution:** 5-minute
- **Notes:**
  - Directory listing with CSV files: `PUB_RealtimeConstTotals_YYYYMMDD.csv`
  - Hour: 1-24 (converted to 0-23)
  - Period: 1-12 (5-min periods within hour, converted to minutes)
  - Column 2: Market Demand (kW)

### Historical Load (Yearly)
**Quick Facts:**
- **URL:** `https://reports-public.ieso.ca/public/Demand/PUB_Demand_%Y.csv`
- **Resolution:** Hourly

### Generation Unit Output (Daily XML)
**Quick Facts:**
- **URL:** `https://reports-public.ieso.ca/public/GenOutputCapability/`
- **Notes:** XML files: `PUB_GenOutputCapability_%Y%m%d.xml`; per-unit generation by fuel type

### Generation Unit Output (Monthly CSV)
**Quick Facts:**
- **URL:** `https://reports-public.ieso.ca/public/GenOutputCapabilityMonth/PUB_GenOutputCapabilityMonth_%Y%m.csv`
- **Resolution:** Hourly

### Generation by Fuel (Yearly XML)
**Quick Facts:**
- **URL:** `https://reports-public.ieso.ca/public/GenOutputbyFuelHourly/PUB_GenOutputbyFuelHourly_%Y.xml`
- **Notes:** Aggregated generation per fuel type

### Price (HOEP) - Daily
**Quick Facts:**
- **URL:** `https://reports-public.ieso.ca/public/DispUnconsHOEP/`
- **Units:** CAD $/MWh
- **Resolution:** Hourly

### Price (HOEP) - Yearly
**Quick Facts:**
- **URL:** `https://reports-public.ieso.ca/public/PriceHOEPPredispOR/PUB_PriceHOEPPredispOR_%Y.csv`

### Intertie Flows (Daily)
**Quick Facts:**
- **URL:** `https://reports-public.ieso.ca/public/IntertieScheduleFlow/PUB_IntertieScheduleFlow_%Y%m%d.xml`
- **Resolution:** 5-minute
- **Notes:** 
  - MANITOBA / MANITOBA SK → CA-ON ↔ CA-MB
  - MICHIGAN / MINNESOTA → CA-ON ↔ US-MISO
  - NEW-YORK → CA-ON ↔ US-NYISO
  - PQ.* (various) → CA-ON ↔ CA-QC

### Intertie Flows (Yearly CSV)
**Quick Facts:**
- **URL:** `https://reports-public.ieso.ca/public/IntertieScheduleFlowYear/PUB_IntertieScheduleFlowYear_%Y.csv`

## Production Type Mapping

| IESO Code | Production Type |
|-----------|----------------|
| NUCLEAR | nuclear |
| GAS | fossil_gas |
| HYDRO | hydro |
| WIND | wind_onshore |
| SOLAR | solar |
| BIOFUEL | biomass |
| OTHER | other |

## Notes
- Hours are 1-indexed (1-24), converted to 0-23
- Periods are 1-indexed within hour
- XML intervals: 1-12 (5-min each)
- Load is in kW (not MW like other sources)
- Intertie: MW (negative value convention)
- HTTP retry for 500/502 errors
- Directory listings parsed for file discovery
- XML parsed via Ox library

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/ieso.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/CA_ON.py)
- [gridstatus.io](https://github.com/gridstatus/gridstatus/blob/main/gridstatus/ieso.py)
