# SQL Exploratory Data Analysis Project

An end-to-end **SQL Server exploratory data analysis (EDA)** project built around a sales data warehouse. The project uses T-SQL to explore business data, calculate key metrics, identify trends, rank products and customers, segment entities, analyze contribution to total sales, and build reusable customer and product reports.

---

## Project Overview

This project focuses on turning a dimensional sales dataset into practical business insights using SQL.

The analysis covers:

- Database and table exploration
- Customer and product dimensions
- Date-range analysis
- Business KPI calculation
- Magnitude analysis
- Product and customer ranking
- Change-over-time analysis
- Cumulative analysis
- Performance analysis
- Customer and product segmentation
- Part-to-whole analysis
- Reusable customer and product reporting views

The repository is organized as a sequence of SQL analysis scripts, progressing from basic exploration toward advanced analytical reporting.

---

## Business Questions Explored

The project answers questions such as:

- How many customers, products, and orders are in the dataset?
- What is the overall sales and quantity sold?
- Which countries have the most customers?
- Which product categories generate the most revenue?
- Which products and customers generate the highest revenue?
- How do sales change over time?
- What are the running sales totals and average trends?
- Which products are performing above or below their historical average?
- Which customers are VIP, Regular, or New?
- Which products are High-Performers, Mid-Range, or Low-Performers?
- What percentage of total revenue comes from each product category?
- What customer and product KPIs can be consolidated into reusable reports?

---

## Data Model

The analysis uses three core tables in the `gold` schema:

### `gold.dim_customers`

Customer-level attributes:

- `customer_key`
- `customer_id`
- `customer_number`
- `first_name`
- `last_name`
- `country`
- `marital_status`
- `gender`
- `birthdate`
- `create_date`

### `gold.dim_products`

Product-level attributes:

- `product_key`
- `product_id`
- `product_number`
- `product_name`
- `category_id`
- `category`
- `subcategory`
- `maintenance`
- `cost`
- `product_line`
- `start_date`

### `gold.fact_sales`

Transaction-level measures:

- `order_number`
- `product_key`
- `customer_key`
- `order_date`
- `shipping_date`
- `due_date`
- `sales_amount`
- `quantity`
- `price`

Relationship:

```text
dim_customers
      |
      | customer_key
      |
      v
fact_sales <---- product_key ----> dim_products
```

---

## Analysis Workflow

```text
Initialize Database
       ↓
Explore Database Structure
       ↓
Explore Dimensions
       ↓
Explore Date Ranges
       ↓
Calculate Business Measures
       ↓
Magnitude Analysis
       ↓
Ranking Analysis
       ↓
Change Over Time
       ↓
Cumulative Analysis
       ↓
Performance Analysis
       ↓
Data Segmentation
       ↓
Part-to-Whole Analysis
       ↓
Customer Report
       ↓
Product Report
```

---

## Analysis Modules

| Script | Analysis |
|---|---|
| `00_init_database.sql` | Creates the database, schema, tables, and loads CSV data |
| `01_database_exploration.sql` | Explores database tables and column metadata |
| `02_dimensions_exploration.sql` | Explores customers, categories, subcategories, and products |
| `03_date_range_exploration.sql` | Examines order and customer date ranges |
| `04_measures_exploration.sql` | Calculates core business KPIs |
| `05_magnitude_analysis.sql` | Measures customers, products, revenue, and quantities by dimensions |
| `06_ranking_analysis.sql` | Ranks top/bottom products and customers |
| `07_change_over_time_analysis.sql` | Analyzes sales trends by year and month |
| `08_cumulative_analysis.sql` | Calculates running totals and moving averages |
| `09_performance_analysis.sql` | Compares yearly product performance and previous-year changes |
| `10_data_segmentation.sql` | Segments products and customers using business rules |
| `11_part_to_whole_analysis.sql` | Calculates category contribution to overall sales |
| `12_report_customers.sql` | Builds a reusable customer analytics view |
| `13_report_products.sql` | Builds a reusable product analytics view |

---

## Key SQL Techniques

This project demonstrates practical SQL Server skills including:

- `SELECT`
- `WHERE`
- `GROUP BY`
- `ORDER BY`
- `DISTINCT`
- `TOP`
- `JOIN` / `LEFT JOIN`
- `CASE`
- `COUNT()`
- `COUNT(DISTINCT ...)`
- `SUM()`
- `AVG()`
- `MIN()`
- `MAX()`
- `DATEDIFF()`
- `DATEPART()`
- `YEAR()`
- `MONTH()`
- `ROW_NUMBER()`
- `RANK()`
- `LAG()`
- `SUM() OVER()`
- `AVG() OVER()`
- `CTE` expressions
- Window functions
- Conditional segmentation
- Part-to-whole calculations
- View creation
- Metadata exploration with `INFORMATION_SCHEMA`

---

## Key Analytical Examples

### Overall Business KPIs

The project calculates:

- Total sales
- Total quantity sold
- Average selling price
- Total orders
- Total products
- Total customers
- Customers who have placed an order

A consolidated KPI query is also included in `04_measures_exploration.sql`.

### Revenue Ranking

The ranking analysis identifies:

- Top 5 products by revenue
- Bottom 5 products by revenue
- Top 10 customers by revenue
- Customers with the fewest orders

It demonstrates both simple `TOP` ranking and window-function-based `RANK()` analysis.

### Time-Series Analysis

`07_change_over_time_analysis.sql` summarizes:

- Sales by year
- Sales by month
- Distinct customers by period
- Quantity sold by period

### Cumulative Analysis

`08_cumulative_analysis.sql` demonstrates:

- Running totals
- Average trends over ordered periods

### Performance Analysis

`09_performance_analysis.sql` uses:

- `LAG()` for previous-year comparison
- `AVG() OVER()` for historical product averages
- Difference calculations
- Above/Below Average classification
- Increase/Decrease/No Change classification

### Customer Segmentation

Customers are grouped using spending and lifespan:

- **VIP**
- **Regular**
- **New Customer**

### Product Segmentation

Products are grouped by cost:

- Below 100
- 100–500
- 500–1000
- Above 1000

Products in the reporting view are additionally classified as:

- High-Performer
- Mid-Range
- Low-Performer

### Part-to-Whole Analysis

`11_part_to_whole_analysis.sql` calculates each product category's:

- Total sales
- Overall sales
- Percentage contribution to total sales

---

## Customer Report

`gold.report_customers` consolidates customer-level KPIs including:

- Customer name and number
- Age group
- Customer segment
- Last order date
- Recency
- Total orders
- Total sales
- Total quantity
- Total products purchased
- Customer lifespan
- Average order value
- Average monthly spend

---

## Product Report

`gold.report_products` consolidates product-level KPIs including:

- Product and category information
- Product cost
- Last sale date
- Recency
- Product performance segment
- Product lifespan
- Total orders
- Total sales
- Total quantity sold
- Total customers
- Average selling price
- Average order revenue
- Average monthly revenue

---

## Project Structure

```text
sql-exploratory-data-analysis-project/
│
├── datasets/
│   ├── source_crm/
│   │   ├── cust_info.csv
│   │   ├── prd_info.csv
│   │   └── sales_details.csv
│   │
│   └── source_erp/
│       ├── CUST_AZ12.csv
│       ├── LOC_A101.csv
│       └── PX_CAT_G1V2.csv
│
├── scripts/
│   ├── 00_init_database.sql
│   ├── 01_database_exploration.sql
│   ├── 02_dimensions_exploration.sql
│   ├── 03_date_range_exploration.sql
│   ├── 04_measures_exploration.sql
│   ├── 05_magnitude_analysis.sql
│   ├── 06_ranking_analysis.sql
│   ├── 07_change_over_time_analysis.sql
│   ├── 08_cumulative_analysis.sql
│   ├── 09_performance_analysis.sql
│   ├── 10_data_segmentation.sql
│   ├── 11_part_to_whole_analysis.sql
│   ├── 12_report_customers.sql
│   └── 13_report_products.sql
│
└── LICENSE
```

---

## How to Run

### Prerequisites

Use:

- Microsoft SQL Server
- SQL Server Management Studio (SSMS)

The project uses SQL Server-specific T-SQL features such as `BULK INSERT`, schemas, views, and window functions.

### 1. Clone the repository

```bash
git clone https://github.com/bhaskar-nb/sql-exploratory-data-analysis-project.git
cd sql-exploratory-data-analysis-project
```

### 2. Initialize the database

Run:

```text
scripts/00_init_database.sql
```

This creates the `DataWarehouseAnalytics` database, the `gold` schema, the three analytical tables, and loads the CSV files.

**Warning:** the script drops and recreates `DataWarehouseAnalytics` if the database already exists.

### 3. Update local CSV paths

Before running the initialization script, update the three `BULK INSERT` paths inside:

```text
scripts/00_init_database.sql
```

The current script contains machine-specific Windows paths from the original development environment.

### 4. Run the analysis scripts

After the database and tables are populated, run the scripts in numerical order:

```text
01 → 02 → 03 → 04 → 05 → 06 → 07 → 08
→ 09 → 10 → 11 → 12 → 13
```

The final two scripts create reusable reporting views:

```text
gold.report_customers
gold.report_products
```

---

## Technologies

- **Database:** Microsoft SQL Server
- **IDE:** SQL Server Management Studio (SSMS)
- **Language:** T-SQL
- **Data Format:** CSV
- **Analysis Type:** Exploratory Data Analysis
- **Model:** Dimensional Sales Model

---

## Skills Demonstrated

This project demonstrates practical Data Analyst and SQL skills:

- SQL querying
- Data exploration
- KPI calculation
- Aggregation
- Data segmentation
- Ranking
- Window functions
- Time-series analysis
- Trend analysis
- Customer analytics
- Product analytics
- Business reporting
- Dimensional data analysis
- Reusable SQL views

---

## Author

**Bhaskar Nakka**

Computer Science Engineering Graduate | Aspiring Data Analyst

Skills demonstrated:
`SQL` • `T-SQL` • `SQL Server` • `EDA` • `Data Analysis` • `Business Analytics` • `Window Functions` • `Data Segmentation` • `Reporting`

---

## License

This project is available under the MIT License. See [LICENSE](LICENSE) for details.
