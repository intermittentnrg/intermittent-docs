# ONS Data Source

**Quick Facts:**
- **Region:** Brazil
  - `BR-NE` (Northeast), `BR-N` (North), `BR-CS` (Southeast/Central-West), `BR-S` (South)
- **Website:** https://www.ons.org.br/
- **Data Portal:** https://dados.ons.org.br/
- **Timezone:** Brazil has multiple timezones; timestamps include offset (`%:z` format)
- **Data Format:** JSON
- **Units:** MW
- **Resolution:** 1-minute
- **Availability:** 
  - Real-time data via AWS SQS queue consumption
  - Configured via `ONS_QUEUE_URL` env var (region: sa-east-1)

## Regions

| Code | Region | API Key |
|------|--------|---------|
| BR-NE | Northeast | nordeste |
| BR-N | North | norte |
| BR-CS | Southeast/Central-West | sudesteECentroOeste |
| BR-S | South | sul |

## Production Type Mapping

| JSON Key | Production Type | Notes |
|----------|----------------|-------|
| hidraulica | hydro | Includes Itaipu contributions |
| itaipu50HzBrasil | - | Added to hydro |
| itaipu60Hz | - | Added to hydro |
| termica | other | Thermal generation |
| eolica | wind | Wind |
| nuclear | nuclear | Nuclear |
| solar | solar | Solar |

## Transmission / Interchange

**International (from BR-S):**
- Argentina (AR)
- Paraguay (PY)
- Uruguay (UY)

**Inter-regional:**
- S-CS: BR-S ↔ BR-CS
- CS-NE: BR-CS ↔ BR-NE
- CS-N: BR-CS ↔ BR-N
- N-NE: BR-N ↔ BR-NE

## Notes

- Time format: `%Y-%m-%dT%H:%M:%S%:z` (ISO 8601 with timezone offset)
- Itaipu hydro plant contributes to both 50Hz (Brazil) and 60Hz systems
- Inter-regional flows use "sudeste_norteFic" for CS-N (North via Fictitious Exchange)

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/ons.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/ONS.py)
