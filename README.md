# Pizza Sales Data Analysis

## Introduction

This analysis focuses on deriving insights from pizza sales data extracted from the `pizza_sales` table using SQL queries. The primary goal is to uncover valuable metrics such as total revenue, average order value, total pizzas sold, and more. Additionally, the data is further enhanced through cleaning and visualizing in Excel, providing an interactive and user-friendly exploration of the analyzed information.

## Overview

This SQL script analyzes pizza sales data from the `pizza_sales` table to derive valuable insights into revenue, order trends, and product performance.

## SQL Queries

### Total Revenue
```sql
-- Get total revenue
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
```
### Average Order Value
```sql
-- Calculate average order value
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS Average_Order_Value FROM pizza_sales;
```
### Total Pizzas Sold
```sql
-- Calculate total pizzas sold
SELECT SUM(quantity) AS Total_Pizzas_Sold FROM pizza_sales;
```
### Total Orders
```sql
-- Count total orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;

```
### Average Pizzas Per Order
```sql
-- Calculate average pizzas per order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10, 2)) / CAST(COUNT(DISTINCT order_id) AS DECIMAL(10, 2)) AS DECIMAL(10, 2))
AS Avg_Pizzas_Per_Order
FROM pizza_sales;

```
### Daily Trend for Total Orders
```sql
-- Analyze daily trend for total orders
SELECT DATENAME(DW, order_date) AS Order_Day, COUNT(DISTINCT order_id) AS Total_Orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);

```
### Hourly Trend for Orders
```sql
-- Analyze hourly trend for orders
SELECT DATEPART(HOUR, order_time) AS Order_Hours, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DATEPART(HOUR, order_time)
ORDER BY DATEPART(HOUR, order_time);

```
### Percentage of Sales by Pizza Category
```sql
-- Calculate percentage of sales by pizza category
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10, 2)) AS Total_Revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10, 2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;

```
### Percentage of Sales by Pizza Size
```sql
-- Calculate percentage of sales by pizza size
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10, 2)) AS Total_Revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10, 2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;

```
### Total Pizzas Sold by Pizza Category
```sql
-- Calculate total pizzas sold by pizza category for a specific month (February in this example)
SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;

```
### Top 5 Best Sellers by Total Pizzas Sold

```sql
-- Identify the top 5 best sellers by total pizzas sold
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizzas_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizzas_Sold DESC;

```
### Bottom 5 Best Sellers by Total Pizzas Sold
```sql
-- Identify the bottom 5 best sellers by total pizzas sold
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizzas_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizzas_Sold ASC;

```
## Data Cleaning and Visualization
The analyzed pizza sales data was further cleaned and visualized in Excel, allowing for a more comprehensive and interactive exploration of the insights derived from the SQL analysis. The visualizations in Excel provided a user-friendly interface for interpreting trends, patterns, and key performance indicators in the pizza sales dataset.

## Conclusion

The pizza sales data analysis, conducted through a series of SQL queries, has provided crucial insights into various aspects of the business, including revenue, order trends, and product performance. The subsequent data cleaning and visualization in Excel not only facilitated a clearer interpretation of the findings but also enabled a more interactive exploration of the dataset. This comprehensive approach enhances decision-making processes and provides a solid foundation for future analyses and improvements in pizza sales strategies.
