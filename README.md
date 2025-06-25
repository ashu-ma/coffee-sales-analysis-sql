Coffee Shop Sales Performance Analysis with PostgreSQL & Power BI

Project Overview

Analyze coffee shop sales data using PostgreSQL and Power BI to uncover key business insights such as revenue trends, top-selling products, and peak sales periods. This project will provide actionable insights for menu optimization, staffing, and promotional planning.

Tools & Technologies

PostgreSQL

Power BI

CSV Dataset (Coffee Shop Sales)


Business Problem

A coffee shop chain wants to leverage its historical sales data to:

Track overall sales performance.

Identify peak and low sales periods.

Pinpoint best and worst-selling products.

Understand customer purchasing patterns.

The goal is to make data-driven decisions to boost sales, reduce waste, and improve operational efficiency.  

SQL Analysis (PostgreSQL)

Total Revenue
SELECT SUM(total_price) AS total_revenue FROM cofee_sales;

![Total Revenue](https://github.com/user-attachments/assets/1cbb1112-bf65-4f95-87a6-5b96888702a3)

Average Order Value
SELECT SUM(total_price) AS total_revenue FROM cofee_sales;

![Average Order Value](https://github.com/user-attachments/assets/cd17c9c5-f957-4aa6-8eb8-b7b74f5aa331)

Total Items Sold
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS avg_order_value FROM cofee_sales;


SELECT SUM(quantity) AS total_items_sold FROM cofee_sales;
Total Orders:

SELECT COUNT(DISTINCT order_id) AS total_orders FROM cofee_sales;
Average Items per Order:

SELECT SUM(quantity) / COUNT(DISTINCT order_id) AS avg_items_per_order FROM cofee_sales;
Trend Analysis
Weekly Order Distribution:

SELECT to_char(order_date, 'Day') AS weekday, COUNT(DISTINCT order_id) AS orders
FROM cofee_sales 
GROUP BY weekday 
ORDER BY weekday
Monthly Order Trends:

SELECT to_char(order_date, 'Mon') AS month, COUNT(DISTINCT order_id)
FROM cofee_sales 
GROUP BY month 
ORDER BY month;
Category & Size Analysis
Revenue by Category:

SELECT category, SUM(total_price) AS revenue,
ROUND(SUM(total_price) * 100.0 / (SELECT SUM(total_price) FROM coffee_sales), 2) AS percentage
FROM cofee_sales 
GROUP BY category;
Sales by Size:

SELECT size, SUM(quantity) AS units_sold FROM cofee_sales
GROUP BY size
ORDER BY units_sold DESC;
Product Performance
Top 5 Products:

SELECT product_name, SUM(total_price) AS revenue FROM cofee_sales
GROUP BY product_name 
ORDER BY revenue DESC 
LIMIT 5;
Bottom 5 Products:

SELECT product_name, SUM(total_price) AS revenue FROM cofee_sales
GROUP BY product_name 
ORDER BY revenue ASC 
LIMIT 5;
Peak Hour Analysis
Hourly Order Trends:

