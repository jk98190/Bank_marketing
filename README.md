# Bank_marketing
# E-Commerce Sales & Customer Analytics — Data Cleaning

Cleaning and preprocessing pipeline for a multi-table e-commerce dataset (~150K orders, 25K customers, 397K order line items, and a 1.1K-product catalog), built as a foundation for downstream analytics, dashboards, and machine learning work.

## Overview

This project takes four raw, related CSV extracts from an e-commerce platform and prepares them for analysis using `pandas`. Each table is cleaned independently — deduplicated, standardized, and validated for referential completeness — before being exported as an analysis-ready CSV.

## Datasets

| File | Description | Rows | Key Columns |
|---|---|---|---|
| `cleaned_Consumer_data.csv` | Customer master data — demographics, location, acquisition cost | ~25,000 | `customer_id`, `customer_name`, `customer_age`, `gender`, `customer_segment`, `region`, `customer_acquisition_cost` |
| `__ecommerce_sales_customer_analytics_150k__1_.csv` | Order-level sales & customer analytics — the core fact table | ~138,000 | `order_id`, `order_date`, `customer_id`, `sales_channel`, `payment_status`, `delivery_status`, `net_sales`, `profit`, `customer_lifetime_value` |
| `order_items_cleaned.csv` | Order line items — product-level detail per order | ~397,000 | `order_id`, `product_id`, `quantity`, `unit_price`, `discount_amount`, `net_sales`, `profit` |
| `product_catalog_cleaned.csv` | Product catalog — category, brand, supplier, pricing | ~1,175 | `product_id`, `product_name`, `product_category`, `product_subcategory`, `brand`, `supplier`, `unit_price`, `product_cost`, `product_rating` |

**Relationships:** `order_items` links to the sales table via `order_id` and to the product catalog via `product_id`; the sales table links to the customer master via `customer_id`.

## Cleaning Process

The pipeline (`File-cleaning.ipynb`) applies a consistent set of steps to each raw table:

1. **Load** the raw CSV with `pandas`.
2. **Remove duplicate rows** with `drop_duplicates()`.
3. **Standardize column names** — strip whitespace, lowercase, replace spaces with underscores.
4. **Trim whitespace** from all text/object columns.
5. **Drop rows missing critical identifiers** (e.g. `customer_id`, `order_id`, `product_id`) to preserve referential integrity across tables.
6. **Export** the cleaned table to a new CSV for downstream use.

## Tech Stack

- Python 3.13
- pandas
- NumPy
- Jupyter Notebook

## Repository Structure

```
├── File-cleaning.ipynb              # Cleaning pipeline (all 4 datasets)
├── cleaned_Consumer_data.csv        # Cleaned customer master
├── order_items_cleaned.csv          # Cleaned order line items
├── product_catalog_cleaned.csv      # Cleaned product catalog
└── __ecommerce_sales_customer_analytics_150k__1_.csv  # Cleaned sales/customer analytics
```

## Next Steps

- Merge tables into a unified analytical dataset (orders + line items + products + customers)
- Exploratory data analysis on sales trends, customer segments, and profitability
- Build dashboards (e.g. Tableau/Power BI or Python-based) on top of the cleaned data
- Feature engineering for churn or CLV prediction models

## Author

Jahaan — BBA Marketing (Analytics minor) student, building a data analytics portfolio.
