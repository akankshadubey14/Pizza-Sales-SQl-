# Pizza Sales Analysis Project

## Overview

The Pizza Sales Analysis Project is designed to analyze sales data from a fictional pizza restaurant chain. By leveraging SQL for data extraction and transformation, the project provides valuable insights into sales trends, customer preferences, and overall business performance. These insights aim to help the restaurant chain optimize operations, improve sales, and enhance customer satisfaction.

## Project Objectives

- 🔢 Analyze sales trends over time.
- 🍕 Identify top-performing pizzas and categories.
- 📊 Evaluate customer order patterns.
- 💡 Provide actionable insights to improve business performance.

## SQL Queries

The following SQL queries were used to extract and analyze data:

### Data Overview

```sql
-- View the data
SELECT * FROM pizza_sales;
```

### Key Metrics

```sql
-- Total Revenue
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

-- Average Order Value
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS Average_Order_Value FROM pizza_sales;

-- Total Pizzas Sold
SELECT SUM(quantity) AS Total_Pizza_Sold FROM pizza_sales;

-- Total Orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;

-- Average Pizzas Per Order
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) /
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_Pizzas_Per_Order FROM pizza_sales;
```

### Trends Analysis

```sql
-- Daily Trends for Total Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);

-- Monthly Trends for Total Orders
SELECT DATENAME(MONTH, order_date) AS Month_Name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DATENAME(MONTH, order_date)
ORDER BY Total_Orders DESC;
```

### Category and Size Analysis

```sql
-- Percentage of Sales by Pizza Category
SELECT pizza_category, SUM(total_price) AS Total_Sales,
SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS Total_Sales_Percentage
FROM pizza_sales
GROUP BY pizza_category;

-- Percentage of Sales by Pizza Size
SELECT pizza_size, SUM(total_price) AS Total_Sales,
SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS Total_Sales_Percentage
FROM pizza_sales
GROUP BY pizza_size
ORDER BY Total_Sales_Percentage DESC;
```

### Performance Analysis

```sql
-- Total Pizzas Sold by Pizza Category
SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;

-- Top 5 Pizzas by Revenue
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;

-- Bottom 5 Pizzas by Revenue
SELECT TOP 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC;

-- Top 5 Pizzas by Quantity
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;

-- Bottom 5 Pizzas by Quantity
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;

-- Top 5 Pizzas by Total Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC;

-- Bottom 5 Pizzas by Total Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC;
```

## Insights and Recommendations

Based on the analysis, the following insights and recommendations are provided:

- 🔝 **Top Performers**: Focus on promoting the top-selling pizzas to maximize revenue.
- 🚫 **Low Performers**: Reevaluate the offerings of the least popular pizzas to optimize the menu.
- 🍽️ **Category Insights**: Invest in the most profitable pizza categories and sizes.
- 📈 **Trends**: Leverage daily and monthly trends to optimize staffing and inventory.

## Dependencies

- 📊 SQL database or data source for analysis.
- 🔧 Tools for running and managing SQL queries (e.g., SQL Server, MySQL, PostgreSQL).

## Conclusion

This project demonstrates the power of SQL in deriving actionable insights from sales data. By analyzing trends, performance, and customer preferences, businesses can make data-driven decisions to improve their operations and profitability.

Feel free to explore and adapt the provided SQL queries for your own data analysis needs!

