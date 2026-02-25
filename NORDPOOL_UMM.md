# Nord Pool UMM (Urgent Market Messages)

**Quick Facts:**
- **Region:** Europe - Multiple bidding zones (Nordic, Baltic, UK, Germany, France, etc.)
- **Website:** https://www.nordpoolgroup.com/
- **Data Portal:** https://umm.nordpoolgroup.com/
- **API Documentation:** https://developers.nordpoolgroup.com/reference/umm-introduction
- **Timezone:** Multiple (depends on bidding zone)
- **Data Format:** JSON
- **Units:** MW (capacity)
- **Resolution:** Event-based (outage periods)
- **Availability:** Full history + future (past events and scheduled maintenance)

## Authentication

No authentication required for public endpoints.

## Endpoints

### Messages
**Quick Facts:**
- **API Endpoint:** `https://ummapi.nordpoolgroup.com/messages`
- **Documentation:** [HTML](https://developers.nordpoolgroup.com/reference/umm-api-messages-search) / [Markdown](https://developers.nordpoolgroup.com/reference/umm-api-messages-search.md)
- **Data Portal:** https://umm.nordpoolgroup.com/
- **Notes:** Returns generation unavailability messages. Use `skip` and `limit` for paging (max 2000 per call).

**Query Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `messageTypes` | array | `ProductionUnavailability`, `ConsumptionUnavailability`, `TransmissionUnavailability`, `OtherUnavailability`, `MarketInformation` |
| `status` | string | `Active`, `Dismissed` |
| `unavailabilityType` | string | `Planned`, `Unplanned` |
| `publicationStartDate` | date | ISO 8601 UTC format |
| `publicationStopDate` | date | ISO 8601 UTC format |
| `eventStartDate` | date | ISO 8601 UTC - filters by outage event start |
| `eventStopDate` | date | ISO 8601 UTC - filters by outage event stop |
| `areas` | array | EIC codes from Areas lookup |
| `fuelTypes` | array | Codes from Fuel Types lookup |
| `marketParticipants` | array | Codes from Market Participants lookup |
| `units` | array | EIC codes from Stations lookup |
| `connections` | array | Codes from Connections lookup |
| `companies` | array | Valid Company IDs |
| `searchText` | string | Search in UnavailabilityReason and Remarks |
| `skip` | int | Number of results to skip (paging) |
| `limit` | int | Max results (default/max: 2000) |
| `order` | string | `PublicationDate` or blank |
| `orderDirection` | string | `ASC` or `DESC` |
| `includeOutdated` | boolean | Include outdated message versions |

**Response:**

```json
{
  "items": [...],
  "total": 19657
}
```

- `items` - array of messages
- `total` - number of messages satisfying filter

**Example:**

```bash
curl 'https://ummapi.nordpoolgroup.com/messages?status=Active&limit=10'
curl 'https://ummapi.nordpoolgroup.com/messages?status=Active&fuelTypes=14&areas=10Y1001A1001A46L'
```

### Areas
**Quick Facts:**
- **API Endpoint:** `https://ummapi.nordpoolgroup.com/infrastructure/areas`
- **Documentation:** [HTML](https://developers.nordpoolgroup.com/reference/umm-api-infrastructure-areas) / [Markdown](https://developers.nordpoolgroup.com/reference/umm-api-infrastructure-areas.md)
- **Notes:** Returns bidding zone EIC codes.

### Stations
**Quick Facts:**
- **API Endpoint:** `https://ummapi.nordpoolgroup.com/infrastructure/stations`
- **Documentation:** [HTML](https://developers.nordpoolgroup.com/reference/umm-api-infrastructure-stations) / [Markdown](https://developers.nordpoolgroup.com/reference/umm-api-infrastructure-stations.md)
- **Notes:** Returns station names and EIC codes for unit filtering. Use `code` for the `units` parameter in messages endpoint.

**Response:**

```json
[
  { "name": "Forsmark Block1", "code": "46WPU0000000015W" },
  { "name": "G3", "code": "46WGU0000000009X" }
]
```

### Fuel Types
**Quick Facts:**
- **API Endpoint:** `https://ummapi.nordpoolgroup.com/infrastructure/fueltypes`
- **Documentation:** [HTML](https://developers.nordpoolgroup.com/reference/umm-api-infrastructure-fuel-types) / [Markdown](https://developers.nordpoolgroup.com/reference/umm-api-infrastructure-fuel-types.md)
- **Notes:** Returns fuel type codes.

### Connections
**Quick Facts:**
- **API Endpoint:** `https://ummapi.nordpoolgroup.com/infrastructure/connections`
- **Documentation:** [HTML](https://developers.nordpoolgroup.com/reference/umm-api-infrastructure-connections) / [Markdown](https://developers.nordpoolgroup.com/reference/umm-api-infrastructure-connections.md)
- **Notes:** Returns connection codes.

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
- See [NORDPOOL.md](NORDPOOL.md) for time series (prices, generation)

## Links

- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/nordpool_umm.rb)
