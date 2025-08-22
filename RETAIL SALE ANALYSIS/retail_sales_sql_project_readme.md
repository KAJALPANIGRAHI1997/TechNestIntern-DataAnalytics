# Retail Sales Analysis (SQL)

A compact end‑to‑end SQL project that cleans, explores, and analyzes a retail transactions dataset. This repository contains the **DDL**, **data‑quality checks**, and **analysis queries** to answer common business questions like best‑selling months, top customers, and category performance.

---

## 📁 Project Structure

```
├── RETAIL SALE OWN.sql        # All SQL: DDL, cleaning, EDA & analysis queries
├── SQL - Retail Sales Analysis_utf .csv   # Source dataset (CSV)
└── README.md                  # You are here
```

> Tip: Keep your SQL script idempotent (safe to re‑run). The provided script drops/creates the table each run.

---

## 🧰 Tech Stack
- **Database:** PostgreSQL (works with minimal changes on other SQL dialects)
- **Language:** Standard SQL with window functions

---

## 🗃️ Dataset & Schema

**Table:** `retail_sales`

| Column            | Type         | Notes                         |
|-------------------|--------------|-------------------------------|
| `transaction_id`  | INT (PK)     | Unique transaction identifier |
| `sale_date`       | DATE         | Transaction date              |
| `sale_time`       | TIME         | Transaction time              |
| `customer_id`     | INT          | Customer ID                   |
| `gender`          | VARCHAR(15)  | Customer gender               |
| `age`             | INT          | Customer age                  |
| `category`        | VARCHAR(15)  | Product category              |
| `quantity`        | INT          | Units sold                    |
| `price_per_unit`  | FLOAT        | Unit price                    |
| `cogs`            | FLOAT        | Cost of goods sold            |
| `total_sale`      | FLOAT        | Revenue per transaction       |

```sql
DROP TABLE IF EXISTS retail_sales;
CREATE TABLE retail_sales (
  transaction_id INT PRIMARY KEY,
  sale_date DATE,
  sale_time TIME,
  customer_id INT,
  gender VARCHAR(15),
  age INT,
  category VARCHAR(15),
  quantity INT,
  price_per_unit FLOAT,
  cogs FLOAT,
  total_sale FLOAT
);
```

---

## 🚦 How to Run (PostgreSQL)

1. **Create the table**
   - Open `psql` or a GUI (pgAdmin/DBeaver), then run the DDL from `RETAIL SALE OWN.sql` to create `retail_sales`.

2. **Load the CSV** (choose one)
   - Using `psql` (server can access the file path):
     ```sql
     \copy retail_sales
     FROM '/absolute/path/SQL - Retail Sales Analysis_utf .csv'
     WITH (FORMAT csv, HEADER true);
     ```
   - Using **pgAdmin**: *Tools → Import/Export → Import → Select file → Header: Yes → Delimiter: , → Target table: retail_sales → OK*.

3. **Run data‑quality checks** (null scans, row counts) and execute the analysis queries below.

---

## 🧽 Data Quality & Cleaning Checks

```sql
-- Basic counts
SELECT COUNT(*) AS total_rows FROM retail_sales;

-- Null scan across critical fields
SELECT *
FROM retail_sales
WHERE transaction_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR gender IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;

-- Optional: purge bad rows
DELETE FROM retail_sales
WHERE transaction_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR gender IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```

---

## 🔎 Exploratory Queries

```sql
-- Total transactions
SELECT COUNT(*) AS total_sale FROM retail_sales;

-- Unique customers
SELECT COUNT(DISTINCT customer_id) AS unique_customers FROM retail_sales;

-- Category list
SELECT DISTINCT category FROM retail_sales;
```

---

## 📊 Business Questions & SQL Answers

### 1) Sales on a specific date (e.g., 2022‑11‑05)
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```

### 2) Clothing transactions with quantity ≥ 4 in Nov‑2022
```sql
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
  AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
  AND quantity >= 4;
```

### 3) Category‑wise net sales & orders
```sql
SELECT category,
       SUM(total_sale) AS net_sale,
       COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
```

### 4) Average age of Beauty buyers
```sql
SELECT ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';
```

### 5) High‑value transactions (> 1000)
```sql
SELECT *
FROM retail_sales
WHERE total_sale > 1000;
```

### 6) Transactions by gender within each category
```sql
SELECT category,
       gender,
       COUNT(*) AS total_trans
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
```

### 7) Best‑selling month each year (by average sale)
```sql
SELECT year, month, avg_sale
FROM (
  SELECT EXTRACT(YEAR FROM sale_date) AS year,
         EXTRACT(MONTH FROM sale_date) AS month,
         AVG(total_sale) AS avg_sale,
         RANK() OVER (
           PARTITION BY EXTRACT(YEAR FROM sale_date)
           ORDER BY AVG(total_sale) DESC
         ) AS rnk
  FROM retail_sales
  GROUP BY 1, 2
) t
WHERE rnk = 1;
```

### 8) Top 5 customers by total sales
```sql
SELECT customer_id,
       SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```

### 9) Unique customers per category
```sql
SELECT category,
       COUNT(DISTINCT customer_id) AS cnt_unique_cs
FROM retail_sales
GROUP BY category;
```

### 10) Orders by shift (Morning <12, Afternoon 12–17, Evening >17)
```sql
WITH hourly_sale AS (
  SELECT *,
         CASE
           WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
           WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
           ELSE 'Evening'
         END AS shift
  FROM retail_sales
)
SELECT shift,
       COUNT(*) AS total_orders
FROM hourly_sale
GROUP BY shift;
```

---

## 🧠 Notes & Gotchas
- Use `TO_CHAR(sale_date, 'YYYY-MM')` (PostgreSQL) or `FORMAT_DATE`/`DATEPART` equivalents per dialect.
- Window functions like `RANK()` require a proper `PARTITION BY` to scope ranking by year.
- Prefer `NUMERIC` for currency fields if you need exact precision.

---

## ✅ Outcomes
This script gives you:
- Cleaned transactional table
- Quick EDA (counts, distincts, categories)
- Ready‑to‑use analysis queries for reporting and dashboard inputs

---

## 📝 License
MIT — free to use and adapt. Credit appreciated.

---

## 🙌 Author
**Kajal Panigrahi**  
Aspiring Data Analyst | SQL • Power BI • Python • Excel  
Connect: *(add LinkedIn/GitHub links here)*

