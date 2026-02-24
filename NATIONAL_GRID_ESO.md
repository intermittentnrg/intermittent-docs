# National Grid ESO Data Source

**Note:** API endpoints stopped working. This documentation retained for reference.

**Quick Facts:**
- **Region:** Great Britain (England, Scotland, Wales) - `GB`
- **Website:** https://www.nationalgrideso.com/
- **Timezone:** Europe/London (UTC+0/+1 with DST)
- **Data Format:** CSV
- **Units:** MW
- **Resolution:** 30-minute settlement periods (1-50 per day)

## Endpoints (No Longer Working)

### Live Demand API
**Quick Facts:**
- **URL:** `https://api.neso.energy/api/3/action/datastore_search_sql`
- **Parameters:** SQL query against CKAN datastore

**Query:**
```sql
SELECT * FROM "177f6fa4-ae49-4182-81ea-0c6b35f26ca6" 
WHERE "SETTLEMENT_DATE" >= '{from}' 
AND "SETTLEMENT_DATE" <= '{now}' 
AND "FORECAST_ACTUAL_INDICATOR" = 'A'
```

### CSV Download
**Quick Facts:**
- **URL:** `https://api.nationalgrideso.com/dataset/7a12172a-939c-404c-b581-a6128b74f588/resource/177f6fa4-ae49-4182-81ea-0c6b35f26ca6/download/demanddataupdate.csv`

## Data Types

### Embedded Generation
- `wind_embedded`: Embedded wind generation
- `solar_embedded`: Embedded solar/PV generation
- `hydro_pumped_storage_charging`: Pumped storage pumping (negative value)

## Notes

- Settlement Period: 30-minute intervals (1-50 per day)
- Date formats: `%Y-%m-%d` (2024-01-15), `%d-%b-%Y` (15-Jan-2024)

## Alternatives

- ELEXON provides GB data
- ENTSO-E provides GB data

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/national_grid_eso.rb)
