# 04 — Exploratory Data Analysis (Pre-Dashboard) Summary

**Project:** `ecommerce-sales-insights` 
**Notebook:** `04_eda.ipynb`  
**Stage:** EDA (pre-Tableau validation & insight harvesting)  
**Date:** 2025-10-22  
**Author:** Pavel Andreenko

---

## 1. Objective

Validate the Gold dataset and extract the **minimum set of trustworthy insights** needed to design a focused Tableau dashboard. The goal is not only to make pretty charts here, but also to **confirm data behavior, quantify relationships, and surface the few patterns that matter**.

---

## 2. Inputs

- Gold dataset version: `data/processed/03_gold_features.parquet`  
- Aggregated KPIs: `data/processed/03_gold_aggregated_kpis.csv`

**Core KPIs (from aggregated file):**

| KPI | Value |
|---|---:|
| Total Revenue | **2,297,200.86** |
| Total Profit | **286,397.02** |
| Average Profit Margin | **12.03 %** |
| Repeat-Customer / Multi-line Rate | **99.37 %** |
| Average Shipping Delay | **3.96 days** |

---

## 3. Data readiness checks 

- **Dtypes:** dates are proper `datetime`; engineered time parts present (`order_year`, `order_month`, `order_weekday`, etc.).  
- **Nulls:** none relevant for KPI columns (sales, profit, discount, dates).  
- **Duplicates:** no true duplicates; repeated `order_id` reflects multi-line orders (expected).  
- **Metric integrity:** profit margin defined as `%`, not fraction.
---

## 4. Insight summary

Below are the **textual insights extracted from the EDA notebook** and tightened up into dashboard-ready statements. I’m staying concise but keeping the business meaning.

### 4.1 Economical performance (time & totals)
- Sales **increase YoY** with recognizable **seasonality**; recurring peaks around **Mar, Sep, Nov** and weak spots in **Jan–Feb** and **mid-summer**.  
- Revenue and profit are **positively coupled** (expected), but profit growth lags slightly behind revenue growth in some periods → margin pressure in peak months.

**Implication for dashboard:** show a monthly Revenue/Profit trend with a YoY toggle; add a secondary line for **profit margin %** to reveal peak-season erosion.

### 4.2 Customer behavior & Pareto shape
- Very high **repeat / multi-line share (~99%)** → a small set of customers and baskets contribute a large chunk of revenue (classic **Pareto**).  
- A minority of customers likely drives most profit; long tail exists.

**Implication:** add a **Top-N customers** tile and a **cumulative contribution curve** (Pareto) to visualize concentration.

### 4.3 Discount & pricing
- **Profit margin is strongly negatively correlated with discount.**  
- Discounted transactions cluster at **lower margins** and occasionally in **loss territory** for certain sub-categories.

**Implication:**  include a **Discount vs Profit Margin** scatter (filterable by category/segment). Add a **no-discount vs discount** comparison of average margin.

### 4.4 Operations — shipping delay
- **Same Day** → almost no delay, highest margins.
- **First/Second Class** → moderate delays (~2–4 days), steady profitability.
- **Standard Class** → longest delays (4–6 days), lowest and occasionally negative margins.
- Longer delays generally mean lower profitability.

**Implication:** Add a **Delay vs. Profit Margin** heatmap by Ship Mode, highlighting Standard Class as least profitable with service-level filtering.

### 4.5 Regional view
- **West** region shows both **highest revenue and profit**; **Central** lags in both revenue and profit.  
- Profitability broadly aligns with sales volume by region (no glaring efficiency anomaly region-wide).  
- **California** and **New York** stand out on total profit; several Central/Southern states underperform.

**Implication:** primary slicers should be **Region → State**; add a state leaderboard + map (if used).

### 4.6 Product portfolio
- **Phones & Copiers**: top performers with both high sales and strong profit → clear growth drivers.
- **Chairs**: solid revenue but moderate margins → pricing or sourcing review needed. 
- **Tables**: consistently high sales but negative profit → pricing and discount strategy need correction.
- **Binders, Appliances, Storage**: balanced performance → maintain current focus.
- **Fasteners, Labels, Art, Envelopes**: minimal impact → consider reducing stock or repositioning.

**Implication:** add a **Category vs Profit Margin** bar chart to highlight top and underperforming products, with Tables flagged for review

---
## 5. Quantified relationships

- **Corr(sales, profit):** strong positive (expected; confirms basics).  
- **Corr(discount, profit_margin):** **negative and material** (pricing levers matter).  
- **Corr(Delay, profit):** weak → keep operational views separate from commercial KPIs.

---

## 6. Risks & conventions to carry into the dashboard

- **Use raw data**, because Tableu does not work with `.parquet` data format
- Multi-line orders: **don’t count “orders” from line-items** unless pre-aggregate; prefer explicit **order count** when needed.  
- For seasonality, use **continuous monthly date**; avoid discrete months across years (to keep trends readable).

---

## 7. Potential dashboard layout (driven by the EDA)

1) **KPI band:** Revenue, Profit, Profit Margin %, Orders, Shipping Delay  
2) **Trend:** Monthly Revenue + Profit + Margin% (YoY switch)  
3) **Drivers:** Map — Region × Segment × Category (Profit & Profit Margin)  
4) **Pricing:** Discount vs Profit Margin scatter + side-by-side no-discount vs discount averages  
5) **Operations:** Delay distribution + exceptions table (>7 days)  
6) **Customers:** Pareto curve + Top-N customers (revenue and profit)

---

## 8. Final takeaway 

- The business grows with clear seasonal peaks.  
- Profit follows revenue but margins **compress when discounting ramps up**.  
- **West** and large states (CA, NY) drive profit; **Tables** needs attention (volume without value).  
- Shipping is mostly fine (avg ~4 days), with a small tail of late deliveries worth monitoring.  

This is enough to start the Tableau build with **confidence** and a **tight scope**.
