# Japan Importers Documentation

All Japanese power companies report data in **10MW** units (万 = 10,000 kW). Timezone is **Asia/Tokyo (UTC+9)** for all regions.

## Juyo (Demand/Supply) Data

All regions provide daily CSV files with demand and renewable generation data.

| Region | Code | Company | URL Pattern |
|--------|------|---------|-------------|
| Hokkaido | JP-HKD | Hokkaido Electric Power | `http://denkiyoho.hepco.co.jp/area/data/juyo_01_{YYYYMMDD}.csv` |
| Hokuriku | JP-HR | Hokuriku Electric Power | `https://www.rikuden.co.jp/nw/denki-yoho/csv/juyo_05_{YYYYMMDD}.csv` |
| Chubu | JP-CB | Chubu Electric Power | `https://powergrid.chuden.co.jp/denki_yoho_content_data/juyo_cepco003.csv` |
| Tokyo | JP-TK | TEPCO | `https://www.tepco.co.jp/forecast/html/images/juyo-d1-j.csv` |
| Kyushu | JP-KS | Kyushu Electric Power | `https://www.kyuden.co.jp/td_power_usages/csv/juyo-hourly-%Y%m%d.csv` |
| Okinawa | JP-ON | Okinawa Electric Power | `https://www.okiden.co.jp/denki2/juyo_10_{YYYYMMDD}.csv` |
| Shikoku | JP-SK | Shikoku Electric Power | `https://www.yonden.co.jp/denkiyoho/juyo_shikoku.csv` |
| Tohoku | JP-TO | Tohoku Electric Power | `https://setsuden.nw.tohoku-epco.co.jp/common/demand/juyo_02_{YYYYMMDD}.csv` |

### CSV Data Format

**Common Format:**
- **Encoding:** Shift_JIS (Japanese)
- **Time format:** `%Y/%m/%d %H:%M`
- **Timezone:** Asia/Tokyo (convert to UTC by subtracting 9 hours)
- **Units:** 万 (10,000 kW = 10 MW)

**CSV Structure:**
- Header rows at the top (region-specific row numbers)
- Data rows start after header (typically row 55+)
- Columns: DATE, TIME, 当日実績 (demand), 太陽光発電 (solar), [風力発電 (wind - Tohoku only)]

### CSV Offsets (Critical)

These offsets are used by all importers to parse the data:

| Region | Header Row | Data Start | Data End | Notes |
|--------|------------|------------|----------|-------|
| Most regions | 54 | 55 | 343 | 288 intervals (24h × 12) |
| Kansai | 57 | 58 | 346 | Different row indices |

**Column Mapping:**
| Index | Field | Description |
|-------|-------|-------------|
| 0 | DATE | Date in `%Y/%m/%d` format |
| 1 | TIME | Time in `%H:%M` format |
| 2 | 当日実績 | Actual demand |
| 3 | 太陽光発電 | Solar generation |
| 4 | 風力発電 | Wind generation (Tohoku only - unique among regions) |

### Region-Specific Notes

- **Tohoku** is unique: includes wind generation (風力発電) in column 4, unlike other regions which only have solar

## Nuclear Data

Some regions have nuclear power plants with real-time data. See individual documentation files:

| Region | Documentation |
|--------|----------------|
| Kansai | [JAPAN_KANSAI.md](JAPAN_KANSAI.md) |
| Kyushu | [JAPAN_KYUSHU.md](JAPAN_KYUSHU.md) |
| Shikoku | [JAPAN_SHIKOKU.md](JAPAN_SHIKOKU.md) |

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/japan_juyo.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/JP.py)
