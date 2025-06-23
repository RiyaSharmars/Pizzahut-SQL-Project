# 🍕 Pizza Hut Sales Analysis – SQL Project

This project focuses on building and querying a structured SQL database for **Pizza Hut's sales data**. It aims to generate business insights such as revenue trends, best-selling items, order types, and customer preferences using advanced SQL queries.

---

## 🗂️ Project Overview

- **Project Title:** Pizza Hut SQL Sales Analysis
- **Technology:** SQL (MySQL)
- **Domain:** Food & Beverage / Retail
- **Type:** Relational Database + Analytical SQL Queries
- **Data Source:** Sample pizza sales dataset from a Pizza Hut chain

---

## 🎯 Objectives

- Analyze total revenue, average order value, and order frequency
- Identify top-selling pizza types and categories
- Understand distribution of orders by size and day
- Monitor monthly and daily performance
- Provide actionable insights to optimize menu and marketing

---

## 🧱 Database Schema Includes

- `pizzas`: Pizza ID, Name, Size, Price, Category (Classic, Veggie, Chicken)
- `orders`: Order ID, Date, Time
- `order_details`: Order ID, Pizza ID, Quantity
- *(Optional Tables: `customers`, `locations`, `payments`, etc.)*

---

## 🔍 Sample SQL Queries

```sql
-- 1. Total Revenue
SELECT ROUND(SUM(od.quantity * p.price), 2) AS total_revenue
FROM order_details od
JOIN pizzas p ON od.pizza_id = p.pizza_id;

-- 2. Top 5 Best-Selling Pizzas
SELECT p.name, SUM(od.quantity) AS total_sold
FROM order_details od
JOIN pizzas p ON od.pizza_id = p.pizza_id
GROUP BY p.name
ORDER BY total_sold DESC
LIMIT 5;

-- 3. Monthly Sales Trend
SELECT DATE_FORMAT(o.date, '%Y-%m') AS month, SUM(od.quantity * p.price) AS revenue
FROM orders o
JOIN order_details od ON o.order_id = od.order_id
JOIN pizzas p ON od.pizza_id = p.pizza_id
GROUP BY month
ORDER BY month;
