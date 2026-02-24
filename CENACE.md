# CENACE Data Source

**Quick Facts:**
- **Region:** Mexico - `MX`
- **Website:** https://www.cenace.gob.mx/Paginas/SIM/Reportes/EnergiaGeneradaTipoTec.aspx
- **Timezone:** America/Mexico_City (UTC-6, no DST observance)
- **Data Format:** CSV
- **Units:** MW
- **Resolution:** Hourly
- **Availability:** 
  - Available from 2016-04-01 onwards
  - Monthly granularity only
  - ASP.NET form submission required

## Endpoints

### Monthly Generation Data
**Quick Facts:**
- **URL:** `https://www.cenace.gob.mx/Paginas/SIM/Reportes/EnergiaGeneradaTipoTec.aspx`
- **Notes:** 
  - Monthly generation data via ASP.NET form submission
  - Form requirements: VIEWSTATE, VIEWSTATEGENERATOR, EVENTVALIDATION tokens, Date picker with client state, CSV download button click (image button submission)
  - ASP.NET AJAX partial postbacks for historical dates
  - Month/year extracted from table header text

**CSV Format:**
- 8 header rows
- Date: `%d/%m/%Y`
- Hour: 1-24 (1-indexed, converted to 0-23)
- Production types (columns 3-13)

## Production Type Mapping

| Column | Production Type |
|--------|----------------|
| 3 | wind |
| 4 | solar |
| 5 | biomass |
| 6 | fossil_coal |
| 7 | fossil_gas_ccgt |
| 8 | fossil_oil_diesel |
| 9 | geothermal |
| 10 | hydro |
| 11 | nuclear |
| 12 | thermal |
| 13 | fossil_gas |

## Notes

- Hours > 23 skipped (bad data filtering)
- Mexico City doesn't observe DST - simple offset conversion
- Spanish month names parsed (Enero-Diciembre)

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/cenace.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/CENACE.py)
