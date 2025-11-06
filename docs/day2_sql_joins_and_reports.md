# 🗓️ Day 2 — SQL Core: Queries, Filtering, Sorting & Joins

**Goal:**  
Understand how to explore, combine, and analyze data using `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, and various types of `JOIN`.

---

## 🧩 Setup Check
Connected to PostgreSQL database:

```sql
\c retailx
🧱 Tables Used
customers
Column	Type	Description
customer_id	SERIAL PRIMARY KEY	Unique ID
first_name	VARCHAR(50)	Customer first name
last_name	VARCHAR(50)	Customer last name
email	VARCHAR(100)	Unique email
city	VARCHAR(50)	City name
country	VARCHAR(50)	Country
created_at	TIMESTAMP	Default current timestamp
orders
Column	Type	Description
order_id	SERIAL PRIMARY KEY	Unique order ID
customer_id	INT FK	References customers
amount	DECIMAL(10,2)	Order value
status	VARCHAR(20)	Order status
order_date	DATE	Order creation date
🧮 Sample Data

Inserted base records for testing:

INSERT INTO customers (first_name, last_name, email, city, country)
VALUES
('John', 'Smith', 'john.smith@example.com', 'New York', 'USA'),
('Emma', 'Jones', 'emma.jones@example.com', 'London', 'UK'),
('Carlos', 'Diaz', 'carlos.diaz@example.com', 'Madrid', 'Spain'),
('Anita', 'Rao', 'anita.rao@example.com', 'Bangalore', 'India'),
('Sven', 'Larsson', 'sven.larsson@example.com', 'Stockholm', 'Sweden'),
('Ivy', 'Chen', 'ivy.chen@example.com', 'Berlin', 'Germany');

INSERT INTO orders (customer_id, amount, status, order_date)
VALUES
(1, 120.50, 'Shipped', '2025-02-01'),
(2, 75.00, 'Pending', '2025-02-10'),
(3, 240.00, 'Delivered', '2025-02-15'),
(4, 315.99, 'Cancelled', '2025-02-20'),
(5, 150.25, 'Delivered', '2025-02-25');

🔍 Core Queries
1️⃣ Basic Join
SELECT 
    c.customer_id,
    c.first_name,
    o.order_id,
    o.amount,
    o.status
FROM customers c
INNER JOIN orders o
    ON c.customer_id = o.customer_id;

2️⃣ Delivered Orders Above $100
SELECT 
    c.first_name,
    c.country,
    o.amount,
    o.status
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.status = 'Delivered' 
  AND o.amount > 100
ORDER BY o.amount DESC;

3️⃣ Total Spend per Customer
SELECT
    c.customer_id,
    c.first_name,
    SUM(o.amount) AS total_spent,
    COUNT(o.order_id) AS total_orders
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.first_name
ORDER BY total_spent DESC;

4️⃣ Revenue by Country
SELECT
    c.country,
    SUM(o.amount) AS total_sales,
    COUNT(o.order_id) AS num_orders
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.country
ORDER BY total_sales DESC;

5️⃣ Customers With No Orders
SELECT
    c.first_name,
    c.country,
    o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;

6️⃣ High-Value Customers (spend > $200)
SELECT
    c.country,
    c.first_name,
    SUM(o.amount) AS total_spent
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.country, c.first_name
HAVING SUM(o.amount) > 200
ORDER BY total_spent DESC;

🧠 Key Learnings
Concept	Description
INNER JOIN	Only matching rows in both tables
LEFT JOIN	All from left, NULL where right missing
RIGHT JOIN	All from right, NULL where left missing
FULL OUTER JOIN	All from both sides
CROSS JOIN	Cartesian product (all combinations)
GROUP BY + HAVING	Aggregate and filter aggregated results
SELECT *	Retrieve all columns from both sides