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

## Production Type Mapping

| EIA Code | Production Type |
|----------|----------------|
| BAT | battery |
| COL | fossil_hard_coal |
| GEO | geothermal |
| NG | fossil_gas |
| NUC | nuclear |
| OIL | fossil_oil |
| OES | storage |
| OTH | other |
| PS | hydro_pumped_storage |
| SNB | solar_with_battery |
| SUN | solar |
| UES | unknown_storage |
| WAT | hydro |
| WND | wind |
| WNB | wind_with_battery |
| UNK | unknown |

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
