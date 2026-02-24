# EirGrid

**Quick Facts:**
- **Region:** Ireland (All-island) - `IE`
- **Website:** https://www.smartgriddashboard.com/
- **Data Portal:** https://www.smartgriddashboard.com/
- **API Documentation:** SEM-O API https://reports.sem-o.com/
- **Timezone:** Europe/Dublin (UTC+0/+1 with DST)
- **Data Format:** CSV, JSON
- **Units:** MW, €/MWh
- **Resolution:** 30-minute
- **Availability:** Historical from 2022, real-time with 24-hour delay

## Endpoints

### EirGrid Dashboard CSV Service
**Quick Facts:**
- **URL:** https://www.smartgriddashboard.com/DashboardService.svc/csv
- **Data Portal:** https://www.smartgriddashboard.com/
- **Units:** MW
- **Resolution:** 30-minute
- **Notes:** Returns CSV files for previous day

**Available CSV Types:**
| Data Type | Area Parameter | Description |
|-----------|----------------|-------------|
| demand | demandActual | System demand |
| wind | windActual | Wind generation |
| interconnection | interconnection | Net interconnector flow |
| generation | generationActual | Total generation |

**Parameters:**
- `area`: See table above
- `region`: ALL
- `datefrom`: `%d-%b-%Y %H:%M` (e.g., "23-Feb-2025 00:00")
- `dateto`: `%d-%b-%Y %H:%M` (e.g., "23-Feb-2025 23:59")

### SEM-O Price API
**Quick Facts:**
- **URL:** https://reports.sem-o.com/api/v1/dynamic/BM-026
- **Documentation:** https://reports.sem-o.com/
- **Units:** €/MWh
- **Resolution:** 30-minute
- **Notes:** Returns imbalance settlement prices

**Parameters:**
- `StartTime`: `>=%Y-%m-%dT%H:%M` (e.g., ">=2025-02-23T00:00")
- `EndTime`: `<=%Y-%m-%dT%H:%M`
- `page_size`: 500

## Production Type Mapping

| Source Field | Production Type | Notes |
|--------------|----------------|-------|
| WIND(MW) | wind_onshore | From CSV data |
| GENERATION(MW) | total_generation | From CSV data |
| ACTUAL DEMAND(MW) | demand | From CSV data |
| Net Total (MW) | interconnection | Positive = imports, negative = exports |

## Notes

**Data Processing:**
- Fossil fuel generation cannot be reliably calculated without hydro data
- Hydro and solar power data not available through primary EirGrid/SEM-O endpoints
- Total generation includes wind, fossil fuels, hydro, and other renewables

**Time Format:**
- CSV files: `%d-%b-%Y %H:%M` (e.g., "23-Feb-2025 00:00")
- SEM-O API: `%Y-%m-%dT%H:%M` (ISO format)
- All times in local timezone (Europe/Dublin)

**Data Limitations:**
- CSV data only available for previous day (no real-time access)
- No direct solar data source through these endpoints
- Price data from SEM-O has settlement delays

**Regional Coverage:**
- All-island data includes Republic of Ireland and Northern Ireland
- Interconnector flows show net imports/exports with Great Britain

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/eirgrid.rb)