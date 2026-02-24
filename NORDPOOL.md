# Nord Pool Time Series Data Source

**Quick Facts:**
- **Region:** Europe - Multiple bidding zones (Nordic, Baltic, UK, Germany, France, etc.)
- **Website:** https://www.nordpoolgroup.com/
- **Data Portal:** https://data.nordpoolgroup.com/
- **Timezone:** Multiple (depends on bidding zone)
- **Data Format:** JSON (API), CSV (downloads)
- **Units:** MW, MWh, €/MWh
- **Resolution:** Hourly, 15-minute (intraday)
- **Availability:** Day-ahead and intraday markets

## Data Services

### Day-Ahead Auctions
**URL:** `https://data.nordpoolgroup.com/auction/day-ahead/prices`

### Intraday
**URL:** `https://data.nordpoolgroup.com/intraday/intraday-market-statistics`

### Power System Data
**URL:** `https://data.nordpoolgroup.com/power-system/`

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

## Terms and Conditions

From https://www.nordpoolgroup.com/en/About-us/terms-and-conditions-for-useofwebsite/:

- Data may be downloaded for trading, analysis, or research purposes
- Redistribution or republication requires prior written consent
- Automatic extraction of data is prohibited (blocks users)
- Data is provided "as is" without warranty
- Subject to Norwegian law

## Notes
- Nord Pool operates day-ahead and intraday markets across Europe
- System price is calculated for Nordic region
- Bidding areas have individual prices
- See [NORDPOOL_UMM.md](NORDPOOL_UMM.md) for generation outage data

## Links
- [electricityMaps](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/electricitymap/contrib/parsers/NORDPOOL.py)
