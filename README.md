# E-commerce-dataanalysis-project
# E-commerce Customer Behavior and Business Insights Analysis

## Overview

This project focuses on understanding how customers shop and how the eCommerce business operates. The goal is to find useful insights to help the business:

- Make customers happier
- Deliver orders faster
- Increase sales

The dataset includes information about:

- When customers placed and received their orders
- How they paid
- What reviews they gave
- Where they are from
- What kind of products they bought

---

## Business Problem

The company wants to improve customer satisfaction, delivery performance, and sales by understanding customer behavior and operational patterns. They face the following challenges:

- Is there a difference in customer purchasing behavior between weekdays and weekends?
- Do customers who pay by credit card give higher review scores?
- How long does it take to deliver pet shop products, and can that be improved?
- Are customers in São Paulo spending more than customers in other cities?
- Does faster delivery lead to better customer reviews?

**Goal:** Find actionable insights to improve payment options, delivery speed, product pricing, and customer satisfaction.

---

## Data Source Information

This project uses the following 9 data files:

- `olist_customer_dataset.csv`
- `olist_geolocation_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_order_payments_dataset.csv`
- `olist_order_reviews_dataset.csv`
- `olist_orders_dataset.csv`
- `olist_sellers_dataset.csv`
- `product_category_name_translation.csv`

---

## Data Cleaning Process

- Remove Unwanted Columns: Identify and delete columns not needed for analysis.
- Remove Duplicates: Eliminate duplicate rows to ensure data accuracy.
- Clean Text in Columns: Use text functions to remove unnecessary words/characters.
- Create a Calendar Table: Build a table containing dates and related info (year, month, day) for easy date analysis.

---

## Data Modeling

![Data Modeling Diagram](https://your-image-link-here.com/data_modeling.png)

*Image: E-commerce data model showing relationships between datasets*

---

## Tools and Technologies Used

- Microsoft Excel
- Power BI
- Tableau
- SQL

---

## Key Insights Included

- Total payments
- Total number of orders
- Average price in São Paulo city
- Orders with 5-star reviews paid by credit card
- Average delivery days for Pet Shop category
- Shipping days vs. review score analysis

---

## Excel

### 📊 Excel Dashboard Features

- Created clear KPIs using Pivot Tables to highlight key business insights.
- Developed a user-friendly, easy-to-read dashboard layout.
- Implemented interactive slicers for smooth data filtering.
- Linked slicers to charts and KPIs for dynamic updates.
- Made the dashboard fully interactive for easy data exploration.

### Dashboard Image

![Excel Dashboard](https://your-image-link-here.com/excel_dashboard.png)

---

## ✅ What I Learned from Excel

- Improved data modeling and data structure skills.
- Created calendar tables using date and time functions.
- Enhanced knowledge of text functions for data cleaning.
- Improved Pivot Tables and chart design skills.
- Learned to track KPIs with interactive visuals.
- Gained experience in building user-friendly dashboards.

---

## What I Did in Excel

- Imported 9 CSV files into Power Query for preparation.
- Created Calendar Table with Year, Month Number, Month Name, Quarter Number, Weekday Number, and Weekday Name/Status.
- Used data modeling to connect all files with proper relationships.
- Applied text functions in Power Query for column cleaning.
- Analyzed data to define KPIs.
- Built Pivot Tables and charts to summarize insights.
- Designed and created an interactive dashboard.

---

## Power BI

### Dashboard Features

- Clean, colorful visualizations
- Interactive reports with filters and slicers
- Documentation explaining design and data sources
- Sample datasets used in reports

### Dashboard Image

![Power BI Dashboard](https://your-image-link-here.com/powerbi_dashboard.png)

---

## What I Did in Power BI

- Combined data from 9 files into a single data model.
- Built calendar tables using the CALENDARAUTO() DAX function.
- Used DAX formulas to calculate KPIs.
- Designed visual charts and dashboards.
- Added filters and slicers for improved interaction.

---

## What I Learned from Power BI

- Strong understanding of data modeling (star and snowflake schemas).
- Proficient in calendar tables for time intelligence.
- Expertise in efficient DAX formulas for KPIs and trends.
- Handling complex measures with CALCULATE, FILTER, and advanced DAX.
- Optimizing Power BI models for performance.
- Building interactive dashboards tailored to business needs.
- Understanding relationships, filter, and row contexts in DAX.

---

## Tableau

### Tableau Dashboard Features

- Combined multiple charts and graphs in dashboards.
- Used LOD (Level of Detail) expressions for KPIs.
- Added filters to focus on data subsets.
- Created interactive dashboards for user exploration.
- Designed simple, user-friendly dashboards.

### Dashboard Image

![Tableau Dashboard](https://your-image-link-here.com/tableau_dashboard.png)

---

## What I Learned from Tableau

- Improved data modeling skills.
- Enhanced calendar tables with calculated fields.
- Better understanding of LOD expressions.
- Developed skills for creating effective interactive dashboards.

---

## What I Did in Tableau

- Imported 8 files as data sources.
- Connected files using data modeling techniques.
- Created a data model linking tables.
- Built a calendar table with date and time functions.
- Analyzed KPIs.
- Created various charts for visualization.
- Developed interactive dashboards with filters.
- Created calculated measures and used LOD expressions.

---

## SQL

### What I Did

- Imported 8 data files into the SQL database.
- Created calendar tables using SQL date/time functions.
- Developed queries to track KPIs.

### What I Learned

- Improved calendar and date/time functions skills in SQL.
- Enhanced understanding of JOIN operations and query execution order.

---

## Sample SQL Queries

```sql
-- Total payment amount (in millions)
SELECT CONCAT(ROUND((SUM(payment_value)/1000000), 2), " M") AS "Total Amount / Total Payment Amount"
FROM olist_order_payment_dataset;

-- Number of Orders with 5-star reviews paid by credit card
SELECT
  reviews.review_score,
  payment.payment_type,
  CONCAT(ROUND(COUNT(orders.order_id)/1000, 0), " K") AS "total no of orders"
FROM olist_order_review_dataset AS reviews
LEFT JOIN olist_order_payment_dataset AS payment
  ON reviews.order_id = payment.order_id
RIGHT JOIN olist_orders_dataset AS orders
  ON reviews.order_id = orders.order_id
WHERE payment.payment_type = "credit_card" AND reviews.review_score = "5"
GROUP BY reviews.review_score;

-- Average delivery days for Pet Shop products
SELECT AVG(DATEDIFF(
  STR_TO_DATE(order_delivered_customer_date, "%d-%m-%y"),
  STR_TO_DATE(order_purchase_timestamp, "%d-%m-%y"))) AS "avg days of delivery"
FROM olist_orders_dataset AS orders
LEFT JOIN olist_order_items_dataset AS product
  ON orders.order_id = product.order_id
WHERE product.product_category_name = "pet_shop";
