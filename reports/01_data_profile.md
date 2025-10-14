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
| Row ID | int | 1 | Internal index — not a business key |
| Order ID | object | CA-2016-152156 | Unique per order |
| Order Date | object | 11/8/2016 | Datetime |
| Ship Date | object | 11/11/2016 | Datetime |
| Ship Mode | object | Second Class | Categorical |
| Customer ID | object | CG-12520 | Unique per customer |
| Customer Name | object | Claire Gute | --- |
| Segment | object | Consumer | Categorical |
| Country | object | United States | Constant |
| City | object | Los Angeles | --- |
| State | object | California | --- |
| Postal Code | float/int | 90036 | Convert to str |
| Region | object | West | Categorical |
| Product ID | object | FUR-BO-10001798 | Unique per product |
| Category | object | Furniture | Categorical |
| Sub-Category | object | Bookcases | Categorical |
| Product Name | object | Bush Somerset Collection Bookcase | ---- |
| Sales | float | 261.96 | --- |
| Quantity | int | 2 | --- |
| Discount | float | 0.00 | --- |
| Profit | float | 41.91 | --- |

---

## 4. Key Findings

- Data loaded successfully with consistent encoding and column alignment.  
- No missing values detected in any field.  
- Date columns are currently objects — will require parsing.  
- Column names contain spaces and uppercase letters — to be standardized.  
- Categorical fields (`Ship Mode`, `Segment`, `Region`) appear clean and consistent.  
- `Row ID` is a sequential index — will be removed in the Cleaning (Silver) stage.

---

## 5. Next Steps (Silver Stage)

1. Rename all columns to `snake_case` and remove non-breaking spaces.  
2. Convert `Order Date` and `Ship Date` to datetime format.  
3. Drop redundant `Row ID` column after verifying uniqueness.  
4. Save cleaned dataset to:  
   `data/interim/02_silver_clean.csv`