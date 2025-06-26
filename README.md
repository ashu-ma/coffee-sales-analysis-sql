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
```
SELECT SUM(total_price) AS total_revenue FROM cofee_sales;
```

![Total Revenue](https://github.com/user-attachments/assets/1cbb1112-bf65-4f95-87a6-5b96888702a3)


Average Order Value
```
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS avg_order_value FROM coffee_sales;
```

![Average Order Value](https://github.com/user-attachments/assets/cd17c9c5-f957-4aa6-8eb8-b7b74f5aa331)


Total Items Sold
```
SELECT SUM(quantity) AS total_items_sold FROM cofee_sales;
```

![Total Items Sold](https://github.com/user-attachments/assets/7fe0738c-cd79-4dca-be2b-f537a1c8d72f)


Total Orders
```
SELECT COUNT(DISTINCT order_id) AS total_orders FROM coffee_sales;
```

![total orders](https://github.com/user-attachments/assets/cade082c-1976-4703-a41d-75c47a91ab36)


Average Items per Order
```
SELECT SUM(quantity)/ COUNT(DISTINCT order_id) AS avg_items_per_order FROM coffee_sales;
```

![aveg items per order](https://github.com/user-attachments/assets/cc6a15ca-f86e-4b25-8e5a-6123ea3fc615)


Weekly Order Distribution
```
SELECT to_char(order_date, 'Day') AS weekday, COUNT(DISTINCT order_id) AS orders
FROM cofee_sales
GROUP BY weekday
ORDER BY weekday;
```

![weekly order distribution](https://github.com/user-attachments/assets/3b56bb35-f7ba-4682-87fa-3823fea074e5)


Monthly Order Trends
```
SELECT to_char(order_date, 'Mon') AS month, COUNT(DISTINCT order_id)
FROM cofee_sales
GROUP BY month
ORDER BY month;
```

![monthly order trend](https://github.com/user-attachments/assets/8b445c00-2b5d-434f-983c-bc0646f01765)


Revenue by Category
```
SELECT category, SUM(total_price) AS revenue,
ROUND(SUM(total_price) * 100.0 / (SELECT SUM(total_price) FROM coffee_sales), 2) AS percentage
FROM cofee_sales
GROUP BY category;
```

![revenue by category](https://github.com/user-attachments/assets/2ef61b61-d60a-42f5-b1ae-4e114583f299)


Sales by Size
```
SELECT size, SUM(quantity) AS units_sold FROM cofee_sales
GROUP BY size
ORDER BY units_sold DESC;
```

![sales by size](https://github.com/user-attachments/assets/6940b18a-2d20-4e67-81a6-579b6ac8c0d0)


Top 5 Products
```
SELECT product_name, SUM(total_price) AS revenue FROM cofee_sales
GROUP BY product_name
ORDER BY revenue DESC
LIMIT 5;
```

![Top 5 products](https://github.com/user-attachments/assets/cf2fc765-b14b-43db-a827-0a9f429a018c)


Bottom 5 Products
```
SELECT product_name, SUM(total_price) AS revenue FROM cofee_sales
GROUP BY product_name
ORDER BY revenue
LIMIT 5;
```

![bottom 5 products](https://github.com/user-attachments/assets/6190c2d8-52a8-4e04-80f2-d48caf8e0443)


Monthly Order Trends
```
SELECT EXTRACT(month FROM order_date) AS month, 
COUNT(DISTINCT order_id) AS order_count
FROM cofee_sales 
GROUP BY month 
ORDER BY month;
```

![peak month analysis](https://github.com/user-attachments/assets/e5e649cd-6fda-4983-b9c7-0f9f44277400)



