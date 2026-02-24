# Importer Documentation Template

This document defines the common structure for all data source importer documentation in `importers/*.md`.

## Standard Structure

```
# <Data Source Name>

**Note:** Optional implementation status or important notice

**Quick Facts:**
- **Region:** <country/region name> - <Area Code(s)>
- **Website:** <URL>
- **Data Portal:** <data portal URL if available>
- **API Documentation:** <API docs URL if available>
- **Timezone:** <TZ>
- **Data Format:** <CSV/JSON/XML>
- **Units:** <MW/MWh/etc>
- **Resolution:** <5min/15min/30min/hourly/daily>
- **Availability:** <real-time / historical from YYYY / limitations>

## Endpoints

### <Endpoint Name>
**Quick Facts:**
- **URL:** <endpoint URL>
- **Documentation:** <API docs URL if available>
- **Data Portal:** <data portal URL if available>
- **Units:** <if different from main>
- **Resolution:** <if different from main>
- **Notes:** <endpoint-specific notes>
- **Columns:**
  - ColumnName
  - AnotherColumn

### <Endpoint Name 2>
...

## Authentication
<explanation of API keys, tokens, etc.>

## Notes
<implementation details, quirks, special handling, time format, data limitations, etc.>
```

## Section Guidelines

### Required Sections
- **Title**: Must follow format `# <Data Source Name>`
- **Quick Facts**: Header with key attributes (Region, Website, Timezone, Data Format, Units, Resolution, Availability)
- **Endpoints**: Section listing all endpoints with mini Quick Facts and CSV columns
- **CSV Columns**: Document columns per endpoint in Quick Facts
- **Notes**: Implementation details, quirks, special handling

### Optional Sections
- **Note**: For deprecation notices, incomplete status, or important warnings (placed after title)
- **Authentication**: API keys, tokens, or credentials needed

### Quick Facts - Main
The main Quick Facts box should contain:
- **Region:** Geographic coverage and area/region code(s) used in database
- **Website:** Primary URL for the data source
- **Data Portal:** Data portal URL for browsing/download (if available)
- **API Documentation:** API documentation URL (if available)
- **Timezone:** IANA timezone identifier with UTC offset and DST info
- **Data Format:** CSV, JSON, XML, etc.
- **Units:** MW, MWh, $/MWh, etc.
- **Resolution:** 5min, 15min, 30min, hourly, daily, etc.
- **Availability:** Historical start date, real-time availability, max range, delays, limitations

### Quick Facts - Endpoint
Each endpoint should have a mini Quick Facts box with:
- **URL:** The endpoint URL
- **Documentation:** API documentation URL (if available)
- **Data Portal:** Data portal URL for browsing/download (if available)
- **Units:** If different from main Quick Facts
- **Resolution:** If different from main Quick Facts
- **Notes:** Endpoint-specific details, parameters, quirks
- **Columns:** (for CSV endpoints)
  - ColumnName
  - AnotherColumn

### CSV Endpoints
Include a CSV example after the Columns list:
```csv
Header1,Header2,Header3
value1,value2,value3
```

### JSON Endpoints
Include a JSON example after the Notes:
```json
{
  "field": "value"
}
```

### Authentication Section
Document authentication requirements:
- API keys (environment variable names)
- Tokens and how to obtain them
- OAuth2 flows
- Geoblocking restrictions
- CSRF tokens or session cookies

### Notes Section
Include:
- Time format details and quirks
- Sign conventions (negative values for exports, charging, etc.)
- Data limitations (max range, delays, etc.)
- Special handling requirements
- Known issues
- Multi-region considerations
- Alternatives (other data sources for same region)

## Formatting Conventions

- Use H3 (`###`) for endpoints
- Use bullet lists for CSV columns
- Include code examples for JSON/XML structures
- Specify strftime format strings in backticks: `%Y-%m-%d %H:%M`
- Document timezone conversions (source timezone → UTC)
- Note any non-standard conventions (negative values, 1-indexed hours, etc.)

## Common Patterns to Document

### Time Format Quirks
- 1-indexed vs 0-indexed hours
- Hour beginning vs hour ending convention
- Leap second notation
- Multiple date formats in same source
- Timezone handling (DST, regional offsets)

### Sign Conventions
- Negative for exports/imports
- Negative for battery/pump storage charging
- Inverted flow directions

### Data Availability
- Maximum date range per request
- Delayed availability (settlement periods)
- Historical vs real-time data differences
- Geoblocking or authentication requirements
- Data gaps or known issues

### Multi-region Sources
- Include all region codes in the Region field
- Use region mapping tables
- Document regional endpoint variations
- Specify timezone differences by region
