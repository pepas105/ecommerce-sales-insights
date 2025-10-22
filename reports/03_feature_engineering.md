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



| KPI  | Description | Value |
|------|--------------|---|
| `total_sales`  | Aggregated revenue | **2,297,200.86** |
| `total_profit` | Aggregated profit |**286,397.02** |
| `avg_profit_margin` | Profitability ratio |**12.03 %** |
| `repeat_customer_rate` | Rate of Customers who made more than 1 order | **99.37%** |
| `avg_ship_delay_days` |  Average delivery delay | **3.96 days** |

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

1. **Perform exploratory data analysis** (`04_eda.ipynb`) to identify trends and outliers.  
2. **Visualize and analyze** Economical Performance, Customer Behaviour, Discount, Pricing, Operational Efficiency, Regional and Product-level profitability.
4. **Explore correlations** between numeric features
5. Document findings in `reports/04_eda_summary.md`.
