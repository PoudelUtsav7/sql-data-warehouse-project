# SQL Data Warehouse Project

A SQL Server data warehouse project that integrates **CRM and ERP data** and transforms raw CSV files into clean, business-ready datasets for analytics.

## Architecture

This project follows a **Medallion Architecture (Bronze → Silver → Gold)**:

<img width="1028" height="341" alt="image" src="https://github.com/user-attachments/assets/386804e4-e55f-453c-b06c-d6dc01e8c8ec" />

### Bronze Layer

Stores raw CRM and ERP data loaded directly from CSV files using `BULK INSERT`.

### Silver Layer

Cleans and transforms the Bronze data by handling duplicates, missing values, inconsistent formats, invalid dates, and standardizing fields such as gender, marital status, and country.

### Gold Layer

Combines the cleaned data into a **star schema** consisting of:

* `gold.dim_customers`
* `gold.dim_products`
* `gold.fact_sales`

The Gold layer is designed to provide business-ready data for analytics and reporting.

## Project Structure

```text
sql-data-warehouse-project/
│
├── datasets/
│   ├── source_crm/
│   └── source_erp/
│
├── scripts/
│   ├── bronze/
│   │   ├── ddl_bronze.sql
│   │   └── proc_load_bronze.sql
│   │
│   ├── silver/
│   │   ├── ddl_silver.sql
│   │   └── proc_load_silver.sql
│   │
│   └── gold/
│       └── ddl_gold.sql
│
└── README.md
```

## How to Run

1. Create the `DataWarehouse` database and `bronze`, `silver`, and `gold` schemas.
2. Run the Bronze DDL script.
3. Update the CSV file paths in the Bronze loading procedure.
4. Run:

```sql
EXEC bronze.load_bronze;
```

5. Run the Silver DDL script and then:

```sql
EXEC silver.load_silver;
```

6. Run the Gold DDL script to create the final views.

The resulting Gold views can then be queried for analysis and reporting.

## Project Goal

The main goal of this project was to practice building a complete **end-to-end SQL data warehouse**, from raw data ingestion and transformation to dimensional modeling and analytics-ready data.
