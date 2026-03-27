# 📊 Interactive Sales Performance Dashboard

> **End-to-end business intelligence project** — from raw data to actionable insights — built with Excel, Power Query, and Power BI.

---

## 🗂️ Table of Contents

- [Project Overview](#project-overview)
- [Dashboard Pages](#dashboard-pages)
- [Key Metrics & Insights](#key-metrics--insights)
- [Workflow Summary](#workflow-summary)
- [Data Preparation — Excel](#data-preparation--excel)
- [Data Modelling — Power BI](#data-modelling--power-bi)
- [DAX Measures](#dax-measures)
- [Tools & Technologies](#tools--technologies)
- [How to Use](#how-to-use)
- [File Structure](#file-structure)

---

## Project Overview

This project delivers an **interactive 3-page sales performance dashboard** designed to give business stakeholders a clear view of revenue trends, product performance, regional breakdowns, and sales team effectiveness.

The full analytics pipeline was built from scratch:

1. **Data cleaning & transformation** in Microsoft Excel (Power Query)
2. **Data modelling & relationship building** in Power BI
3. **DAX measures** to derive calculated KPIs and dynamic metrics
4. **Interactive visualisations** across 3 dedicated report pages

---

## Dashboard Pages

The report is structured across three focused pages, navigable from the landing screen:

### Page 1 — Executive Overview
> *"Real-time insights into your business performance"*

A high-level summary page for leadership — consolidating the most critical business metrics in one view.

**Visuals included:**
- 3 KPI cards: Total Revenue, Units Sold, Average Order Value
- Revenue Over Time — monthly area chart (2020 trend)
- Revenue by Product Category — horizontal bar chart (Categories A–D)
- Revenue by Region — bar chart (East, West, South, Central)
- Salesperson Revenue leaderboard table
- Month slicer for dynamic filtering

---

### Page 2 — Sales Overview
> *"Track and manage your sales force performance"*

A deep-dive into sales team performance, regional breakdowns, and individual target attainment.

**Visuals included:**
- 4 KPI cards: Salespersons, Total Revenue, Units Sold, Active Regions
- Sales Trend by Category Over Time — line chart (order volume, 2020)
- Salesperson Performance Table — Revenue, Region, Sales Volume, Performance %, and Target
- Count of Salesperson by Region — donut chart
- Regional Revenue Cards — individual tiles for East, West, South, Central (revenue + order size)
- Month slicer for dynamic filtering

---

### Page 3 — Product Overview
> *"Analyze product performance and category insights"*

A product-level page for category managers and merchandising teams.

**Visuals included:**
- 4 KPI cards: Product Categories, Product Revenue, Units Sold, Return Rate
- Product Category Cards — 4 tiles (A, B, C, D) each showing Total Revenue, Order Size, Average Price, Return Rate
- Sales Trend by Category Over Time — multi-line chart comparing all 4 categories across 2020
- Month slicer for dynamic filtering

---

## Key Metrics & Insights

### 📌 Top-Level KPIs

| Metric | Value |
|--------|-------|
| **Total Revenue** | $19.7M |
| **Units Sold** | 1,334 |
| **Average Order Value** | $14,783 |
| **Active Regions** | 4 |
| **Salespersons** | 6 |
| **Product Categories** | 4 |
| **Overall Return Rate** | 16.4% |

---

### 🌍 Revenue by Region

| Region | Total Revenue | Orders |
|--------|--------------|--------|
| **East** | $6,713,699 | 458 |
| **West** | $6,208,930 | 412 |
| **South** | $3,539,599 | 239 |
| **Central** | $3,258,215 | 225 |

> East and West together account for approximately **65%** of total revenue.

---

### 👤 Salesperson Performance

| Salesperson | Revenue | Region | Performance vs Target |
|-------------|---------|--------|----------------------|
| Robert Brown | $3,539,599 | South | **416%** |
| Mike Davis | $3,258,215 | Central | **343%** |
| John Smith | $3,484,342 | East | 290% |
| Emily Chen | $3,104,794 | West | 282% |
| Sarah Johnson | $3,104,136 | West | 282% |
| Lisa Anderson | $3,229,357 | East | 269% |
| **Total** | **$19,720,443** | | **481%** |

> Every salesperson significantly exceeded their individual targets — the team collectively reached **481% of total target**.

---

### 📦 Product Category Performance

| Category | Revenue | Orders | Avg Price | Return Rate |
|----------|---------|--------|-----------|-------------|
| **D** | $5,309,581 | 346 | $254.28 | 17.9% |
| **A** | $5,218,986 | 349 | $252.49 | **12.0%** ✅ |
| **B** | $4,684,906 | 334 | $237.64 | 17.3% |
| **C** | $4,506,970 | 305 | $249.72 | 18.6% ⚠️ |

> Category **D** leads in revenue. Category **A** has both strong revenue and the lowest return rate (12%). Category **C** has the highest return rate at 18.6% — a candidate for quality or fulfilment review.

---

## Workflow Summary

```
Raw Sales Data (Excel)
        │
        ▼
  Data Cleaning & Transformation (Power Query / Excel)
        │
        ▼
  Data Modelling (Power BI — Star Schema)
        │
        ▼
  DAX Measures (KPIs, Rankings, Performance %)
        │
        ▼
  3-Page Interactive Dashboard (Power BI Report)
  ┌─────────────┐  ┌────────────────┐  ┌──────────────────┐
  │  Executive  │  │    Sales       │  │    Product       │
  │  Overview   │  │    Overview    │  │    Overview      │
  └─────────────┘  └────────────────┘  └──────────────────┘
```

---

## Data Preparation — Excel

Before loading into Power BI, the raw data was cleaned and structured in Excel using **Power Query**:

| Step | Action |
|------|--------|
| ✅ Removed duplicates | Identified and eliminated duplicate transaction records |
| ✅ Handled nulls | Filled or flagged missing values in key columns |
| ✅ Standardised formats | Unified date formats, text casing, and currency notation |
| ✅ Split & merged columns | Separated full names, split date into Year/Month/Quarter |
| ✅ Filtered irrelevant records | Removed test entries and out-of-scope data |
| ✅ Created lookup tables | Built dimension tables for Products, Regions, and Salespeople |
| ✅ Data type enforcement | Assigned correct data types (Date, Decimal, Whole Number, Text) |

---

## Data Modelling — Power BI

The data model follows a **Star Schema** design for optimal query performance and DAX simplicity.

```
        ┌─────────────┐
        │  dim_Date   │
        └──────┬──────┘
               │
┌──────────────┼──────────────────┐
│              │                  │
▼              ▼                  ▼
dim_Product  fact_Sales       dim_Region
             (Central)
▲              ▲                  ▲
│              │                  │
└──────────────┼──────────────────┘
               │
        ┌──────┴─────────────┐
        │  dim_Salesperson   │
        └────────────────────┘
```

**Relationships:**
- All dimension tables connect to `fact_Sales` via **one-to-many** relationships
- Cross-filter direction set to **Single** to prevent ambiguous results
- A dedicated **`dim_Date`** table powers all time intelligence functions

---

## DAX Measures

Custom DAX measures were written to power the KPI cards and visuals across all three report pages:

### 💰 Core Revenue Metrics
```dax
$_TotalRevenue = SUM(fact_Sales[Sales Amount])

Units Sold = COUNT(fact_Sales[OrderID])

Average Order Value = DIVIDE([$_TotalRevenue], [Units Sold], 0)

Return Rate % = DIVIDE(SUM(fact_Sales[Returns]), [Units Sold], 0)
```

### 🎯 Sales Performance
```dax
Sales Performance % = 
DIVIDE([Units Sold], SUM(fact_Sales[Target]), 0)

Target Achievement = 
DIVIDE([$_TotalRevenue], SUM(dim_Salesperson[Target]), 0)
```

### 📦 Product Metrics
```dax
Average Price = 
DIVIDE([$_TotalRevenue], [Units Sold], 0)

Revenue by Category = 
CALCULATE(
    [$_TotalRevenue],
    ALLEXCEPT(dim_Product, dim_Product[Category])
)
```

### 📅 Time Intelligence
```dax
Revenue MTD = TOTALMTD([$_TotalRevenue], dim_Date[Date])

Revenue YTD = TOTALYTD([$_TotalRevenue], dim_Date[Date])

Revenue LY = 
CALCULATE([$_TotalRevenue], SAMEPERIODLASTYEAR(dim_Date[Date]))

YoY Growth % = DIVIDE([$_TotalRevenue] - [Revenue LY], [Revenue LY], 0)
```

---

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Microsoft Excel** | Initial data cleaning, Power Query transformations |
| **Power Query (M Language)** | ETL — Extract, Transform, Load |
| **Power BI Desktop** | Data modelling, DAX, dashboard design |
| **DAX (Data Analysis Expressions)** | KPI calculations & performance metrics |

---

## How to Use

### Prerequisites
- [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free) — latest version recommended

### Steps

1. **Clone or download this repository**
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   ```

2. **Open the dashboard file**
   - Launch Power BI Desktop
   - `File` → `Open report` → select `Interactive_Sales_Performance_Dashboard.pbix`

3. **Navigate the report**
   - Use the page navigator at the top: **Executive Summary → Sales → Products**
   - Use the **Month slicer** on any page to filter by time period
   - Click any visual to cross-filter the others on the same page

4. **Refresh data** *(if connecting to a live source)*
   - `Home` → `Refresh`
   - Update credentials under `Transform Data` → `Data source settings` if prompted

---

## File Structure

```
📁 repository-root/
│
├── 📊 Interactive_Sales_Performance_Dashboard.pbix   # Main Power BI report
├── 📄 README.md                                       # Project documentation
│
└── 📁 data/                                           # (Optional) Source data
    ├── raw_sales_data.xlsx                            # Original raw data
    └── cleaned_sales_data.xlsx                       # Post-transformation data
```

---

## 📬 Contact

**Your Name**
- GitHub: [vaatijvk](https://github.com/vaatijvk)
- LinkedIn: [Judith Vaati Kyee](https://linkedin.com/in/judith-vaati)
- Email: judithkyee@gmail.com

---

> ⭐ *If you found this project helpful or interesting, consider giving it a star!*
