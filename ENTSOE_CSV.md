# ENTSO-E CSV Data Source

**Quick Facts:**
- **Region:** European Union + associated countries (35+ bidding zones)
- **Website:** https://transparency.entsoe.eu/
- **Data Portal:** https://fms.tp.entsoe.eu
- **API Documentation:** https://transparency.entsoe.eu/api-documentation
- **Timezone:** UTC (all timestamps)
- **Data Format:** CSV (tab-separated), optionally ZIP compressed
- **Units:** MW, €/MWh (prices, stored as cents/MWh, ×100)
- **Resolution:** Hourly or 15-minute
- **Availability:**
  - Monthly CSV files
  - Files follow naming pattern: `YYYY_MM_<description>.csv`
  - Download via FMS File Management System

## Endpoints

### Aggregated Generation per Type
**Quick Facts:**
- **FMS Directory:** `/TP_export/AggregatedGenerationPerType_16.1.B_C_r3/`
- **Filename Pattern:** `YYYY_MM_AggregatedGenerationPerType_16.1.B_C_r3.csv`
- **Time Format:** `%Y-%m-%d %H:%M:%S`
- **Columns:**
  - DateTime(UTC)
  - ResolutionCode
  - AreaCode
  - AreaDisplayName
  - AreaTypeCode
  - AreaMapCode
  - ProductionType
  - ActualGenerationOutput[MW]
  - ActualConsumption[MW]
  - UpdateTime(UTC)
- **Notes:** Skip rows with AreaTypeCode 'CTA'

```
DateTime(UTC)	ResolutionCode	AreaCode	AreaDisplayName	AreaTypeCode	AreaMapCode	ProductionType	ActualGenerationOutput[MW]	ActualConsumption[MW]	UpdateTime(UTC)
2026-02-01 00:00:00	PT15M	10YAT-APG------L	Austria (AT)	BZN/CTA/CTY	AT	Biomass	248.000000	0.000000	2026-02-05 10:48:37
```

### Actual Generation Output per Generation Unit
**Quick Facts:**
- **FMS Directory:** `/TP_export/ActualGenerationOutputPerGenerationUnit_16.1.A_r3/`
- **Filename Pattern:** `YYYY_MM_ActualGenerationOutputPerGenerationUnit_16.1.A_r3.csv`
- **Time Format:** `%Y-%m-%d %H:%M:%S`
- **Columns:**
  - DateTime(UTC)
  - ResolutionCode
  - AreaCode
  - AreaDisplayName
  - AreaTypeCode
  - AreaMapCode
  - GenerationUnitCode
  - GenerationUnitName
  - GenerationUnitType
  - ActualGenerationOutput[MW]
  - ActualConsumption[MW]
  - UpdateTime(UTC)
- **Notes:**
  - Unit-level data
  - Area code overrides: DE_Amprion/DE_TenneT_GER/DE_TransnetBW/DE_50HzT → DE, NIE → GB, UA_IPS/UA_BEI → UA

```
DateTime(UTC)	ResolutionCode	AreaCode	AreaDisplayName	AreaTypeCode	AreaMapCode	GenerationUnitCode	GenerationUnitName	GenerationUnitType	ActualGenerationOutput[MW]	ActualConsumption[MW]	UpdateTime(UTC)
2015-01-04 23:00:00	PT60M	10YAT-APG------L	Austria (AT)	BZN/CTA	AT	14W-BLOCK07-L--J	Block 07 Linz	Fossil Gas	107.4		2025-08-06 15:07:58
```

### Actual Total Load
**Quick Facts:**
- **FMS Directory:** `/TP_export/ActualTotalLoad_6.1.A_r3/`
- **Filename Pattern:** `YYYY_MM_ActualTotalLoad_6.1.A_r3.csv`
- **Time Format:** `%Y-%m-%d %H:%M:%S`
- **Columns:**
  - DateTime(UTC)
  - ResolutionCode
  - AreaCode
  - AreaDisplayName
  - AreaTypeCode
  - AreaMapCode
  - TotalLoad[MW]
  - UpdateTime(UTC)
- **Notes:** Skip rows with AreaTypeCode 'CTA'

```
DateTime(UTC)	ResolutionCode	AreaCode	AreaDisplayName	AreaTypeCode	AreaMapCode	TotalLoad[MW]	UpdateTime(UTC)
2025-11-01 00:00:00	PT15M	10YAL-KESH-----5	Albania (AL)	BZN/CTA/CTY	AL	470.0	2025-11-10 10:04:10
```

### Energy Prices
**Quick Facts:**
- **FMS Directory:** `/TP_export/EnergyPrices_12.1.D_r3/`
- **Filename Pattern:** `YYYY_MM_EnergyPrices_12.1.D_r3.csv`
- **Time Format:** `%Y-%m-%d %H:%M:%S`
- **Units:** €/MWh (converted to cents/MWh, ×100)
- **Columns:**
  - InstanceCode
  - DateTime(UTC)
  - ResolutionCode
  - AreaCode
  - AreaDisplayName
  - AreaTypeCode
  - MapCode
  - ContractType
  - Sequence
  - Price[Currency/MWh]
  - Currency
  - UpdateTime(UTC)
- **Notes:** Filter by ContractType='Day-ahead' and Sequence blank or '1'

```
InstanceCode	DateTime(UTC)	ResolutionCode	AreaCode	AreaDisplayName	AreaTypeCode	MapCode	ContractType	Sequence	Price[Currency/MWh]	Currency	UpdateTime(UTC)
242e8d60a55556121f162035f554fa24	2025-10-01 00:00:00	PT15M	10YAT-APG------L	Austria (AT)	BZN	AT	Day-ahead	1	97.05	EUR	2025-09-30 11:41:39
```

### Physical Flows
**Quick Facts:**
- **FMS Directory:** `/TP_export/PhysicalFlows_12.1.G_r3/`
- **Filename Pattern:** `YYYY_MM_PhysicalFlows_12.1.G_r3.csv`
- **Time Format:** `%Y-%m-%d %H:%M:%S`
- **Columns:**
  - DateTime(UTC)
  - ResolutionCode
  - OutAreaCode
  - OutAreaDisplayName
  - OutAreaTypeCode
  - OutAreaMapCode
  - InAreaCode
  - InAreaDisplayName
  - InAreaTypeCode
  - InAreaMapCode
  - Flow[MW]
  - UpdateTime(UTC)
- **Notes:**
  - Skip rows with OutAreaTypeCode 'CTA' or InAreaTypeCode 'CTA'
  - Area type mapping: BZN/CTA/CTY → country, BZN → zone, CTY → country

```
DateTime(UTC)	ResolutionCode	OutAreaCode	OutAreaDisplayName	OutAreaTypeCode	OutAreaMapCode	InAreaCode	InAreaDisplayName	InAreaTypeCode	InAreaMapCode	Flow[MW]	UpdateTime(UTC)
2025-10-01 00:00:00	PT60M	10YAL-KESH-----5	Albania (AL)	BZN/CTA/CTY	AL	10YGR-HTSO-----Y	Greece (GR)	BZN/CTA/CTY	GR	61.0	2025-10-09 12:03:40
```

### Installed Capacity (Production Units)
**Quick Facts:**
- **FMS Directory:** `/TP_export/InstalledCapacityProductionUnit_14.1.B/`
- **Time Format:** `%Y-%m-%d %H:%M:%S.%L`
- **Columns:**
  - EICCode
  - Name
  - ValidFrom
  - ValidTo
  - Status
  - Type
  - Location
  - InstalledCapacity
  - ControlArea
  - BiddingZone
  - Voltage
- **Notes:** 
  - EIC Type Code = Resource Object W; map found at https://www.entsoe.eu/data/energy-identification-codes-eic/eic-approved-codes/
  - Data quality issues: Reported peak outputs vary widely (50%-200% of installed capacity) between countries

## Authentication

FMS (File Management System) requires OAuth2 authentication:
- OAuth2 endpoint: `https://keycloak.tp.entsoe.eu/realms/tp/protocol/openid-connect/token`
- Client ID: `tp-fms-public`
- Token refresh handled automatically; token cached until expiry

## Notes

- CSV files are tab-separated
- Files may be ZIP compressed
- Duplicate detection by filename and timestamp
- Area code mapping for imports (DE_Amprion → DE, NIE → GB, etc.)

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/entsoe_csv.rb)
