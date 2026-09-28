# Retail Project - Forensic Audit

Read-only forensic reconstruction of `D:\Power BI\Retail`. Scope is limited to this project. No external services, Power BI Desktop refresh, database connection, or destructive command was used. No existing project or source file was modified.

## 1. Executive Summary

### Finding
The Retail folder contains a PBIP project named `SCC_Retail`, a PBIR report, a TMDL semantic model, a PBIX binary, six local fact CSVs, an Excel product master, a SQL dimension-insert script, a Python fact-generation script, DAX reference files, documentation, and report/model images.

### Evidence
- `SCC_Retail.pbip`
- `SCC_Retail.Report/definition.pbir`
- `SCC_Retail.SemanticModel/definition.pbism`
- `SCC_Retail.SemanticModel/definition/`
- `README Retail.md`

### Classification
OBSERVED FACT

### Finding
The deployed PBIP semantic-model partitions are Import-mode Power Query/M definitions that navigate to SQL Server `DESKTOP-HATC9ED`, database `RetailBI_Dev`, schema `dbo`. The local CSVs and Python generator are not named as the active PBIP partition source in the TMDL.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/FactSales.tmdl`
- `SCC_Retail.SemanticModel/definition/tables/FactPurchases.tmdl`
- `SCC_Retail.SemanticModel/definition/tables/DimProduct.tmdl`
- `generate_all_facts_v3.py`
- `README Retail.md`

### Classification
OBSERVED FACT

### Finding
The report contains two PBIR pages and 74 visual JSON files: 40 on `Overview` and 34 on `Products and Supplier Analysis`. The second page is marked `HiddenInViewMode`.

### Evidence
- `SCC_Retail.Report/definition/pages/pages.json`
- `SCC_Retail.Report/definition/pages/283e2a46abc63d5194c7/page.json`
- `SCC_Retail.Report/definition/pages/d266936cc4ce01c4215c/page.json`
- `SCC_Retail.Report/definition/pages/*/visuals/*/visual.json`

### Classification
OBSERVED FACT

### Finding
The implemented model and report contain executive financial, sales, cash, inventory/replenishment, dead-stock, product-ranking, and supplier-rate comparison logic. Several supporting DAX definitions describe additional planned or reference measures that are not present in the deployed `_Measures.tmdl`.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/_Measures.tmdl`
- `Page1_DAX_Library.dax`
- `Page2_DAX_Measures.txt`
- `SCC_Retail.Report/definition/pages/*/visuals/*/visual.json`

### Classification
OBSERVED FACT

## Development History & Implementation Boundary

This section adds creator-provided historical context to the local forensic evidence. The historical account explains development sequence and intent; it does not replace the file-based findings about what the current PBIP references.

### Implemented / Actually Built

#### Finding
Creator-provided history states that the Retail scenario was explored while learning, rather than implemented from an existing enterprise system or formal architecture specification. The business problem and synthetic-data approach were discussed with an AI model, which assisted with the approach and provided the Python data-generation script.

#### Evidence
- Creator-provided historical context for this audit amendment.
- `README Retail.md`
- `generate_all_facts_v3.py`

#### Classification
CREATOR-PROVIDED HISTORICAL CONTEXT, supported by forensic evidence that the project contains the documented scenario, Python generator, and generated fact-data artifacts.

#### Finding
Creator-provided history states that Python generated the fact-table data, the generated fact data exists as CSV files, and the dimensions were created/populated separately. The current PBIP then connects to SQL Server, consistent with the TMDL partitions navigating to `DESKTOP-HATC9ED` -> `RetailBI_Dev` -> `dbo` tables.

#### Evidence
- Creator-provided historical context for this audit amendment.
- `generate_all_facts_v3.py`
- `FactSales.csv`, `FactPurchases.csv`, `FactExpenses.csv`, `FactPayables.csv`, `FactReceivables.csv`, `FactPayments.csv`
- `RetailBI_DimInserts.sql`
- `SCC_Retail.SemanticModel/definition/tables/*.tmdl`

#### Classification
CREATOR-PROVIDED HISTORICAL CONTEXT plus OBSERVED FACT. Python is described here as generating fact data, not dimensions.

#### Finding
Creator-provided history states that the generated CSV data was manually imported or uploaded into SQL Server after difficulty getting it directly into SQL Server Management Studio. The current PBIP is SQL Server-backed, while the exact historical role of every CSV after import is not fully remembered.

#### Evidence
- Creator-provided historical context for this audit amendment.
- `SCC_Retail.SemanticModel/definition/tables/FactSales.tmdl`
- `SCC_Retail.SemanticModel/definition/tables/FactPurchases.tmdl`
- `README Retail.md`

#### Classification
CREATOR-PROVIDED HISTORICAL CONTEXT for the manual import; OBSERVED FACT for the current SQL-backed PBIP; UNKNOWN for the exact post-import role of every CSV.

#### Finding
The currently evidenced built solution includes the SQL Server-backed Power BI semantic model, DAX/business logic, and Power BI report. AI assistance is part of the creator-provided development history, not an independent production-system component.

#### Evidence
- Creator-provided historical context for this audit amendment.
- `SCC_Retail.SemanticModel/definition/`
- `SCC_Retail.SemanticModel/definition/tables/_Measures.tmdl`
- `SCC_Retail.Report/definition/`

#### Classification
CREATOR-PROVIDED HISTORICAL CONTEXT plus OBSERVED FACT.

### Designed / Intended but Not Implemented

#### Finding
The original concept included a stock-reconciliation workflow involving system/live database stock, physical stock counting, Power Apps for capturing physical counts, reconciliation between system and physical stock, and identification of stock differences/variance. The creator states that the Power Apps component was not built and that the complete system-stock versus physical-stock reconciliation workflow was not implemented in the current project.

#### Evidence
- Creator-provided historical context for this audit amendment.
- `README Retail.md`: `FactStockReconciliation` is described as schema-only and the Power Apps stock-reconciliation workflow appears in the Phase 2 roadmap.
- No `FactStockReconciliation` TMDL table or Power Apps artifact was found in the current Retail project inventory.

#### Classification
CREATOR-PROVIDED HISTORICAL CONTEXT, supported by forensic evidence of the roadmap/schema-only boundary. NOT IMPLEMENTED in the current project.

#### Finding
Power Apps, physical-stock capture, system-stock versus physical-stock reconciliation, and stock-variance workflow must not be treated as implemented Retail functionality.

#### Evidence
- Creator-provided historical context for this audit amendment.
- `README Retail.md`
- `SCC_Retail.SemanticModel/definition/tables/` inventory

#### Classification
NOT IMPLEMENTED.

### Historical / Not Fully Recoverable

#### Finding
The exact historical role of every CSV after SQL Server import is not known, and the exact historical execution sequence cannot be completely reconstructed from the current artifacts.

#### Evidence
- Creator-provided historical context for this audit amendment.
- `Fact*.csv`
- `generate_all_facts_v3.py`
- `RetailBI_DimInserts.sql`
- SQL-backed partitions in `SCC_Retail.SemanticModel/definition/tables/*.tmdl`

#### Classification
UNKNOWN / HISTORICAL RECONSTRUCTION BOUNDARY.

#### Finding
PBIX/PBIP synchronization remains unknown. Because the project was developed during learning, some supporting artifacts may represent intermediate or reference stages rather than a perfectly synchronized final architecture; this is a reconstruction boundary, not a quality judgment.

#### Evidence
- Creator-provided historical context for this audit amendment.
- `SCC_Retail.pbix`
- `SCC_Retail.pbip`
- `Page1_DAX_Library.dax`
- `Page2_DAX_Measures.txt`
- `README Retail.md`

#### Classification
UNKNOWN / HISTORICAL RECONSTRUCTION BOUNDARY.

## 2. Project Inventory

### Finding
The root inventory is:

| Artifact | Count / status | Apparent purpose | Active/reference status | Evidence |
|---|---:|---|---|---|
| PBIP | 1 | Project entry point | Active project entry point | `SCC_Retail.pbip` |
| PBIR entry | 1 | Report connection and format entry point | Active report definition | `SCC_Retail.Report/definition.pbir` |
| PBIR JSON | 90 JSON files in the project tree, including report/page/visual metadata | Report definition, pages, visuals, bookmarks, resources, and local settings | Report definition files are active project metadata; `.pbi/localSettings.json` is local runtime state | `SCC_Retail.Report/definition/` and `.pbi/localSettings.json` |
| TMDL | 24 files | Semantic-model metadata and measures | Active model metadata | `SCC_Retail.SemanticModel/definition/` |
| TMDL tables | 20 table files | Dimensions, facts, helper tables, and measure table | Active or model-resident objects; helper usage varies | `SCC_Retail.SemanticModel/definition/tables/` |
| PBISM | 1 | Semantic-model project entry point | Active semantic-model entry point | `SCC_Retail.SemanticModel/definition.pbism` |
| PBIX | 1 | Binary Power BI Desktop artifact | Present; synchronization with PBIP is UNKNOWN | `SCC_Retail.pbix` |
| CSV | 6 | Local fact-table data artifacts | Present; direct connection to current PBIP is not established | `FactSales.csv`, `FactPurchases.csv`, `FactExpenses.csv`, `FactReceivables.csv`, `FactPayables.csv`, `FactPayments.csv` |
| Excel | 1 | Product master/source reference | Supporting source artifact; direct PBIP reference is not established | `Retail_BI_Product_Master_v2.xlsx` |
| SQL | 1 | Dimension inserts and date generation | Upstream/manual database population script; not directly referenced by PBIP metadata | `RetailBI_DimInserts.sql` |
| Python | 1 | Fact-data generation and reconciliation | Supporting data-generation script; not referenced by PBIP metadata | `generate_all_facts_v3.py` |
| DAX | 1 | DAX library/reference document | Supporting reference; not the deployed measure store | `Page1_DAX_Library.dax` |
| TXT | 1 | DAX measures/design notes | Supporting reference; not the deployed measure store | `Page2_DAX_Measures.txt` |
| Markdown | 1 | Project description and replication notes | Documentation | `README Retail.md` |
| DOCX | 1 plus a lock file | Case study/documentation | Supporting documentation; DOCX internals not parsed | `Retail_BI_Case_Study.docx`, `~$tail_BI_Case_Study.docx` |
| JPG | 12 | Schema, wireframe, data, gateway, and report screenshots | Supporting visual evidence; image contents not interpreted here | Root `*.JPG` files |
| PNG | 5 | Registered report image resources | Referenced by PBIR report resource packages | `SCC_Retail.Report/StaticResources/RegisteredResources/*.png` |
| JSON themes | 2 | Base and custom report themes | Referenced by report metadata | `SCC_Retail.Report/StaticResources/SharedResources/BaseThemes/CY26SU02.json`, `SCC_Retail.Report/StaticResources/RegisteredResources/Custom5459566171599872.json` |
| `.abf` | 1 | Local model cache/runtime artifact | Runtime/cache artifact; contents not parsed | `SCC_Retail.SemanticModel/.pbi/cache.abf` |

### Classification
OBSERVED FACT. File counts are extension/path inventory counts. Presence alone is not treated as proof of active use.

### Finding
The PBIP entry points to `SCC_Retail.Report`; the report uses a local model path rather than a remote connection.

### Evidence
- `SCC_Retail.pbip`: `artifacts[0].report.path = "SCC_Retail.Report"`
- `SCC_Retail.Report/definition.pbir`: `byPath` reference to `../SCC_Retail.SemanticModel`

### Classification
OBSERVED FACT

### Finding
The following semantic-model tables are present:

- Dimensions: `DimBusinessUnit`, `DimCategory`, `DimCustomer`, `DimDate`, `DimEmployee`, `DimExpenseAccount`, `DimPaymentMethod`, `DimProduct`, `DimShift`, `DimSupplier`.
- Facts: `FactExpenses`, `FactPayables`, `FactPayments`, `FactPurchases`, `FactReceivables`, `FactSales`.
- Helper/parameter/measure tables: `_Measures`, `Rank Parameter`, `SupplierRateComparison`, `Top%2FBottom`.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/*.tmdl`
- `README Retail.md` lists `FactStockReconciliation` as schema-only, but no corresponding deployed TMDL table file was found.

### Classification
OBSERVED FACT

### Finding
The six local CSVs have these observed row counts, column counts, and date-key ranges when read as CSV text:

| File | Rows | Columns | DateKey range observed |
|---|---:|---:|---|
| `FactSales.csv` | 306,518 | 13 | 20230101 to 20241231 |
| `FactPurchases.csv` | 28,177 | 11 | 20230102 to 20241230 |
| `FactExpenses.csv` | 5,429 | 8 | 20230101 to 20241231 |
| `FactPayables.csv` | 408 | 12 | 20230102 to 20241231 |
| `FactReceivables.csv` | 280 | 9 | 20230101 to 20241228 |
| `FactPayments.csv` | 4,386 | 8 | 20230101 to 20241231 |

### Evidence
- The six CSV files listed above; headers were read from the first row and rows were counted locally.

### Classification
OBSERVED FACT

### Finding
`Retail_BI_Product_Master_v2.xlsx` contains a `Product Master` sheet with 456 worksheet rows including its header, 13 columns, and a `Summary` sheet with 23 worksheet rows and 4 columns. The Product Master header includes `ProductCode`, `BusinessUnit`, `Category`, `SubCategory`, `ProductName`, `Variant`, `UnitOfMeasure`, `PackSize`, `SalePriceMin`, `SalePriceMax`, `ReorderLevel`, `IsActive`, and `Notes`.

### Evidence
- `Retail_BI_Product_Master_v2.xlsx`
- Read-only workbook metadata inspection using an installed Python Excel reader.

### Classification
OBSERVED FACT

## 3. Business Purpose

### Finding
The documented business purpose is multi-category retail operations analysis for Shopping Center and Grocery business units. The README describes executive sales/COGS/expense/profit/cash analysis, shift planning, product restocking, dead-stock identification, supplier purchase-rate comparison, product ranking, and margin erosion analysis.

### Evidence
- `README Retail.md`, sections `The Problem`, `What Was Built`, `Business Units in Scope`, and `Patterns embedded in simulation data`.
- `Page1_DAX_Library.dax`
- `Page2_DAX_Measures.txt`
- `_Measures.tmdl`

### Classification
OBSERVED FACT

### Finding
The README describes operational problems including manual POS exports, limited product-revenue visibility, supplier-rate differences, stock-count disruption, and purchase-cost-driven margin erosion.

### Evidence
- `README Retail.md`, section `The Problem`.

### Classification
OBSERVED FACT

### Finding
The report/model evidence supports the inference that the implemented solution is intended to analyze retail financial performance and inventory/purchasing decisions across the two modeled business units.

### Evidence
- `_Measures.tmdl`: `Net Sales`, `COGS`, `Gross Profit`, `Total Expenses`, `Net Profit`, inventory/replenishment, and supplier measures.
- `DimBusinessUnit.tmdl`, `DimProduct.tmdl`, `DimSupplier.tmdl`.
- PBIR visual references to financial, inventory, product, and supplier fields.

### Classification
INFERENCE

### Finding
Whether the local CSV files represent production/operational data, generated test data, or an intermediate export cannot be established from PBIP metadata alone. The README and Python comments explicitly describe two years of simulated data.

### Evidence
- `README Retail.md`: `Two years of simulated data`.
- `generate_all_facts_v3.py`: generation comments and fixed date range.

### Classification
OBSERVED FACT for the documented simulation claim; UNKNOWN for whether the current CSVs were generated by the current script version.

## 4. Source Systems

### Finding
The active model source pattern is SQL Server navigation through Power Query/M. Every physical dimension/fact partition inspected follows the pattern `Sql.Databases("DESKTOP-HATC9ED")`, selects database `RetailBI_Dev`, then navigates to a `dbo` item.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/FactSales.tmdl`, partition `FactSales`.
- `SCC_Retail.SemanticModel/definition/tables/DimProduct.tmdl`, partition `DimProduct`.
- Equivalent partitions in the other physical table TMDL files.

### Classification
OBSERVED FACT

### Finding
The SQL population script targets the same conceptual database/table names used by the M source definitions, but the PBIP does not directly call the SQL script.

### Evidence
- `RetailBI_DimInserts.sql`: inserts into `DimBusinessUnit`, `DimCategory`, `DimProduct`, and other dimensions; date generation for `DimDate`.
- TMDL M partitions: `RetailBI_Dev` and `dbo_<table>` navigation.
- No reference to `RetailBI_DimInserts.sql` was found in PBIP/PBIR/TMDL metadata.

### Classification
OBSERVED FACT

### Finding
The local CSV files are present and structurally resemble the fact tables used by the model, but direct use by the current PBIP is not established.

### Evidence
- CSV headers match the corresponding fact TMDL source-column names.
- TMDL partitions use `Sql.Databases`, not `File.Contents` or `Csv.Document`.

### Classification
OBSERVED FACT

### Finding
The Excel product master is documented as the 455-product source for `DimProduct`, but no direct `Excel.Workbook` or `File.Contents` reference to this workbook appears in the inspected `DimProduct.tmdl` partition.

### Evidence
- `README Retail.md`: repository contents and data-generation instructions.
- `Retail_BI_Product_Master_v2.xlsx`: 455 product data rows inferred from 456 worksheet rows including header.
- `SCC_Retail.SemanticModel/definition/tables/DimProduct.tmdl`: SQL Server partition.

### Classification
OBSERVED FACT for the documentation and TMDL source; UNKNOWN for whether the workbook was used upstream to populate SQL.

### Finding
No external SQL Server connection was attempted, so server/database availability and the actual active production source cannot be confirmed.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/*.tmdl` contains the connection strings.
- No external connection was made during this audit.

### Classification
UNKNOWN

## 5. Data Generation

### Finding
`generate_all_facts_v3.py` is a Python/pandas/numpy generator intended to produce six `_v3.csv` fact outputs from `FactSales.csv`, `FactExpenses.csv`, and `FactReceivables.csv`.

### Evidence
- `generate_all_facts_v3.py`, header comments and Sections 1-6 onward.
- Inputs checked by the script: `FactSales.csv`, `FactExpenses.csv`, `FactReceivables.csv`.
- Header-listed outputs: `FactSales_v3.csv`, `FactPurchases_v3.csv`, `FactPayables_v3.csv`, `FactExpenses_v3.csv`, `FactPayments_v3.csv`, `FactReceivables_v3.csv`.

### Classification
OBSERVED FACT

### Finding
The generator uses fixed seeds: NumPy seed 42, Python `random` seed 42, and a seeded NumPy generator. It sets the generation period to 2023-01-01 through 2024-12-31.

### Evidence
- `generate_all_facts_v3.py`, imports/seeding and `START_DATE` / `END_DATE` configuration.

### Classification
OBSERVED FACT

### Finding
The script derives purchases from monthly sales quantities, applies a 5%-20% purchase buffer, maps products to suppliers, applies target margins and variance, applies premium supplier rates, assigns payment methods, and links credit purchases to payable invoice identifiers.

### Evidence
- `generate_all_facts_v3.py`, Sections 0, 2, 4, and 5.
- Configuration constants: `PURCHASE_BUFFER_MIN`, `PURCHASE_BUFFER_MAX`, `TARGET_MARGIN`, `PREMIUM_SUPPLIER_RATES`, supplier maps, and payment weights.

### Classification
OBSERVED FACT

### Finding
The generator encodes Ramadan/pre-Ramadan purchase periods, payment-method probabilities, daily cash-to-bank banking, expense schedules, opening balances, payable settlement patterns, and eight grocery margin-erosion products with a 0.8% monthly cost increase while sale price remains fixed.

### Evidence
- `generate_all_facts_v3.py`, `RAMADAN_PERIODS`, `DAILY_CASH_BANKING_RATE`, `EXPENSE_SCHEDULE`, `PAYABLE_PATTERNS`, `EROSION_RATE`, and `EROSION_COUNT`.
- `README Retail.md`, `Patterns embedded in simulation data`.

### Classification
OBSERVED FACT

### Finding
The script is reproducible in its pseudo-random configuration, but the current local CSV files cannot be attributed to this exact script run from workspace evidence alone. The script expects/produces `_v3` names while the current root files use non-`_v3` names.

### Evidence
- `generate_all_facts_v3.py`: input/output names and fixed seeds.
- Root files: `FactSales.csv`, `FactPurchases.csv`, `FactExpenses.csv`, `FactPayables.csv`, `FactPayments.csv`, `FactReceivables.csv`.
- No `_v3.csv` files are present in the Retail root inventory.

### Classification
OBSERVED FACT for naming difference; UNKNOWN for provenance of the current CSVs.

### Finding
The generator reads the existing CSV files using relative working-directory paths and is documented for Google Colab execution. That is a local/runtime dependency for reproduction.

### Evidence
- `generate_all_facts_v3.py`: `os.path.exists(f)` and `pd.read_csv(f)` calls.
- Header comments: `HOW TO RUN IN GOOGLE COLAB`.

### Classification
OBSERVED FACT

## 6. Data Transformation / Power Query

### Finding
The physical model partitions use Import mode and direct SQL navigation. The inspected M expressions do not show filters, merges, appends, renames, type conversions, or custom calculated transformations after navigation.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/FactSales.tmdl`, `FactSales` partition.
- Equivalent partition blocks in `Dim*.tmdl` and `Fact*.tmdl` files.

### Classification
OBSERVED FACT

### Finding
The model contains SQL-backed partitions for 17 physical/helper tables: 10 dimensions, 6 fact tables, and `SupplierRateComparison`. `_Measures` uses an embedded empty import table; `Top%2FBottom` uses an embedded two-column import table; `Rank Parameter` is a calculated import table.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/*.tmdl` partition blocks.
- `SupplierRateComparison.tmdl`, `_Measures.tmdl`, `Top%2FBottom.tmdl`, and `Rank Parameter.tmdl`.

### Classification
OBSERVED FACT

### Finding
Query folding cannot be established from the local definitions. The M is simple SQL navigation, but no native query execution, Power Query diagnostic, or server metadata was obtained.

### Evidence
- SQL navigation M expressions in `SCC_Retail.SemanticModel/definition/tables/*.tmdl`.
- No external query or Power Query execution was performed.

### Classification
UNKNOWN

### Finding
The SQL source has a hard-coded machine/server name and database name in the TMDL partitions.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/FactSales.tmdl`: `Sql.Databases("DESKTOP-HATC9ED")` and `RetailBI_Dev`.
- Equivalent source strings in the other SQL-backed table partitions.

### Classification
OBSERVED FACT; reproducibility impact is a POTENTIAL GAP.

## 7. Semantic Model

### Finding
The semantic model contains 20 TMDL table files: 10 dimension tables, 6 fact tables, 3 helper/parameter tables, and one measure table. `_Measures.tmdl` contains 34 measures. `Rank Parameter.tmdl` contains one parameter measure.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/`
- `_Measures.tmdl`
- `Rank Parameter.tmdl`

### Classification
OBSERVED FACT

### Finding
The model uses a star-style architecture as an inference: fact tables connect to shared dimensions such as date, business unit, product, supplier, customer, employee, shift, payment method, and expense account. `DimProduct` connects to `DimCategory`.

### Evidence
- `SCC_Retail.SemanticModel/definition/relationships.tmdl`
- Table definitions under `SCC_Retail.SemanticModel/definition/tables/`

### Classification
INFERENCE

### Finding
Fact table roles and apparent grains are:

| Fact | Apparent grain from columns | Evidence |
|---|---|---|
| `FactSales` | Sales transaction/product line with date, product, BU, employee, shift, hour, quantity, prices, and payment method | `FactSales.tmdl` |
| `FactPurchases` | Purchase line/order with date, product, supplier, BU, invoice, quantity, prices, payment method, and payable invoice | `FactPurchases.tmdl` |
| `FactExpenses` | Expense record with date, BU, expense account, amount, description, reference, and payment method | `FactExpenses.tmdl` |
| `FactReceivables` | Receivable/invoice record with date, due date, customer, BU, invoice and payment amounts, and days outstanding | `FactReceivables.tmdl` |
| `FactPayables` | Payable/invoice record with date, due date, supplier, BU, invoice and payment amounts, payment date/method, and outstanding amount | `FactPayables.tmdl` |
| `FactPayments` | Daily payment-method/business-unit balance record with opening, collected, paid, and closing balances | `FactPayments.tmdl` |

Exact source-system grain and uniqueness constraints are UNKNOWN.

### Classification
INFERENCE from column structure; exact grain UNKNOWN.

### Finding
`relationships.tmdl` declares 25 relationships. Four are explicitly inactive: category-to-business-unit, employee-to-business-unit, expense-account-to-business-unit, and product-to-business-unit. The file does not explicitly serialize cardinality or cross-filter behavior for these relationships.

### Evidence
- `SCC_Retail.SemanticModel/definition/relationships.tmdl`
- `README Retail.md` documents 17 relationships, which differs from the deployed TMDL count.

### Classification
OBSERVED FACT

### Finding
The model has no role files, role declarations, table permissions, calculation groups, calculation items, or object-level security metadata in the inspected TMDL.

### Evidence
- `SCC_Retail.SemanticModel/definition/roles/` absent.
- `SCC_Retail.SemanticModel/definition/relationships.tmdl`
- Recursive search of `SCC_Retail.SemanticModel/definition/*.tmdl` for role and calculation-group declarations.

### Classification
OBSERVED FACT

### Finding
Observed calculated objects are `DimCategory[Category Display]`, `DimDate[Short Month]`, and the `Rank Parameter` calculated table generated with `GENERATESERIES(0, 50, 1)`. No calculated columns were found in fact tables.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/DimCategory.tmdl`
- `SCC_Retail.SemanticModel/definition/tables/DimDate.tmdl`
- `SCC_Retail.SemanticModel/definition/tables/Rank Parameter.tmdl`

### Classification
OBSERVED FACT

### Finding
`SupplierRateComparison` is hidden and all eight of its columns are hidden. It is SQL-backed and has no relationship declaration connecting it to the normal model. The `Estimated Supplier Overpay` measure iterates it directly.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/SupplierRateComparison.tmdl`
- `_Measures.tmdl`: `Estimated Supplier Overpay`
- `relationships.tmdl`: no relationship involving `SupplierRateComparison`

### Classification
OBSERVED FACT

### Finding
`FactPayables[PaymentDate]` is typed as `double` in TMDL. The reason for this type is not established.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/FactPayables.tmdl`

### Classification
OBSERVED FACT for the type; UNKNOWN for intent.

## 8. DAX / Business Logic

### Finding
The deployed measure store is `_Measures.tmdl` and contains 34 measures organized into display folders including `Executive Summary`, `Inventory`, `Sales Analysis`, `Replenishment`, `Supplier & Purchasing`, `Ranking & Parameters`, and `Utility`. No explicit measure descriptions were observed.

### Evidence
- `SCC_Retail.SemanticModel/definition/tables/_Measures.tmdl`

### Classification
OBSERVED FACT

### Finding
Financial logic includes `Net Sales`, `COGS`, `Gross Profit`, `Total Expenses`, `Net Profit`, and `Net Profit %`. `COGS` iterates visible products, sums sales quantity in context, and calculates average purchase cost after removing date filters. `Net Profit %` uses `DIVIDE` with zero alternate result.

### Evidence
- `_Measures.tmdl`, measures `Net Sales`, `COGS`, `Gross Profit`, `Total Expenses`, `Net Profit`, and `Net Profit %`.

### Classification
OBSERVED FACT

### Finding
Cash logic includes separate cash, bank, and wallet closing balances plus `Total Cash Position`. Each closing-balance measure selects the latest `FactPayments[DateKey]` within the selected date-key set for a payment method, then sums the closing balance.

### Evidence
- `_Measures.tmdl`, `Cash Closing Balance`, `Bank Closing Balance`, `Wallet Closing Balance`, and `Total Cash Position`.

### Classification
OBSERVED FACT

### Finding
Inventory and replenishment logic includes cumulative system stock, seven-day quantity sold, seven-day average daily sales, next-week predicted demand, restock quantity, and status categories `Out of Stock`, `Below Reorder`, `Restock This Week`, and `OK`.

### Evidence
- `_Measures.tmdl`, `System Stock Qty`, `Last 7 Days Qty Sold`, `Last 7 Days Avg Daily Sales`, `Next Week Predicted Demand`, `Restock Qty Needed`, and `Restock Alert Status`.

### Classification
OBSERVED FACT

### Finding
Dead-stock logic includes last sale date, days since last sale, aging buckets (`Never Sold`, `90+ Days`, `60-90 Days`, `30-60 Days`, `Active`), inactive product count, and inactive stock value.

### Evidence
- `_Measures.tmdl`, `Last Sale Date`, `Days Since Last Sale`, `Dead Stock Aging Bucket`, `Inactive Products`, and `Inactive Stock Value`.

### Classification
OBSERVED FACT

### Finding
Ranking and product concentration logic includes `Dynamic Rank`, a top/bottom selector from `Top%2FBottom`, a numeric rank parameter, `Condition`, `Product Revenue`, `Total Revenue All Products`, and `Top 10 Products Revenue Share %`.

### Evidence
- `_Measures.tmdl`
- `SCC_Retail.SemanticModel/definition/tables/Top%2FBottom.tmdl`
- `SCC_Retail.SemanticModel/definition/tables/Rank Parameter.tmdl`

### Classification
OBSERVED FACT

### Finding
Supplier analysis includes supplier count per product and estimated overpay calculated from `(AvgUnitPrice - MinPrice) * PurchaseOrders` over the hidden `SupplierRateComparison` table.

### Evidence
- `_Measures.tmdl`, `Supplier Count Per Product` and `Estimated Supplier Overpay`.
- `SupplierRateComparison.tmdl`

### Classification
OBSERVED FACT

### Finding
Supporting DAX files contain more definitions than the deployed measure store. `Page1_DAX_Library.dax` contains 28 reference definitions; `Page2_DAX_Measures.txt` contains 76 reference definitions/design notes. The support files include definitions such as `Gross Profit %`, KPI labels, `Daily Net Sales`, margin-erosion and Pareto logic that are not all present in `_Measures.tmdl`.

### Evidence
- `Page1_DAX_Library.dax`
- `Page2_DAX_Measures.txt`
- `_Measures.tmdl`

### Classification
OBSERVED FACT

### Finding
The DAX support files are not a complete synchronized source of deployed measures. Whether each reference measure was replaced, abandoned, embedded elsewhere, or omitted from the current report cannot be established solely from file names.

### Evidence
- Name comparison between `Page1_DAX_Library.dax`, `Page2_DAX_Measures.txt`, and `_Measures.tmdl`.

### Classification
OBSERVED FACT for the mismatch; UNKNOWN for the reason.

### Finding
No DAX was rewritten or evaluated. Runtime correctness, performance, dependency completeness, and numerical outputs are UNKNOWN.

### Evidence
- Local DAX/TMDL definitions were read only.
- No Power BI Desktop, Tabular Editor, MCP model connection, or external query was used.

### Classification
UNKNOWN

## 9. Report / PBIR

### Finding
The report has two pages:

| Page | Visibility | Visuals | Observable visual types |
|---|---|---:|---|
| `Overview` | Visible | 40 | 3 bar charts, 1 bookmark navigator, 6 cards, 1 card visual, 1 column chart, 5 images, 1 line chart, 1 page navigator, 1 pivot table, 9 shapes, 3 slicers, 1 table, 6 textboxes |
| `Products and Supplier Analysis` | `HiddenInViewMode` | 34 | 1 advanced slicer, 1 bar chart, 6 cards, 1 page navigator, 3 pivot tables, 9 shapes, 6 slicers, 6 textboxes |

### Evidence
- `SCC_Retail.Report/definition/pages/pages.json`
- `SCC_Retail.Report/definition/pages/283e2a46abc63d5194c7/page.json`
- `SCC_Retail.Report/definition/pages/d266936cc4ce01c4215c/page.json`
- Each page's `visuals/*/visual.json` files.

### Classification
OBSERVED FACT

### Finding
`Overview` contains PBIR text/reference evidence for financial measures, cash measures, dates, business-unit/category/expense fields, and `TransactionHour`. The Products page contains evidence for product/supplier, purchase, stock, reorder, recent-sales, predicted-demand, dead-stock, and supplier-overpay logic.

### Evidence
- `SCC_Retail.Report/definition/pages/283e2a46abc63d5194c7/visuals/*/visual.json`
- `SCC_Retail.Report/definition/pages/d266936cc4ce01c4215c/visuals/*/visual.json`
- Direct text-reference counts include `Net Sales`, `COGS`, `Total Expenses`, `Net Profit`, `Net Profit %`, `System Stock Qty`, `Restock`, `Dead Stock`, `Supplier Overpay`, `TransactionHour`, `FactSales`, and `FactPurchases`.

### Classification
OBSERVED FACT

### Finding
Report navigation includes a page navigator on both pages and a bookmark navigator on `Overview`. Three bookmark state files are present; the bookmark metadata identifiers are `41a5ee624ef61b68ef18`, `6ad5489415e524795adb`, and `aadc0167e13f3e5a5e58`. The human-readable intent of each state is not fully established from metadata alone.

### Evidence
- `SCC_Retail.Report/definition/pages/*/visuals/*/visual.json`
- `SCC_Retail.Report/definition/bookmarks/bookmarks.json`
- `SCC_Retail.Report/definition/bookmarks/*.bookmark.json`

### Classification
OBSERVED FACT for the navigators and files; UNKNOWN for complete runtime behavior.

### Finding
Report metadata specifies a `1500 x 1050` canvas with `FitToWidth`, a `CY26SU02` shared base theme, a registered custom theme `Custom5459566171599872.json`, and six registered image resources.

### Evidence
- `SCC_Retail.Report/definition/pages/*/page.json`
- `SCC_Retail.Report/definition/report.json`
- `SCC_Retail.Report/StaticResources/`

### Classification
OBSERVED FACT

### Finding
The report JSON contains slicer/filter and visual interaction metadata, but actual rendered interactions, bookmark behavior, navigation behavior, and field resolution were not tested.

### Evidence
- `SCC_Retail.Report/definition/pages/*/visuals/*/visual.json`
- `SCC_Retail.Report/definition/bookmarks/*.bookmark.json`

### Classification
OBSERVED FACT for metadata presence; UNKNOWN for runtime behavior.

## 10. End-to-End Lineage

### Finding
The evidence-supported current PBIP path is:

```text
SQL Server DESKTOP-HATC9ED / RetailBI_Dev / dbo tables
    -> Power Query/M Sql.Databases navigation
    -> Import-mode TMDL semantic model
    -> 25 model relationships
    -> DAX measures in _Measures.tmdl and helper tables
    -> PBIR visuals on Overview and Products and Supplier Analysis
```

### Evidence
- SQL navigation partitions in `SCC_Retail.SemanticModel/definition/tables/*.tmdl`.
- `SCC_Retail.SemanticModel/definition/relationships.tmdl`.
- `_Measures.tmdl`.
- `SCC_Retail.Report/definition/pages/*/visuals/*/visual.json`.

### Classification
OBSERVED FACT for the file-defined path.

### Finding
A documented upstream/supporting path is:

```text
Retail_BI_Product_Master_v2.xlsx + source fact CSVs
    -> generate_all_facts_v3.py / RetailBI_DimInserts.sql
    -> SQL Server RetailBI_Dev (documented/intended path)
    -> current PBIP SQL partitions
```

The first two stages are documented and present, but the actual execution history and current database contents are UNKNOWN.

### Evidence
- `README Retail.md`, replication steps.
- `generate_all_facts_v3.py`.
- `RetailBI_DimInserts.sql`.
- TMDL SQL partitions.

### Classification
INFERENCE for the combined end-to-end chain; OBSERVED FACT for each documented/file-defined component.

### Finding
The local CSV files are not directly connected to the current PBIP by the inspected M definitions. They may be source-generation inputs, exports, validation artifacts, or a parallel local representation.

### Evidence
- CSV headers and files in the project root.
- TMDL partitions use `Sql.Databases`, not CSV connectors.
- `generate_all_facts_v3.py` reads/writes CSV files.

### Classification
OBSERVED FACT for the separation; UNKNOWN for the intended operational role of the current CSVs.

### Finding
Tenant/workspace downstream lineage was not established. The installed lineage skill requires authenticated service access, and no external connection was approved or attempted.

### Evidence
- `lineage-analysis/SKILL.md` describes service/API requirements.
- No Fabric or Power BI Service API call was made.

### Classification
UNKNOWN

## 11. Analytical Capabilities

### Finding
The following analytical capabilities are actually evidenced in deployed model/report artifacts:

| Capability | Evidence |
|---|---|
| Sales/revenue analysis | `_Measures.tmdl`: `Net Sales`, `Product Revenue`, `Total Revenue All Products`; Overview PBIR references |
| COGS and gross profit | `_Measures.tmdl`: `COGS`, `Gross Profit` |
| Expense and net profit analysis | `_Measures.tmdl`: `Total Expenses`, `Net Profit`, `Net Profit %` |
| Cash position | `_Measures.tmdl`: cash, bank, wallet, and `Total Cash Position` |
| Daily and previous-month sales comparison | `_Measures.tmdl`: `Prev Month Daily Sales`, `Sale diff`; Overview line-chart/report references |
| Peak-hour/transaction-hour analysis | `FactSales.tmdl`: `TransactionHour`; Overview visual references and README |
| Product/category analysis | `DimProduct.tmdl`, `DimCategory.tmdl`, product/category PBIR bindings |
| Inventory approximation | `_Measures.tmdl`: `System Stock Qty`, based on cumulative purchases less sales |
| Restock/replenishment | `_Measures.tmdl`: recent sales, predicted demand, restock quantity, restock status |
| Dead-stock aging | `_Measures.tmdl`: last sale date, days since sale, aging bucket, inactive product/value measures |
| Product ranking and concentration | `_Measures.tmdl`: `Dynamic Rank`, `Condition`, `Top 10 Products Revenue Share %`; parameter tables |
| Supplier comparison/overpay estimate | `SupplierRateComparison.tmdl`; `_Measures.tmdl`: supplier count and estimated overpay |
| Business-unit filtering/titles | `DimBusinessUnit.tmdl`; `_Measures.tmdl`: `Page Title`, `Page 2 Title`; report slicer/filter metadata |

### Classification
OBSERVED FACT

### Finding
Margin erosion, 80/20 distribution, Ramadan/Eid/weekday patterns, and supplier premiums are explicitly encoded in the simulation documentation/generator. Their presence as intended data-generation patterns does not prove that each pattern is quantitatively visible or validated in the current report.

### Evidence
- `README Retail.md`, `Patterns embedded in simulation data`.
- `generate_all_facts_v3.py`, margin erosion, supplier premium, Ramadan, and payment/purchase configuration.
- `Page2_DAX_Measures.txt` for reference logic.

### Classification
OBSERVED FACT for encoded/documented patterns; UNKNOWN for current report validation.

## 12. Technical Architecture

### Confirmed architecture

```text
SQL Server-style source
  -> Power Query/M Sql.Databases navigation
  -> Power BI Import semantic model in TMDL
  -> dimensions/facts/helper tables and 25 relationships
  -> DAX measures in _Measures.tmdl
  -> PBIR report with two pages and 74 visuals
```

Evidence: `SCC_Retail.SemanticModel/definition/tables/*.tmdl`, `relationships.tmdl`, `_Measures.tmdl`, and `SCC_Retail.Report/definition/`.

### Probable/documented upstream architecture

```text
Excel product master + source CSVs
  -> Python simulation/generation and SQL dimension inserts
  -> SQL Server RetailBI_Dev
  -> Power BI SQL Import model
```

Evidence: `README Retail.md`, `generate_all_facts_v3.py`, `RetailBI_DimInserts.sql`, and SQL-backed TMDL partitions.

### Unknown architecture

- Whether the current six CSVs were loaded into the database used by the PBIP.
- Whether the PBIX was generated from the current PBIP state or is a separate revision.
- Whether the SQL Server source is reachable and populated.
- Whether the report was published and, if so, which service workspace/model it uses.

## 13. Data Quality & Reproducibility

### Finding
The six CSVs are readable and contain the expected fact-style headers. Three checked fact keys (`ExpenseKey`, `PayableKey`, and `PaymentKey`) had no duplicate key groups or null key rows in the local scan. Duplicate/null status for the remaining CSV keys was not used as a conclusion because the large-file scan was stopped before completion.

### Evidence
- `FactExpenses.csv`, `FactPayables.csv`, `FactPayments.csv`.
- Read-only CSV import/grouping scan.

### Classification
OBSERVED FACT for the three checked files; UNKNOWN for the remaining files.

### Finding
The local source files show two years of date-key coverage, but date continuity, missing dates, referential integrity against dimensions, numeric outliers, duplicate business transactions, and null values across all fields were not fully established.

### Evidence
- DateKey ranges from the six CSV files.
- No complete referential-integrity or all-column profiling was executed.

### Classification
UNKNOWN

### Finding
The Python generator contains fixed seeds and explicit generation rules, which supports reproducibility when its expected input files, Python environment, and working directory are available.

### Evidence
- `generate_all_facts_v3.py`, seed setup, relative input paths, configuration constants, and output logic.

### Classification
OBSERVED FACT

### Finding
Reproduction depends on external/runtime conditions: Google Colab instructions, relative CSV paths, Python packages (`pandas`, `numpy`), SQL Server availability for the final model, and possibly the original input versions.

### Evidence
- `generate_all_facts_v3.py` header and imports.
- TMDL `Sql.Databases("DESKTOP-HATC9ED")` partitions.

### Classification
OBSERVED FACT; reproducibility impact is a POTENTIAL GAP.

### Finding
No actual refresh, database load, query execution, report rendering, or Power BI model validation was performed. Therefore runtime data quality and refresh outcomes are not established from available artifacts.

### Evidence
- Audit procedure was read-only and local-file based.

### Classification
UNKNOWN

## 14. Gaps / Unknowns

### Confirmed gap

- The README describes `FactStockReconciliation` as schema-only/Phase 2, but no corresponding deployed TMDL table is present: `README Retail.md`; `SCC_Retail.SemanticModel/definition/tables/`.
- README relationship count (`17`) differs from deployed TMDL relationship declarations (`25`): `README Retail.md`; `relationships.tmdl`.
- The PBIP partitions use a hard-coded server name `DESKTOP-HATC9ED`: `SCC_Retail.SemanticModel/definition/tables/*.tmdl`.
- Support DAX contains more/reference definitions than the deployed `_Measures.tmdl`: `Page1_DAX_Library.dax`, `Page2_DAX_Measures.txt`, `_Measures.tmdl`.
- The Excel product master and local CSVs are not direct PBIP partition sources in the inspected TMDL; the active connection is SQL navigation: `DimProduct.tmdl`, `FactSales.tmdl`, and other partitions.
- No RLS role files/declarations were found in the local semantic-model metadata: `SCC_Retail.SemanticModel/definition/`.

### Potential gap

- Current PBIP refresh may depend on a specific local SQL Server machine/database name.
- The PBIX may not be synchronized with the PBIP/TMDL state.
- `FactPayables[PaymentDate]` being typed as `double` may be intentional or may indicate a source/model mismatch; intent is not established.
- The hidden, unconnected `SupplierRateComparison` table may be intentionally pre-aggregated; its refresh/data lineage is not independently verified.
- The current CSVs may be stale, parallel, or generated from a different script revision because the generator uses `_v3` output names while root files do not.

### Unknown

- Actual SQL Server availability, database contents, and refresh success.
- Actual relationship cardinality, cross-filter behavior, key uniqueness in the SQL source, and referential integrity.
- Actual report rendering, visual interaction, slicer behavior, bookmarks, and page navigation at runtime.
- PBIX internal contents and PBIX/PBIP synchronization.
- Service publication, workspace identity, users, usage metrics, and downstream lineage.
- Workbook internal formulas/values beyond read-only sheet dimensions and headers.
- Contents of DOCX, PDF-like exports if any, JPG/PNG visual assets, and binary cache artifacts beyond their file paths.
- Whether every support DAX definition was ever deployed, replaced, or abandoned.

## 15. Portfolio-Relevant Facts

- Power BI PBIP/PBIR/TMDL project named `SCC_Retail`.
- Import-mode semantic model with SQL Server-style Power Query/M partitions targeting `DESKTOP-HATC9ED` / `RetailBI_Dev` / `dbo` tables.
- 10 dimension tables, 6 fact tables, 3 helper/parameter tables, and one `_Measures` table in the deployed TMDL.
- 34 deployed measures in `_Measures.tmdl`, plus one parameter measure in `Rank Parameter.tmdl`.
- 25 relationship declarations, including 4 explicitly inactive relationships.
- Two report pages, 74 PBIR visual files, three bookmark state files, page navigation, bookmark navigation, base/custom themes, and registered image resources.
- Local data artifacts include six fact CSVs, an Excel product master with 455 product data rows, one SQL dimension/date-population script, and one deterministic Python fact-generation script.
- Implemented analytical areas include sales, COGS/profit/expenses, cash position, time comparison, product/category analysis, inventory approximation, replenishment, dead-stock aging, ranking/concentration, and supplier overpay estimation.
- Supporting documentation explicitly describes simulated two-year retail data, Shopping Center and Grocery business units, supplier price variance, margin erosion, seasonality, and peak-hour patterns.
- The project contains both a current PBIP representation and a PBIX binary; synchronization is UNKNOWN.

## 16. Evidence Index

### Project and report

- `SCC_Retail.pbip` - PBIP project entry point and report path.
- `SCC_Retail.Report/definition.pbir` - PBIR report-to-model binding.
- `SCC_Retail.Report/definition/report.json` - themes, resources, report settings.
- `SCC_Retail.Report/definition/pages/pages.json` - page order and active page.
- `SCC_Retail.Report/definition/pages/283e2a46abc63d5194c7/page.json` - Overview metadata.
- `SCC_Retail.Report/definition/pages/d266936cc4ce01c4215c/page.json` - Products and Supplier Analysis metadata and hidden state.
- `SCC_Retail.Report/definition/pages/*/visuals/*/visual.json` - visual types, bindings, filters, titles, and navigation metadata.
- `SCC_Retail.Report/definition/bookmarks/bookmarks.json` - bookmark metadata identifiers.
- `SCC_Retail.Report/definition/bookmarks/*.bookmark.json` - bookmark states.
- `SCC_Retail.Report/StaticResources/` - base/custom themes and registered images.

### Semantic model and DAX

- `SCC_Retail.SemanticModel/definition.pbism` - semantic-model project entry point.
- `SCC_Retail.SemanticModel/definition/model.tmdl` - model metadata and culture/source settings.
- `SCC_Retail.SemanticModel/definition/relationships.tmdl` - relationship declarations and inactive flags.
- `SCC_Retail.SemanticModel/definition/tables/*.tmdl` - table, column, measure, partition, and metadata definitions.
- `SCC_Retail.SemanticModel/definition/tables/_Measures.tmdl` - deployed DAX measure store.
- `SCC_Retail.SemanticModel/definition/tables/DimDate.tmdl` - date columns and `Short Month` calculation.
- `SCC_Retail.SemanticModel/definition/tables/DimProduct.tmdl` - product model columns and SQL partition.
- `SCC_Retail.SemanticModel/definition/tables/FactSales.tmdl` - sales columns and SQL partition.
- `SCC_Retail.SemanticModel/definition/tables/SupplierRateComparison.tmdl` - hidden SQL helper table.
- `SCC_Retail.SemanticModel/definition/tables/Rank Parameter.tmdl` - parameter table/measure.
- `SCC_Retail.SemanticModel/definition/tables/Top%2FBottom.tmdl` - top/bottom helper table.
- `Page1_DAX_Library.dax` - DAX/reference/report-design library.
- `Page2_DAX_Measures.txt` - DAX/reference/design notes.

### Source and generation

- `FactSales.csv` - local sales fact artifact.
- `FactPurchases.csv` - local purchases fact artifact.
- `FactExpenses.csv` - local expenses fact artifact.
- `FactReceivables.csv` - local receivables fact artifact.
- `FactPayables.csv` - local payables fact artifact.
- `FactPayments.csv` - local payment/balance artifact.
- `Retail_BI_Product_Master_v2.xlsx` - product master workbook.
- `RetailBI_DimInserts.sql` - dimension inserts and date generation.
- `generate_all_facts_v3.py` - deterministic fact-generation script.

### Documentation and supporting assets

- `README Retail.md` - stated business purpose, architecture, simulation patterns, replication procedure, and roadmap.
- `Retail_BI_Case_Study.docx` - case-study artifact; internal content not parsed.
- Root `*.JPG` files - schema, wireframe, data, gateway, and screenshot artifacts; image content not evaluated in this audit.
- `SCC_Retail.pbix` - binary Power BI Desktop artifact; internal content not parsed.

### Audit limitations

- This document records local observable evidence only.
- No claims are made that the report renders, refreshes, or produces correct numerical results.
- No claim is made that SQL Server, Power BI Service, or any external source is currently available.
- No service lineage was queried.
