# ENEC Data Source

**Quick Facts:**
- **Region:** United Arab Emirates - `AE`
- **Website:** https://www.enec.gov.ae/
- **Timezone:** Asia/Dubai (UTC+4, no DST)
- **Data Format:** HTML (scraped from front page)
- **Units:** GWh (converted to MWh: value × 1,000,000)
- **Resolution:** Real-time (instant snapshot)
- **Availability:** Real-time only - data fetched from front page, not archived

## Data Source

**URL:** `https://www.enec.gov.ae/` (front page)

**Notes:**
- Data is from the front page of ENEC website (Barakah Nuclear Power Plant)
- Instant snapshot only - no historical data available

## Nuclear Units

| Unit | Unit ID | Notes |
|------|---------|-------|
| Unit 1 | BARAKAH-1 | |
| Unit 2 | BARAKAH-2 | |
| Unit 3 | BARAKAH-3 | |
| Unit 4 | BARAKAH-4 | |

## Data Extraction

- Parses HTML from front page
- Extracts time from JavaScript: `let actualDate = new Date("...")`
- Unit data from elements: `#count-air-unit1` through `#count-air-unit4`
- Global aggregate from: `#count-air-unit-global`

## Notes
- Time format: `%Y-%m-%d %H:%M:%S`
- Values are in GWh, converted to MWh for storage
- 4 operational nuclear units at Barakah plant

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/enec.rb)
