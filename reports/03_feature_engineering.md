# 03 — Feature Engineering Report

**Project:** Retail Sales Insights  
**Notebook:** `03_feature_engineering.ipynb`  
**Stage:** Gold — Feature Engineering & KPI Aggregation  
**Date:** 2025-10-15  
**Author:** Pavel Andreenko

---

## 1. Overview

**Goal:**  
Transform the cleaned Silver-stage dataset into an enriched analytical dataset and derive KPIs for subsequent exploratory analysis and dashboard visualization.

**Input dataset:**  
`data/interim/02_silver_clean.csv`  

**Outputs:**  
- `data/processed/03_gold_features.parquet` — enriched transactional dataset  
- `data/processed/03_gold_aggregated_kpis.csv` — aggregated KPI metrics  

---

## 2. Engineered Features

| Feature          | Purpose                                                   |
|-----------------|-----------------------------------------------------------|
| `order_year`     | Enables year-over-year comparison                         |
| `order_month`    | Month-level trend analysis                                |
| `order_weekday`  | Detects weekday vs weekend purchase patterns              |
| `order_quarter`  | Seasonal grouping for profitability analysis              |
| `ship_delay_days`| Measures logistics efficiency and delivery speed          |
| `profit_margin`  | Evaluates transaction-level profitability                 |
| `has_discount`  | Indicates discounted transactions                         |


Each feature was verified for correct dtype, non-null values, and alignment with business logic.  

---

## 3. Aggregated KPIs

**Objective:**  
Summarize total business performance to support Tableau dashboards and EDA.

**Output file:**  
`data/processed/03_gold_aggregated_kpis.csv`

| KPI  | Description |
|------|--------------|
| `total_sales`  | Aggregated revenue |
| `total_profit` | Aggregated profit |
| `avg_profit_margin` | Profitability ratio |
| `discount_rate` | Average discount applied |
| `order_count` | Number of transactions |
| `avg_ship_delay_days` |  Average delivery delay |

The file was cross-validated to ensure group totals match transactional-level data within `03_gold_features.parquet`.

---

## 4. Data Quality Validation

| Check | Result | Notes |
|--------|---------|-------|
| Rows × Columns (`03_gold_features.parquet`) | 9,994 × 28 | 7 new engineered features added |
| Missing values | None | All calculated columns complete |
| Duplicates | None | Verified by `Order ID` |

---

## 5. Key Improvements

- Added **temporal**, **logistics**, and **profitability** features for richer analytics.  
- Created **aggregated KPIs** to support both Tableau and Python-based EDA.  
- Verified feature consistency and ensured all dtypes preserved via Parquet output.  
- Dataset is now analysis-ready, containing all relevant dimensions for slicing and aggregation.

---

## 6. Next Steps (EDA Stage)

1. Perform exploratory data analysis (`04_eda.ipynb`) to identify trends and outliers.  
2. Visualize and analyze regional and category-level profitability.  
3. Evaluate discount impact on margin and shipping delay patterns.
4. Explore correlations between numeric features
5. Document findings in `reports/04_eda_summary.md`.
