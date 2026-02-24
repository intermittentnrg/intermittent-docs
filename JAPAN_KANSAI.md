# Kansai Nuclear Data

Kansai doesn't provide public demand CSV files like other regions. See [JAPAN.md](JAPAN.md) for demand data.

## Nuclear Power Generation

**URL:** `https://www.kepco.co.jp/energy_supply/energy/nuclear_power/info/monitor/live_unten/`

**Notes:**
- Live monitor page with multiple nuclear units
- OCR of time image (.time-data class)
- Capacity in 万 (万 = 10,000 kW = 10 MW)
- Percentage extracted from gif images via OCR
- Real-time only (no historical CSV)

## Production Type Mapping

| Source | Production Type |
|--------|----------------|
| Multiple units | nuclear |

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/japan_nuclear/kepco.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/JP_KN.py)
