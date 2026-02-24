# Taipower Data Source

**Quick Facts:**
- **Region:** Taiwan - `TW`
- **Website:** https://www.taipower.com.tw/
- **Real-time Data:** https://www.taipower.com.tw/2764/2826/2829/2830/25090/
- **Historical Data:** https://www.taipower.com.tw/2764/2826/2829/2832/25093/normalPost
- **Timezone:** Asia/Taipei (UTC+8, no DST)
- **Data Format:** JSON
- **Units:** MW
- **Resolution:** 10-minute
- **Availability:** 
  - Real-time
  - Historical data only available as 24-hour averages on website
  - Archived historical data available: https://github.com/intermittentnrg/intermittent-taipower-sns-sqs

## Data Collection

### JSON Example

```json
{
  "": "2025-12-14 00:00",
  "dataset": [
    [["<A NAME='coal'></A><b>COAL</b>", "", "Linkou#1", "800.0", "756.1", "94.512%", " ", ""]],
    [["<A NAME='coal'></A><b>COAL</b>", "", "Subtotal", "10600.0(18.458%)", "4659.0(19.512%)", "", "", ""]],
    [["<A NAME='wind'></A><b>WIND</b>", "", "Subtotal", "762.4", "423.5", "", "", ""]],
    [["<A NAME='solar'></A><b>SOLAR</b>", "", "Subtotal", "0.0", "0.0", "", "", ""]]
  ]
}
```

## Unit-Level Classification

Units are further classified by inspecting unit names:
- Contains "Geothermal" → geothermal
- Contains "Biofuel" → biomass

## Notes

- Time format: `%Y-%m-%d %H:%M`
- Generation aggregates: Sum of units grouped by production type (rows with "Subtotal" in unit_id)
- Unit-level data: Individual power plant outputs
- Duplicate detection by timestamp
- Unit IDs may contain remarks in parentheses (stripped)
- Data provided at both generation aggregate and unit-level granularity

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/taipower.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/TAIPOWER.py)
