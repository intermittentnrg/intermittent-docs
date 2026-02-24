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
  - 8 header rows
  - Date: `%d/%m/%Y`
  - Hour: 1-24 (1-indexed, converted to 0-23)
  - Header rows have CR (`\r`) inside quoted strings, LF (`\n`) line endings
  - **Settlement Versions:** The page displays multiple settlement versions/rows in an HTML table (column "No. de Liquidación Asociada"). The CSV header shows settlement types:
    - **L0**: Original (Original)
    - **L1**: Re-Liquidacion Inicial (Initial Re-Settlement)
    - **L2**: Re-Liquidacion Intermedia (Intermediate Re-Settlement)
    - **L3**: Re-Liquidacion Final (Final Re-Settlement)
    - **L4**: Re-Liquidacion por Controversia 4 (Re-Settlement by Controversy 4)
    - **L5**: Re-Liquidacion por Controversia 5 (Re-Settlement by Controversy 5)
    - The importer downloads the latest settlement via `buttons.last` CSS selector
- **Columns:**
  - Sistema
  - Dia
  - Hora
  - Eolica
  - Fotovoltaica
  - Biomasa
  - Carboelectrica
  - Ciclo Combinado
  - Combustion Interna
  - Geotermoelectrica
  - Hidroelectrica
  - Nucleoelectrica
  - Termica Convencional
  - Turbo Gas

```
"Centro Nacional de Control de Energia\r"
"Estadistica de la Energia Generada Liquidada Agregada (MWh) Intermitente y Firme por Tipo de Tecnologia\r"
"Sistema Electrico Nacional\r"
"Dias de Operacion del Mes de: noviembre 2025\r"
"Proceso de Liquidacion: Re-Liquidacion Inicial (L1) \r"
"Archivo descargado desde el Sistema de Informacion del Mercado (Area Publica) creado el 25/ene/2026 05:05:01 hrs.\r"
"Nota: Los acentos de este reporte se omiten intencionalmente por sistema."
"Sistema"," Dia"," Hora"," Eolica"," Fotovoltaica","  Biomasa"," Carboelectrica"," Ciclo Combinado"," Combustion Interna"," Geotermoelectrica"," Hidroelectrica"," Nucleoelectrica"," Termica Convencional"," Turbo Gas"
"SEN","01/11/2025","1","3044.9291","0.0424","2.4439","740.3315","24417.7417","331.4234","378.6465","3643.7015","754.9493","1695.7735","1140.0202"
```

## Notes

- Hours > 23 skipped (bad data filtering)
- Mexico City doesn't observe DST - simple offset conversion
- Spanish month names parsed (Enero-Diciembre)

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/cenace.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/CENACE.py)
