# SuperMarket Sales BI – Data Warehouse, ETL & OLAP Cube

An end-to-end Business Intelligence solution on supermarket transaction data, built with the Microsoft BI stack:
**SQL Server → SSIS (ETL) → SSAS (OLAP cube) → MDX → HTML dashboard**.

> Individual project – *Data Warehouse* practicum, Ho Chi Minh City University of Industry and Trade (HUIT), 2026.
> **Author: Nguyen Thu Thao** – designed and built every part of this project on my own.

## Business questions
1. Which **cities and branches** generate the most revenue?
2. Which **product lines** perform best in sales, quantity and gross income?
3. How do **customer segments** (Member vs. Normal, gender) differ in spending?
4. How do sales and gross income change **over time**?
5. Which **payment methods** are used most, and what is the average transaction value?

## Data model (star schema)
| Table | Content |
|---|---|
| `Fact_Sales` | Invoice ID, Sales, Quantity, Unit price, COGS, Gross income, Gross margin %, Tax 5%, Rating |
| `DimBranch` | Branch, City |
| `DimCustomer` | Customer type (Member / Normal), Gender |
| `DimProduct` | Product line |
| `DimDate` / `DimTime` | Purchase date and time |
| `DimPayment` | Payment method (Cash, Credit card, E-wallet) |

Source data: [`data/supermarket_sales.csv`](data/supermarket_sales.csv) (public Kaggle *Supermarket Sales* dataset, ~1,000 invoices).

## Repository structure
```
data/          source CSV
sql/           queries for the staging, dimension and fact tables
ssis/          SSIS project – ETL packages loading staging → data warehouse
ssas/          SSAS multidimensional project – data source view, dimensions, cube
mdx/           MDX queries answering the business questions
database/      SQL Server backup of the Stage_SuperMarket database (.bak)
dashboard/     interactive HTML dashboard (Chart.js + AdminLTE)
practice/      an extra SSIS practice package from the same course
```

## How to run
1. Restore `database/Stage_SuperMarket1.bak` in SQL Server (SSMS → *Restore Database*).
2. Open `ssis/SSIS.sln` in Visual Studio with SQL Server Data Tools (SSIS extension); update the connection managers to your server name; run the packages.
3. Open `ssas/Test3.sln` (Analysis Services extension); update the data source; deploy and process the cube.
4. Run the queries in `mdx/business_questions.mdx` from SSMS against the `Stage Super Market` cube.
5. Open `dashboard/index.html` in a browser.

## Skills demonstrated
Dimensional modeling (Kimball star schema) · ETL with SSIS · OLAP cube design with SSAS · MDX (calculated members, ranking with `ORDER`, cross-joins) · Data validation (duplicate rows after joins, key checks) · Dashboard design

## Tech
SQL Server (T-SQL) · SSIS · SSAS · MDX · Visual Studio (SSDT) · HTML / Chart.js
