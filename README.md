# World Indicators Analysis

End-to-end analysis of **26 World Bank indicators (2016-2024)** across **217 countries**, combining a Python data pipeline with an interactive Power BI dashboard on health, economy, trade, poverty, technology and the environment.

## Highlights

- **Income is the master variable.** Log GDP per capita correlates 0.87 (Spearman) with life expectancy and 0.88 with internet use.
- **Health spending (% of GDP) explains almost nothing once income is known.** R² stays at 0.70 with or without it.
- **Pandemic impact:** average GDP growth fell to -5.1% in 2020, and life expectancy dropped in 84% of countries between 2019 and 2021.
- **Digital catch-up:** lower-middle-income countries gained 26 points of internet use in 2016-2022, against 9 for high-income countries.
- **Data quality matters:** including regional aggregates (World, income groups) inflated average trade value 6.7x.

## Tech Stack

- **Python:** pandas, NumPy, requests, seaborn, matplotlib
- **Jupyter Notebook:** data fetching and exploration
- **Power BI Desktop:** Power Query (M), DAX measures, Python visuals
- **Data source:** [World Bank Open Data API (v2)](https://datahelpdesk.worldbank.org/knowledgebase/articles/889392-about-the-indicators-api-documentation)

## Indicators

| Theme | Indicators |
|---|---|
| Economic | GDP growth, GDP per capita |
| Labour | Unemployment (total, youth), labour force |
| Trade | Exports, imports |
| Poverty | Poverty headcount, Gini index |
| Environment | Renewable energy share, forest area |
| Health | Life expectancy, infant and maternal mortality, health expenditure, immunization (DPT, measles), water access, TB, HIV, and more (13 total) |
| Technology | Internet users, mobile subscriptions |

## Project Structure

```
world-indicators-analysis/
├── README.md
├── requirements.txt
├── notebook/        # Jupyter notebook (API fetch, cleaning, analysis)
├── dashboard/       # Power BI file (.pbix)
├── data/            # CSV extracts
├── images/          # Dashboard screenshots
└── report/          # Full project report
```

## How It Works

1. **Fetch:** the notebook pulls the countries list and each indicator from the World Bank API, paginating through all pages and keeping years after 2015.
2. **Clean and merge:** each theme is merged with country attributes (region, income level) on ISO2 country code.
3. **Model:** Power BI loads the tables through Power Query (`Python.Execute`) and links them to a country dimension table.
4. **Visualize:** KPI cards, regional charts, animated bubble scatters, poverty top/bottom 10 tables, a regression plot, and a health correlation heatmap.

## Getting Started

```bash
git clone https://github.com/<your-username>/world-indicators-analysis.git
cd world-indicators-analysis
pip install -r requirements.txt
jupyter notebook
```

Run the notebook top to bottom, then open the `.pbix` file in Power BI Desktop.

### Power BI notes

- The dashboard loads data through Python scripts, so Python must be enabled in Power BI Desktop (File > Options > Python scripting).
- Some queries read a local CSV. Update the file path in Power Query (Transform data > Source) to match your machine.
- The data snapshot ends around 2023, and 2024 is mostly empty. Refreshing will pull newer years as the World Bank publishes them.

## Key Findings and Data Notes

- Analysis is **country-level only**: 49 regional and income-group aggregates are excluded.
- Medians are used for skewed indicators (in 2022, mean GDP per capita was $20,520 and the median $7,606).
- Poverty data covers only about 20% of country-years, so regional poverty comparisons are unreliable.
- All relationships are correlations, not causal effects.

## Future Work

- Add per-capita health spending and test its effect on life expectancy.
- Population-weighted averages and a panel regression with country fixed effects.
- Cluster countries on development indicators.
- Scheduled refresh through a Power BI gateway.

## Author

**Shravan Aldar**
Pune
