# Task6_Sales-Trend-Analysis
# 🧾 Task 6: Sales Trend Analysis Using Aggregations

## 🎯 Objective
The goal of this task is to analyze *monthly revenue* and *order volume* using SQL queries.  
The analysis helps understand sales performance trends over time.

---

## 🛠️ Tools & Technologies Used
- *Database:* SQLite  
- *Interface:* DB Browser for SQLite  
- *Dataset:* Online Sales Data.csv  
- *Database File:* Online_Sales.db  
- *Result File:* sales_trend_screenshot.pdf  

---

## 📊 Dataset Overview
The dataset contains online sales transaction data with the following key columns:
- Transaction ID
- Date
- Product Name
- Units Sold
- Unit Price
- Total Revenue
- Region
- Customer Type
- Payment Method

Rows: *240*  
Columns: *9*

---

## 🧩 Steps Followed

### 1️⃣ Create Database
- Open *DB Browser for SQLite*
- Click *File → New Database*
- Save as Online_Sales.db

### 2️⃣ Import CSV File
- Click *File → Import → Table from CSV file*
- Select Online Sales Data.csv
- Name the table *online_sales*
- Check “First row is column names”
- Click *OK → Finish Import*

### 3️⃣ Verify Data

`SELECT * FROM online_sales LIMIT 10;`

### 💡 SQL Queries Used
#### 🔹 Monthly Revenue and Order Volume

`SELECT 
    strftime('%Y', Date) AS Year,
    strftime('%m', Date) AS Month,
    SUM("Total Revenue") AS Total_Revenue,
    COUNT(DISTINCT "Transaction ID") AS Total_Orders
FROM online_sales
GROUP BY Year, Month
ORDER BY Year, Month;`

#### 🔹 Regional Revenue Analysis

`SELECT 
    Region,
    SUM("Total Revenue") AS Revenue,
    COUNT("Transaction ID") AS Orders
FROM online_sales
GROUP BY Region
ORDER BY Revenue DESC;`

#### 🔹 Top 5 Best-Selling Products

`SELECT 
    "Product Name",
    SUM("Units Sold") AS Total_Units,
    SUM("Total Revenue") AS Revenue
FROM online_sales
GROUP BY "Product Name"
ORDER BY Revenue DESC
LIMIT 5;`

#### 🔹 Create Monthly Sales Trend View

`CREATE VIEW Monthly_Sales_Trend AS
SELECT 
    strftime('%Y-%m', Date) AS Month,
    SUM("Total Revenue") AS Revenue,
    COUNT(DISTINCT "Transaction ID") AS Orders
FROM online_sales
GROUP BY Month
ORDER BY Month;`

#### 🔹 Optimize with Index

`CREATE INDEX idx_date ON online_sales(Date);`

### 📈 Output & Results

- SQL results and tables were captured as screenshots.
- All screenshots are included in the file: sales_trend_screenshot.pdf

#### The analysis shows:

-Peak months for revenue and orders.
-High-performing product categories.
-Regional sales distribution.

### 🧾 Deliverables
-✅ Online_Sales.db – Database file
-✅ sales_trend_screenshot.pdf – Screenshot results
-✅ README.md – Documentation (this file)

