# CAMMESA Data Source

**Quick Facts:**
- **Region:** Argentina - `AR`
- **Website:** https://cammesaweb.cammesa.com/generacion-real/
- **Timezone:** America/Argentina/Buenos_Aires (UTC-3, no DST)
- **Data Format:** JSON/CSV (ZIP)
- **Units:** MW
- **Resolution:** Hourly
- **Availability:** Real-time and historical

## Endpoints

### Renewable Generation (Renovables)
**Quick Facts:**
- **URL:** `https://cdsrenovables.cammesa.com/exhisto/RenovablesService/GetChartTotalTRDataSource/`
- **Parameters:** `desde`: DD-MM-YYYY, `hasta`: DD-MM-YYYY
- **Notes:** JSON response with real-time renewables

### Daily Programming (ProgramacionDiaria)
**Quick Facts:**
- **Lookup URL:** `https://api.cammesa.com/pub-svc/public/findDocumentosByNemoRango`
- **Download URL:** `https://api.cammesa.com/pub-svc/public/findAttachmentByNemoId`
- **Data Format:** CSV (ZIP file containing `BALANCE.csv` and `VALORES_GENERADORES.csv` - only BALANCE.csv is currently processed)
- **Release Schedule:** Daily around 20:00 ART (GMT-3)
- **Notes:**
  - Two-step process: lookup then download
  - CSV format: TIPO, RGE, VARIABLE columns, H01-H24 hourly values
  - ZIP files: `PD%y%m%d.zip` (e.g., `PD260222.zip` = Feb 22, 2026)
  - UTF-8 BOM handling for CSV

#### Document Lookup API Response

The lookup endpoint returns an array of document metadata:

```json
[{
  "id": "763EA55FD024635403258DA5007E582F",
  "fecha": "21/02/2026",
  "nemo": "PROGRAMACION_DIARIA",
  "titulo": "Programacion diaria",
  "comentario": "",
  "hora": "20:00",
  "adjuntos": [{
    "id": "PD260222.zip",
    "campo": "$File",
    "nombre": "PD260222.zip"
  }],
  "version": "2026-02-21T20:00:00.000-03:00"
}]
```

**Field Meanings:**

| Field | Description |
|-------|-------------|
| `id` | Document unique identifier |
| `fecha` | Publication date (DD/MM/YYYY) |
| `nemo` | Document type: `PROGRAMACION_DIARIA` = daily programming |
| `titulo` | Document title |
| `comentario` | Comments (usually empty) |
| `hora` | Publication time (HH:MM, typically 20:00) |
| `adjuntos` | Array of attached files |
| `adjuntos[].id` | Filename (`PDYYMMDD.zip`) |
| `adjuntos[].campo` | Field type: `$File` = file attachment |
| `adjuntos[].nombre` | Full filename |
| `version` | **Document publication timestamp** (ISO 8601 with GMT-3). Indicates when this daily programming file was published by Cammesa. |

#### BALANCE.csv Format
- TIPO, RGE, VARIABLE columns
- H01-H24 hourly values
- Multiple region rows

```
TIPO,RGE,VARIABLE,H01,H02,H03,H04,H05,H06,H07,H08,H09,H10,H11,H12,H13,H14,H15,H16,H17,H18,H19,H20,H21,H22,H23,H24
D,BAS,Demanda Neta,1911,1829,1799,1762,1788,1732,1818,1948,2071,2135,2205,2173,2167,2182,2125,2072,2087,2097,2135,2315,2355,2295,2180,2061
```

### BALANCE.csv Codes

- Nuclear: Nuclear generation
- Termica: Thermal generation
- Ren Hidro >50MW: Hydro >50MW
- Ren ley 26190: Hydro renewable
- Importacion: Imports
- Exportacion: Exports
- Demanda Neta: Net demand

#### VALORES_GENERADORES.csv Format
- Unit-level generation data
- Columns: Region, Agent, Unit, Type, H01-H24 hourly values
- Headers removed, quotes may be present in fields

### Unit-Level Type Codes

- EO: Wind
- BG: Biomass
- TV, HR, HI: Hydro
- NU: Nuclear
- DI, TG, CC: Thermal
- FV: Solar

## Rate Limiting

**Warning:** The ProgramacionDiaria API may block IPs that poll too frequently. The `version` field in the response can be used to determine if a new file has been published since the last check, avoiding unnecessary re-downloads of unchanged data.

## Notes

- Time format: API `%d-%m-%Y`, CSV date + hour index (0-23), Timestamp `%Y-%m-%dT%H:%M:%S.%L%z`
- Imports/exports to/from "other" (unspecified)
- Timezone: America/Sao_Paulo (GMT-3, no DST) - all times converted to UTC for storage

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/cammesa.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/CAMMESA.py)
