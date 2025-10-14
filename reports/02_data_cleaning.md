# 02 - Data Cleaning

**Project:** `ecommerce-sales-insights`  
**Notebook:** `02_data_cleaning.ipynb`  
**Stage:** Silver  — Data Cleaning 
**Date:** 2025-10-14  
**Author:** Pavel Andreenko

---
## 1. Overview
**Goal**: Make data consistent, clean, and analysis-ready.

**Input:** `data/interim/01_bronze_intake.csv`  
**Output:** `data/interim/02_silver_clean.csv`

---

## 2. Cleaning Summary

| Step | Action | Result |
|------|---------|--------|
| 1 | Convert datetimes, categorical colunms and sting-columns | ✅ |
| 2 | Standartize column names | ✅ |
| 3 | Drop `Row ID` and `Country`| ✅ |

---

## 3. Validation
| Check | Result |
|--------|--------|
| Rows × Cols | 9 994 × 19 |
| Missing values | 0 |
| Encoding | UTF-8 |
| Duplicates | 0 true duplicates |

---

## 4. Key Improvements
- Redundant columns dropped.
- Uniform naming and datatypes.  
- Structural cleanliness achieved.  
- Dataset ready for feature engineering.

---

## 5. Next Steps
- Create derived time and business features.  
- Save to `data/processed/03_gold_features.csv`.