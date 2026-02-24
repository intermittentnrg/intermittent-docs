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
**Data Portal:** `https://data.nordpoolgroup.com/auction/day-ahead/prices`

### Intraday
**Data Portal:** `https://data.nordpoolgroup.com/intraday/intraday-market-statistics`

### Power System Data
**Data Portal:** `https://data.nordpoolgroup.com/power-system/`

## Terms and Conditions

From https://www.nordpoolgroup.com/en/About-us/terms-and-conditions-for-useofwebsite/:

- Data may be downloaded for analysis or research of your firm or company
- You may not republish, retransmit, redistribute or otherwise make the contents available to any other party or on any website without express prior written consent

## Notes
- Nord Pool operates day-ahead and intraday markets across Europe
- System price is calculated for Nordic region
- Bidding areas have individual prices
- See [NORDPOOL_UMM.md](NORDPOOL_UMM.md) for generation outage data
