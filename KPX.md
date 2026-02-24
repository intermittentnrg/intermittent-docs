# KPX Data Source

**Quick Facts:**
- **Region:** South Korea - `KR`
- **Website:** https://new.kpx.or.kr/
- **Timezone:** Asia/Seoul (UTC+9, no DST)
- **Data Format:** HTML/JSON
- **Units:** MW (generation), Won/kWh (price, converted to Won/MWh)
- **Resolution:** Hourly
- **Availability:** Real-time and historical

## Endpoints

### Real-time Generation
**Quick Facts:**
- **URL:** `https://new.kpx.or.kr/powerinfoSubmain.es?mid=a10606030000`
- **Notes:** Generation mix embedded in HTML/JavaScript (`var ictArr`)

### Historical Generation
**Quick Facts:**
- **URL:** `https://new.kpx.or.kr/powerSource.es?mid=a10606030000&device=chart`
- **Notes:** POST form with CSRF token required; date selection via `view_sdate`/`view_edate`

### Real-time Price (SMP)
**Quick Facts:**
- **URL:** `https://new.kpx.or.kr/smpInland.es?mid=a10606080100&device=pc`
- **Units:** Won/kWh (converted to Won/MWh)
- **Resolution:** Hourly, past 7 days
- **Notes:** 
  - Won/kWh → Won/MWh (×1000)
  - Won → jeon/cents (×100)
  - Hour 24 rolls over to next day (Korean convention)

## Notes
- Time format: Generation `%Y-%m-%d %H:%M`; Price dates `%m.%d` with Korean weekday
- CSRF token required for historical data
- Session cookies managed via Faraday cookie jar

## Links
- [intermittent.energy](https://github.com/intermittentnrg/intermittent-importer/blob/master/lib/kpx.rb)
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/KPX.py)
