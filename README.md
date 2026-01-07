# E-Commerce SQL Analysis Project

## Project Overview
This project analyzes customer and order data for an e-commerce business using SQLite. 
The goal is to answer key business questions and generate actionable insights using SQL queries.

## Dataset
The project uses two tables:

### `customers`
| Column        | Description                     |
|---------------|---------------------------------|
| customer_id   | Unique ID for each customer     |
| customer_type | SMB, Mid-Market, or Enterprise |
| city          | Customer's city                 |
| signup_date   | Date customer signed up         |

### `orders`
| Column          | Description                           |
|-----------------|---------------------------------------|
| order_id        | Unique ID for each order               |
| customer_id     | ID of the customer who placed the order |
| order_date      | Date of the order                     |
| product_category| Shoes, Suits, Accessories             |
| order_status    | Delivered, Returned, or Cancelled     |
| order_value     | Value of the order (£)                 |

---

## Business Questions and SQL Queries

### 1. Total revenue from delivered orders
```sql
SELECT SUM(order_value) AS total_revenue
FROM orders
WHERE order_status = 'Delivered';
Question: How much total revenue did the company earn from delivered orders?
Insight: Shows actual revenue, ignoring cancelled or returned orders.

2. Orders per product category
SELECT product_category, COUNT(*) AS total_orders
FROM orders
GROUP BY product_category;


Question: How many orders were placed for each product category?
Insight: Identifies the most popular products by order count.

3. Average order value per product category
SELECT product_category, AVG(order_value) AS avg_order_value
FROM orders
WHERE order_status = 'Delivered'
GROUP BY product_category;


Question: What is the average order value for each product category?
Insight: Shows which products tend to have higher-value orders.

4. Total revenue per product category
SELECT product_category, SUM(order_value) AS total_revenue
FROM orders
WHERE order_status = 'Delivered'
GROUP BY product_category
ORDER BY total_revenue DESC;


Question: How much revenue did each product category generate, and which is the most profitable?
Insight: Identifies the top-performing product category by revenue.

5. Customers with more than 2 orders
SELECT customer_id, COUNT(order_id) AS total_orders
FROM orders
GROUP BY customer_id
HAVING COUNT(order_id) > 2;


Question: Which customers placed more than 2 orders?
Insight: Highlights repeat or loyal customers for possible promotions or loyalty programs.

6. Average order value per customer type
SELECT c.customer_type, AVG(o.order_value) AS avg_order_value
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
WHERE o.order_status = 'Delivered'
GROUP BY c.customer_type;


Question: What is the average order value for each customer type (SMB, Mid-Market, Enterprise)?
Insight: Shows which customer segments tend to place higher-value orders.

7. Monthly orders per product category
SELECT strftime('%Y-%m', order_date) AS month, product_category, COUNT(*) AS total_orders
FROM orders
GROUP BY month, product_category
ORDER BY month, product_category;


Question: How many orders were placed each month for each product category?
Insight: Tracks monthly trends and seasonality for different products.

8. Revenue by customer type
SELECT c.customer_type, SUM(o.order_value) AS total_revenue
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
WHERE o.order_status = 'Delivered'
GROUP BY c.customer_type;


Question: Which customer type generates the most revenue?
Insight: Identifies the most profitable customer segments.

## Summary

This project demonstrates how to analyze e-commerce customer and order data using SQL in SQLite. 
By running these queries, I was able to extract actionable insights such as revenue trends, top-performing products, customer purchasing patterns, and high-value segments.

The project highlights key SQL skills including:
- Aggregation functions (SUM, AVG, COUNT)
- Filtering with WHERE and HAVING
- Grouping data with GROUP BY
- Joining tables to combine customer and order information
- Working with dates and calculating monthly trends

These insights could help a business optimize marketing strategies, focus on profitable customers, and improve product planning.



