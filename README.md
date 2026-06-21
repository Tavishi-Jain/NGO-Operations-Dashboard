# NGO Donor & Operations Dashboard

An Excel-based operational reporting dashboard built as a companion piece to **[FoodCast](https://huggingface.co/spaces/Tavishi-jain08)** — my ML-based NGO donation forecasting engine. While FoodCast answers "what will donations look like next quarter?", this dashboard answers the question NGO program managers actually ask every Monday: **"What's happening with our donors right now?"**

## Why This Project Exists

Forecasting models are powerful, but most NGO decision-makers don't open Jupyter notebooks — they open Excel. This project demonstrates the other half of a complete data analytics skillset: turning raw, messy transactional data into a clean, interactive, decision-ready reporting tool.

## Dashboard Preview

![Dashboard Screenshot](dashboard_screens<img width="1187" height="732" alt="Dashboard_Screenshot" src="https://github.com/user-attachments/assets/752fd1a6-8268-47ad-8f58-1b6d7f5d6f18" />
hot.png)


## Key Metrics Tracked

- **Total Donations:** ₹46,94,553 across 1,801 transactions (Jan 2024 – Jun 2025)
- **Donor Retention Rate:** 93.5% (115 Active / 8 Lapsed donors, out of 123 total)
- **Top Campaign:** EmergencyFoodBank
- **Regional Performance:** Central region leads (₹10.85L); East trails (₹7.55L) — flagged as an outreach opportunity
- **Lapsed Donor Watchlist:** 8 donors flagged for re-engagement, prioritized by lifetime giving value

## Skills Demonstrated

| Category | Tools/Functions Used |
|---|---|
| Data Cleaning | `SUBSTITUTE`, `DATE`, `IFERROR`, `TRIM`, `PROPER`, `TEXT` |
| Conditional Logic | `IF`, nested `IF` for donor status classification |
| Aggregation | `SUMIFS`, `AVERAGEIF`, `COUNTIFS`, `MAXIFS` |
| Lookups | `XLOOKUP` for live donor search (name → status, total given) |
| Reporting | Pivot Tables (with manual date grouping), Pivot Charts, Slicers, power query, dax, power pivot |
| Visualization | Conditional Formatting (regional heatmap), Line & Bar charts |
| Data Validation | Duplicate detection, locale-aware date parsing, whitespace/casing normalization |


## Notable Debugging Challenges 


A few real-world data issues solved during this build (documented because debugging is half the skill):

- **Locale-dependent date parsing:** `DATEVALUE()` behaves inconsistently across regional settings — replaced with a manual `LEFT`/`MID`/`RIGHT` + `DATE()` reconstruction wrapped in `IFERROR` to handle two mixed date formats reliably.
- **Donor-level vs. transaction-level aggregation:** Used `MAXIFS()` to correctly compute "most recent donation" per donor (not per row), since each donor has multiple transactions.
- **Hidden whitespace bugs:** Donor names and category fields contained invisible trailing spaces, breaking `UNIQUE()` deduplication — caught via `EXACT()` testing and fixed with `TRIM()`.
- **Stale formula dependencies:** Learned to always convert formulas to static values (Paste Special → Values) *before* deleting their source/helper cells, after breaking the dashboard twice by doing it in the wrong order.

## Dataset

Synthetic NGO donation transaction data (1,815 rows, 7 fields), deliberately constructed with realistic data quality issues — mixed date formats, inconsistent casing, blank fields, and duplicate rows — to simulate authentic raw operational data.

## Related Work

- 🔗 [FoodCast — NGO Donation Forecasting Engine](https://huggingface.co/spaces/Tavishi-jain08) (ARIMA, ETS, Prophet, XGBoost, LSTM benchmarked — XGBoost achieving 13.81% MAPE)


---

*Built as part of a structured Excel-for-Data-Analytics learning path, following an 8-phase project methodology: Data Understanding → Cleaning → Helper Columns → Formula Building → Lookups → Pivot Tables → Dashboard Assembly → Insights.*
