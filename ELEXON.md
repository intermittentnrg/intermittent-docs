# ELEXON Data Source

**Quick Facts:**
- **Region:** Great Britain (England, Scotland, Wales) - `GB`
- **Website:** https://bmrs.elexon.co.uk/api-documentation
- **Timezone:** UTC (all timestamps)
- **Data Format:** JSON
- **Units:** MW
- **Resolution:** 30-minute settlement periods, 5-minute unit-level
- **Availability:** 
  - Real-time (FUELINST)
  - Historical (AGPT, ATL): 7-day max range per request
  - Unit-level (B1610): 5 business days delayed

## Endpoints

### Fuel Instant (FUELINST) - Generation & Transmission
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/datasets/FUELINST`
- **Documentation:** https://bmrs.elexon.co.uk/api-documentation
- **Parameters:** `settlementDateFrom`/`settlementDateTo`: YYYY-MM-DD
- **Notes:** Real-time generation by fuel type and international transmission

```
Dataset,PublishTime,StartTime,SettlementDate,SettlementPeriod,FuelType,Generation
FUELINST,2023-07-19T23:00:00Z,2023-07-19T22:55:00Z,2023-07-19,48,BIOMASS,1902
```

**Interconnectors:**
- INTELE/INTELEC → FR (France)
- INTEW/INTGRNL/INTIRL → IE (Ireland)
- INTFR → FR (France)
- INTIFA2 → FR (France - IFA2)
- INTNED → NL (Netherlands)
- INTNEM → BE (Belgium)
- INTNSL → NO (Norway)
- INTVKL → DK (Denmark)

### Actual Generation Per Type (AGPT)
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/datasets/AGPT`
- **Parameters:** `publishDateTimeFrom`/`publishDateTimeTo`: YYYY-MM-DD HH:MM
- **Notes:** Historic generation per type for GB_B1620 area; 7-day maximum range

```
Dataset,DocumentId,DocumentRevisionNumber,PublishTime,BusinessType,PsrType,Quantity,StartTime,SettlementDate,SettlementPeriod
AGPT,NGET-EMFIP-AGPT-06417742,1,2023-01-01T23:59:09Z,Solar generation,Solar,1000.000,2023-01-01T22:30:00Z,2023-01-01,46
AGPT,NGET-EMFIP-AGPT-06417742,1,2023-01-01T23:59:09Z,Production,Wind,2000.000,2023-01-01T22:30:00Z,2023-01-01,46
```

### Actual Total Load (ATL)
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/demand/actual/total`
- **Parameters:** `from`/`to`: YYYY-MM-DD
- **Notes:** National electricity demand; 7-day maximum range

```
PublishTime,StartTime,SettlementDate,SettlementPeriod,Quantity
2023-07-19T01:55:08Z,2023-07-19T00:00:00Z,2023-07-19,3,19999.000
```

### Generation Unit Output (B1610)
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/datasets/B1610`
- **Parameters:** `settlementDate`: YYYY-MM-DD, `settlementPeriod`: 1-50
- **Notes:** Unit-level generation data; 5 business days delayed; iterate through all 50 settlement periods per day

```
Dataset,PsrType,BmUnit,NationalGridBmUnitId,SettlementDate,SettlementPeriod,HalfHourEndTime,Quantity
B1610,Generation,E_HYWDW-1,HYWDW-1,2023-09-01,20,09/01/2023 09:00:00,0.074
```

### Installed Generation Capacity (IGCA)
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/datasets/IGCA`
- **Resolution:** Yearly (P1Y)
- **Notes:** Yearly installed capacity per production type for GB_B1620

### Unit Capacity (IGCPU)
**Quick Facts:**
- **URL:** `https://data.elexon.co.uk/bmrs/api/v1/datasets/IGCPU`
- **Notes:** Unit-level installed capacity with commissioning/decommissioning dates

## Fuel Types

- BIOMASS: Biomass
- CCGT: Combined cycle gas turbine
- COAL: Coal
- NPSHYD: Hydro
- NUCLEAR: Nuclear
- OCGT: Open cycle gas turbine
- OIL: Oil
- OTHER: Other
- PS: Pumped storage
- WIND: Wind

## Notes
- Settlement periods: 30-minute intervals (1-50 per day)
- Timestamp format: `%Y-%m-%dT%H:%M:%SZ` (ISO 8601 UTC)
- Date format: `%Y-%m-%d`
- Datetime format: `%Y-%m-%d %H:%M`
- FUELINST provides both generation and transmission data
- B1610 unit data requires iterating through all 50 settlement periods per day

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/elexon.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/ELEXON.py)

