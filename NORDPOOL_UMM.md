# Nord Pool UMM (Urgent Market Messages) Data Source

**Quick Facts:**
- **Region:** Europe - Multiple bidding zones (Nordic, Baltic, UK, Germany, France, etc.)
- **Website:** https://www.nordpoolgroup.com/
- **API:** `https://ummapi.nordpoolgroup.com/messages`
- **Timezone:** Multiple (depends on bidding zone)
- **Data Format:** JSON
- **Units:** MW (capacity)
- **Resolution:** Event-based (outage periods)
- **Availability:** Real-time UMM messages
- **Authentication:** None required (public API)

## API Endpoint

```
GET https://ummapi.nordpoolgroup.com/messages
```

### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `messageTypes` | array | `ProductionUnavailability`, `ConsumptionUnavailability`, `TransmissionUnavailability`, `OtherUnavailability`, `MarketInformation` |
| `status` | string | `Active`, `Dismissed` |
| `unavailabilityType` | string | `Planned`, `Unplanned` |
| `publicationStartDate` | date | ISO 8601 UTC format |
| `publicationStopDate` | date | ISO 8601 UTC format |
| `eventStartDate` | date | ISO 8601 UTC format - filters by outage event start |
| `eventStopDate` | date | ISO 8601 UTC format - filters by outage event stop |
| `areas` | array | Area codes (e.g., `SE1`, `FI`, `DK1`) |
| `fuelTypes` | array | Fuel type codes |
| `marketParticipants` | array | From Market Participants lookup |
| `units` | array | Station codes |
| `connections` | array | From Connections lookup |
| `companies` | array | Valid Company IDs |
| `searchText` | string | Search in UnavailabilityReason and Remarks |
| `skip` | int | Number of results to skip (paging) |
| `limit` | int | Max results (default/max: 2000) |
| `order` | string | `PublicationDate` or blank |
| `orderDirection` | string | `ASC` or `DESC` |
| `includeOutdated` | boolean | Include outdated message versions |

### Example

```bash
curl 'https://ummapi.nordpoolgroup.com/messages?status=Active&limit=10'
curl 'https://ummapi.nordpoolgroup.com/messages?status=Active&fuelTypes=14&areas=SE'
```

### Response

```json
{
  "items": [...],
  "total": 92041
}
```

## Infrastructure Endpoints

```
GET /infrastructure/areas
GET /infrastructure/assets
GET /infrastructure/fueltypes
GET /infrastructure/stations
GET /infrastructure/connections
```

## Supported Areas

| Code | EIC Code | Country |
|------|----------|---------|
| UK | 10Y1001A1001A57G | United Kingdom |
| 50Hz | 10YDE-VE-------2 | Germany |
| TBW | 10YDE-ENBW-----N | Germany |
| AMP | 10YDE-RWENET---I | Germany |
| AT | 10YAT-APG------L | Austria |
| NL | 10YNL----------L | Netherlands |
| FR | 10YFR-RTE------C | France |
| NO1 | 10YNO-1--------2 | Norway |
| NO2 | 10YNO-2--------T | Norway |
| NO3 | 10YNO-3--------J | Norway |
| NO4 | 10YNO-4--------9 | Norway |
| FI | 10YFI-1--------U | Finland |
| BE | 10YBE----------2 | Belgium |
| DK1 | 10YDK-1--------W | Denmark |
| DK2 | 10YDK-2--------M | Denmark |
| SE1 | 10Y1001A1001A44P | Sweden |
| SE2 | 10Y1001A1001A45N | Sweden |
| SE3 | 10Y1001A1001A46L | Sweden |
| SE4 | 10Y1001A1001A47J | Sweden |
| EE | 10Y1001A1001A39I | Estonia |
| LV | 10YLV-1001A00074 | Latvia |
| LT | 10YLT-1001A0008Q | Lithuania |
| PL | 10YPL-AREA-----S | Poland |

## Fuel Type Codes

- 14: Nuclear
- 18: Wind Offshore
- 19: Wind Onshore
- 16: Solar
- 12: Hydro
- 4: Fossil Gas
- 5: Fossil Hard Coal

## Notes
- UMM provides generation unavailability data (not real-time generation)
- Used for tracking planned and unplanned outages
- No authentication required for public endpoints
- See [NORDPOOL.md](NORDPOOL.md) for time series (prices, generation)

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/nordpool_umm.rb)
