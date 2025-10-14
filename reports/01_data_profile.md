# 01 - Data Intake and Audit Report

**Project:** `ecommerce-sales-insights`  
**Notebook:** `01_data_intake.ipynb`  
**Stage:** Bronze — Data Intake & Structural Audit  
**Date:** 2025-10-14  
**Author:** Pavel Andreenko

---

## 1. Overview

**Goal:**  
Verify that the raw Superstore dataset is readable, structurally consistent, and ready for subsequent cleaning and transformation.

**Source file:**  
`data/raw/superstore.csv`  
**Encoding:** Latin-1  
**Rows:** 9,994  
**Columns:** 21  

The dataset contains order-level sales records including customer, product, and shipping details.

---

## 2. Structural Profile

| Check | Result | Notes |
|-------|---------|-------|
| File encoding | UTF-8 | Original file contained non-UTF-8 characters (`\xa0`), re-read using `encoding = 'latin-1'` and cleaned. |
| Rows × Columns | 9,994 × 21 | --- |
| Column names | Mostly clean; contain spaces and capital letters | Will be standardized to `snake_case` |
| Missing values | None detected | --- |
| Duplicate rows | 1 exact duplicate  | Likely duplicate packaging records |
| Date format | `mm/dd/yyyy` objects | Requires conversion to datetime |
| Numeric formats | Decimal points, no currency symbols | Safe for numeric parsing |

---

## 3. Column Summary 

| Column | Type | Example | Notes |
|---------|------|----------|-------|
| Row ID | int | 1 | Internal index — not a business key, should be dropped |
| Order ID | object | CA-2016-152156 | Unique per order, Requires conversion to `str` |
| Order Date | object | 11/8/2016 | Requires conversion to `datetime` |
| Ship Date | object | 11/11/2016 | Requires conversion to `datetime` |
| Ship Mode | object | Second Class | Requires conversion to `category` |
| Customer ID | object | CG-12520 | Unique per customer, Requires conversion to `str` |
| Customer Name | object | Claire Gute | Requires conversion to `str` |
| Segment | object | Consumer | Requires conversion to `category` |
| Country | object | United States | Constant, should be dropped |
| City | object | Los Angeles | Requires conversion to `str` |
| State | object | California | Requires conversion to `category` |
| Postal Code | float/int | 90036 | Requires conversion to `str` |
| Region | object | West | Requires conversion to `category` |
| Product ID | object | FUR-BO-10001798 | Unique per product, Requires conversion to `str` |
| Category | object | Furniture | Requires conversion to `category` |
| Sub-Category | object | Bookcases | Requires conversion to `category` |
| Product Name | object | Bush Somerset Collection Bookcase | Unique per product, Requires conversion to `str` |
| Sales | float | 261.96 | numeric |
| Quantity | int | 2 | numeric |
| Discount | float | 0.00 | numeric |
| Profit | float | 41.91 | numeric |

---

## 4. Key Findings

- Data loaded successfully with consistent encoding and column alignment.  
- No missing values detected in any field.  
- Date columns are currently objects — will require parsing.  
- Column names contain spaces and uppercase letters — to be standardized.  
- Categorical fields appear clean and consistent.  
- `Row ID` adds no informational value, it will be dropped during the data cleaning stage.
- `Country` has only one unique value and will be dropped during cleaning stage.

---

## 5. Next Steps (Silver Stage)

1. Drop redundant `Row ID` and `Country` columns. 
2. Rename all columns to `snake_case` and remove non-breaking spaces.  
3. Convert dtypes
4. Save cleaned dataset to:  
   `data/interim/02_silver_clean.csv`