# Hydro-Québec Data Source

**Note:** Implementation incomplete. Endpoint returns data but parsing needs completion.

**Quick Facts:**
- **Region:** Québec Province, Canada - `CA-QC`
- **Website:** https://www.hydroquebec.com/
- **Timezone:** America/Toronto (UTC-5/-4 with DST)
- **Data Format:** JSON (French field names)
- **Units:** MWh
- **Resolution:** Daily or hourly (uncertain)

## Endpoints

### Production Data
**Quick Facts:**
- **URL:** `https://www.hydroquebec.com/data/documents-donnees/donnees-ouvertes/json/production.json`
- **Notes:** JSON with French field names

**Response Format:**
```json
{
  "dateStart": "2024-01-15T00:00:00",
  "dateEnd": "2024-01-15T23:59:59",
  "details": [
    {
      "date": "2024-01-15T00:00:00",
      "valeurs": {
        "hydraulique": 1234.5,
        "thermique": 100.0,
        "solaire": 0.0,
        "eolien": 50.0,
        "autres": 25.0
      }
    }
  ]
}
```

## Production Type Mapping

| French | English | Production Type |
|--------|---------|----------------|
| hydraulique | hydraulic | hydro |
| thermique | thermal | thermal |
| solaire | solar | solar |
| eolien | wind | wind |
| autres | others | biomass |

## Notes

- Québec has massive hydroelectric generation (James Bay Project)
- Data frequency may be daily vs hourly

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/hydro_quebec.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/CA_QC.py)
