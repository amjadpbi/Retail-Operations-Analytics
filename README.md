# Retail BI â€” Power BI Solution for Multi-Category Retail Operations

**Muhammad Amjad | Power BI Specialist | Pipeline-First**

A complete retail business intelligence solution built from scratch on real operational problems. Two years of simulated data. Two report pages. Every feature maps to a question the business owner actually asks.

---

## The Problem

A multi-category retail store was running blind:

- Weekly manual POS exports, cleaned and formatted by hand
- No visibility into which products drive revenue and which lock up capital
- Same product purchased from multiple suppliers at different rates with no comparison
- Stock counts shutting the business down 3 times in 18 months
- Margin erosion happening silently as purchase costs rose but sale prices did not move

This project replaces all of that with an automated, always-on BI system.

---

## What Was Built

### Page 1 â€” Executive Summary
- Daily sales, COGS, expenses and net profit by business unit
- Cash position across Cash, Bank and Wallet
- Peak hours heatmap for staff shift planning
- Daily sales trend comparing current month vs previous month
- Sales by category with Sale / Profit / Expenses toggle

### Page 2 â€” Products and Supplier Intelligence
- Product restock alert â€” system stock vs reorder level with 7-day predicted demand
- Dead stock alert â€” products with zero sales in 30+ days with capital locked value
- Purchase rate comparison â€” same product, multiple suppliers, rates side by side
- Top and bottom products field parameter for dynamic revenue analysis

---

## Tech Stack

| Layer | Tool |
|---|---|
| Database | SQL Server (On-Premises) |
| Data Simulation | Python in Google Colab |
| Modeling and Reporting | Power BI Desktop |
| Publishing | Power BI Service |

---

## Data Model

Star schema. 7 fact tables. 10 dimension tables. 455 real Pakistani retail products. 24 months of simulated data with embedded business patterns.

**Fact Tables:** FactSales, FactPurchases, FactExpenses, FactReceivables, FactPayables, FactPayments, FactStockReconciliation (schema only, Phase 2)

**Dimension Tables:** DimDate, DimProduct, DimCategory, DimBusinessUnit, DimSupplier, DimCustomer, DimPaymentMethod, DimEmployee, DimShift, DimExpenseAccount

**Patterns embedded in simulation data:**
- Eid spike: 3x Shopping Center volume for 5 days around each Eid
- Ramadan spike: 1.6x Grocery volume across Ramadan period
- Weekend boost: 1.3x both units on Friday and Saturday
- 80/20 distribution: top 20% products at 4x sales weight
- Dead stock: bottom 10% products at near-zero sales weight
- Margin erosion: 8 grocery products with 0.8% monthly cost increase, price unchanged
- Supplier price variance: 3 suppliers charging 3-12% premium for same products
- Peak hours: SC evening 17:00-21:00, GR morning 09:00-12:00 and evening 16:00-19:00

---

## Repository Contents

```
â”œâ”€â”€ RetailBI_DimInserts.sql          # All dimension table INSERT scripts
â”œâ”€â”€ generate_all_facts_v3           # FactTables simulation â€” run in Google Colab
â”œâ”€â”€ data/reference/Retail_BI_Product_Master_v2.xlsx # 455 products â€” source for DimProduct
â”œâ”€â”€ retail_bi_schema                 # Star Schema
â”œâ”€â”€ SCC_Retail.pbix                  # Power BI report file
â”œâ”€â”€ docs/Retail_BI_Case_Study.docx        # Full project case study and learning narrative
â””â”€â”€ data/generated/
    â”œâ”€â”€ FactSales.csv
    â”œâ”€â”€ FactPurchases.csv
    â”œâ”€â”€ FactExpenses.csv
    â”œâ”€â”€ FactReceivables.csv
    â”œâ”€â”€ FactPayables.csv
    â””â”€â”€ FactPayments.csv
```

---

## How to Replicate

**Step 1 â€” Create the database**
Create database `RetailBI_Dev` in SQL Server. Run `RetailBI_DimInserts.sql` in SSMS.

**Step 2 â€” Generate fact data**
Upload `data/reference/Retail_BI_Product_Master_v2.xlsx` and Python scripts to Google Colab. Run each script and download the generated CSV files.

**Step 3 â€” Import CSVs**
Import in this order: FactPurchases, FactExpenses, FactReceivables, FactPayables, FactPayments, FactSales.

**Step 4 â€” Connect Power BI**
Open `SCC_Retail.pbix`. Update the SQL Server connection to your local instance. Verify all 17 table relationships match the schema diagram.

---

## Business Units in Scope

**Shopping Center** â€” Cloth, Readymade Garments, Shoes (Male, Female, Kids)

**Grocery and General Store** â€” Tea, Cooking Oil and Ghee, Rice and Pulses, Spices, Jams and Spreads, Confectionery, Beverages, Formula Milk, Pampers and Kids, Laundry and Cleaning, Personal Care

**Food Point** â€” Excluded from Phase 1. Manual COGS allocation. Phase 2 roadmap.

---

## Phase 2 Roadmap

- **Stock Reconciliation** â€” Power Apps barcode scanning app writing to FactStockReconciliation. Rolling physical counts without business shutdown.
- **Food Point** â€” Recipe-level costing integration for the third business unit.

---

## A Note on How This Was Built

AI assistance was used throughout â€” Python scripts, SQL, DAX, and Power Query. Every output was reviewed, validated and understood before use. The business logic, design decisions, and what to build and what to leave out were entirely my own. AI accelerated execution. It did not replace judgment.

---

## About

Built by Muhammad Amjad â€” Power BI Specialist with 4 years of retail operations experience.

Portfolio: [amjad-bi-portfolio.lovable.app](https://amjad-bi-portfolio.lovable.app)

*Build Solutions. Not Just Dashboards.*

