# EIA Bulk Data Source

**Quick Facts:**
- **Region:** United States - Regional balancing authorities
  - Balancing Authority Codes: US48, CISO, SW, ERCOT, etc.
- **Website:** https://www.eia.gov/
- **Data Portal:** https://www.eia.gov/opendata/v1/bulkfiles.php
- **Timezone:** UTC (all timestamps)
- **Data Format:** Line-delimited JSON (JSONL/NDJSON), optionally ZIP compressed
- **Units:** MW (generation, demand, interchange)
- **Resolution:** Hourly
- **Availability:** Historical bulk downloads

## Series ID Format

`EBA.{from_area}-{to_area}.{type}.{subtype}.{timezone}`

### Components:
- `EBA`: Electricity Bulk Archive prefix
- Area codes: Balancing authority codes (e.g., US48, CISO, SW, ERCOT)
- Type codes:
  - `NG`: Net Generation
  - `D`: Demand
  - `ID`: Interchange (flow between areas)
- Subtype: Fuel type for generation (SUN, WND, NG, etc.)
- Timezone: `H` for hourly

### Examples:
- `EBA.US48-ALL.NG.H`: US48 total net generation
- `EBA.CISO-ALL.NG.SUN.H`: California ISO solar generation
- `EBA.SW-ALL.D.H`: Southwest demand
- `EBA.CISO-AZPS.ID.H`: Flow from CAISO to Arizona Public Service

### Fuel Type Codes

- BAT: Battery
- COL: Coal
- GEO: Geothermal
- NG: Natural gas
- NUC: Nuclear
- OIL: Oil
- OES: Energy storage
- OTH: Other
- PS: Pumped storage
- SNB: Solar with battery
- SUN: Solar
- UES: Unknown storage
- WAT: Water (hydro)
- WND: Wind
- WNB: Wind with battery
- UNK: Unknown

## Data Types

### Generation
**Quick Facts:**
- **Series Pattern:** `EBA.{area}-ALL.NG.{fuel}.H`
- **Units:** MW

### Demand
**Quick Facts:**
- **Series Pattern:** `EBA.{area}-ALL.D.H`
- **Units:** MW

### Interchange
**Quick Facts:**
- **Series Pattern:** `EBA.{from_area}-{to_area}.ID.H`
- **Units:** MW (with negative value convention for exports)
- **Notes:** Values are inverted (export measured as drain)

## Notes

- Time format input: `YYYYMMDDHH` (e.g., 2024011514)
- Hour beginning convention - subtract 1 hour for interval end

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/eia_bulk.rb)
