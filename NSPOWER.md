# NSPower Data Source

**Note:** Generation reported as percentages of total load, not absolute values.

**Quick Facts:**
- **Region:** Nova Scotia, Canada - `CA-NS`
- **Website:** https://www.nspower.ca/
- **Timezone:** America/Halifax (UTC-4/-3 with DST)
- **Data Format:** JSON
- **Units:** MW (load), percentages (generation mix)
- **Resolution:** Real-time
- **Availability:** Real-time only

## Endpoints

### Load Data
**Quick Facts:**
- **URL:** `https://www.nspower.ca/library/CurrentLoad/CurrentLoad.json`
- **Units:** MW

### Generation Mix
**Quick Facts:**
- **URL:** `https://www.nspower.ca/library/CurrentLoad/CurrentMix.json`
- **Units:** Percentages of total load

## Notes
- Time format: `datetime` field in format `/Date(1234567890000-0500)/` (milliseconds since epoch + timezone offset)
- Absolute generation values calculated as: `load * percentage / 100.0`
- Generation mix reported as percentages, not absolute values

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/nspower.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/CA_NS.py)
