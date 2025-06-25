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
Key Metrics
Total Revenue:
![Total Revenue](https://github.com/user-attachments/assets/1cbb1112-bf65-4f95-87a6-5b96888702a3)


SELECT SUM(total_price) AS total_revenue FROM coffee_sales;
Average Order Value:
![Average Order Value](https://github.com/user-attachments/assets/cd17c9c5-f957-4aa6-8eb8-b7b74f5aa331)


SELECT SUM(total_price)::numeric / COUNT(DISTINCT order_id) AS avg_order_value FROM coffee_sales;
Total Items Sold:

SELECT SUM(quantity) AS total_items_sold FROM coffee_sales;
Total Orders:

SELECT COUNT(DISTINCT order_id) AS total_orders FROM coffee_sales;
Average Items per Order:

SELECT SUM(quantity)::numeric / COUNT(DISTINCT order_id) AS avg_items_per_order FROM coffee_sales;
Trend Analysis
Weekly Order Distribution:

SELECT to_char(order_date, 'Day') AS weekday, COUNT(DISTINCT order_id) AS orders
FROM coffee_sales GROUP BY weekday ORDER BY date_part('dow', order_date);
Monthly Order Trends:

SELECT to_char(order_date, 'Mon') AS month, COUNT(DISTINCT order_id)
FROM coffee_sales GROUP BY month ORDER BY date_part('month', order_date);
Category & Size Analysis
Revenue by Category:

SELECT category, SUM(total_price) AS revenue,
ROUND(SUM(total_price) * 100.0 / (SELECT SUM(total_price) FROM coffee_sales), 2) AS percentage
FROM coffee_sales GROUP BY category;
Sales by Size:

SELECT size, SUM(quantity) AS units_sold FROM coffee_sales GROUP BY size ORDER BY units_sold DESC;
Product Performance
Top 5 Products:

SELECT product_name, SUM(total_price) AS revenue FROM coffee_sales
GROUP BY product_name ORDER BY revenue DESC LIMIT 5;
Bottom 5 Products:

SELECT product_name, SUM(total_price) AS revenue FROM coffee_sales
GROUP BY product_name ORDER BY revenue ASC LIMIT 5;
Peak Hour Analysis
Hourly Order Trends:

