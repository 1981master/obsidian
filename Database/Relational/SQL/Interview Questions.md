# ⭐ SECTION 1 — BASIC SELECT & FILTERS (Questions 1–10)

---

## **1. Select all rows from a table**

`SELECT * FROM customer;`

---

## **2. Select specific columns**

`SELECT first_name, last_name, email FROM customer;`

---

## **3. Filter using WHERE**

`SELECT * FROM customer WHERE city = 'Austin';`

### Output:

Alice Johnson

---

## **4. Use AND / OR**

`SELECT * FROM customer WHERE city = 'Austin' OR city = 'Dallas';`

---

## **5. Use LIKE for partial search**

`SELECT * FROM customer WHERE email LIKE '%mail.com';`

---

## **6. Find customers created this year**

`SELECT * FROM customer WHERE YEAR(created_at) = YEAR(NOW());`

---

## **7. Sorting results**

`SELECT first_name, salary FROM employee ORDER BY salary DESC;`

---

## **8. Remove duplicates**

`SELECT DISTINCT city FROM customer;`

---

## **9. Limit results**

`SELECT * FROM customer LIMIT 2;`

---

## **10. Mathematical operations**

`SELECT item_name, sale_price - cost_price AS profit FROM item;`

---

# ⭐ SECTION 2 — AGGREGATIONS & GROUP BY (Questions 11–20)

---

## **11. Count records**

`SELECT COUNT(*) FROM employee;`

---

## **12. Count employees per store**

`SELECT store_id, COUNT(*) AS num_employees FROM employee GROUP BY store_id;`

---

## **13. Sum of salaries per store**

`SELECT store_id, SUM(salary) AS total_salary FROM employee GROUP BY store_id;`

---

## **14. Average salary**

`SELECT AVG(salary) FROM employee;`

---

## **15. Max salary**

`SELECT MAX(salary) FROM employee;`

---

## **16. Min salary per store**

`SELECT store_id, MIN(salary) FROM employee GROUP BY store_id;`

---

## **17. Group by multiple fields**

`SELECT store_id, position, COUNT(*) FROM employee GROUP BY store_id, position;`

---

## **18. HAVING clause**

(Get stores with more than 1 employee)

`SELECT store_id, COUNT(*) FROM employee GROUP BY store_id HAVING COUNT(*) > 1;`

---

## **19. Average sale per payment method**

`SELECT payment_method, AVG(total_amount) FROM sale GROUP BY payment_method;`

---

## **20. Highest sale per store**

`SELECT store_id, MAX(total_amount) FROM sale GROUP BY store_id;`

---

# ⭐ SECTION 3 — JOINS (Questions 21–30)

---

## **21. Inner join**

`SELECT c.first_name, s.total_amount FROM customer c JOIN sale s ON c.customer_id = s.customer_id;`

---

## **22. Left join**

`SELECT c.first_name, s.total_amount FROM customer c LEFT JOIN sale s ON c.customer_id = s.customer_id;`

---

## **23. Right join**

(MySQL supports it)

`SELECT s.store_name, e.first_name FROM store s RIGHT JOIN employee e ON s.store_id = e.store_id;`

---

## **24. Full join**

(Works in PostgreSQL / Oracle)

`SELECT * FROM customer FULL OUTER JOIN sale ON customer.customer_id = sale.customer_id;`

---

## **25. Joining 3 tables**

`SELECT c.first_name, i.item_name, si.total_price FROM customer c JOIN sale s ON c.customer_id = s.customer_id JOIN sale_item si ON s.sale_id = si.sale_id JOIN item i ON si.item_id = i.item_id;`

---

## **26. Employees with manager names**

`SELECT e.first_name AS employee, m.first_name AS manager FROM employee e LEFT JOIN employee m ON e.manager_id = m.employee_id;`

---

## **27. Show store + manager name**

`SELECT s.store_name, e.first_name AS manager FROM store s JOIN employee e ON s.store_id = e.store_id WHERE e.position = 'Manager';`

---

## **28. Items with store info**

`SELECT i.item_name, s.store_name FROM item i JOIN store s ON i.store_id = s.store_id;`

---

## **29. Sales with customer + store**

`SELECT c.first_name, s2.store_name, s.total_amount FROM sale s JOIN customer c ON s.customer_id = c.customer_id JOIN store s2 ON s.store_id = s2.store_id;`

---

## **30. Items and categories sold**

`SELECT i.category, COUNT(*) FROM sale_item si JOIN item i ON si.item_id = i.item_id GROUP BY category;`

---

# ⭐ Pause here to avoid message cutoff.

## ✔ READY FOR SECTION 4 → 10?

This includes:

### Section 4 — Subqueries

### Section 5 — Window Functions (Rank, Row_Number, Lead/Lag)

### Section 6 — CTE, Views

### Section 7 — DDL, Indexes, Keys

### Section 8 — Transactions, ACID

### Section 9 — Performance Tuning

### Section 10 — Advanced Analytics & Interview Puzzles

Reply:  
👉 **“Continue”** to get Questions **31–100**.

##### You said:

👉 “Continue” to get Questions 31–100.

###### ChatGPT said:

Nice — continuing with **Questions 31–100** (Sections 4–10). Each item has the **question**, the **SQL answer**, and a small **example output** (where applicable, using your schema). I kept queries portable across common RDBMS where possible and noted dialect differences when necessary.

---

# #️⃣ SECTION 4 — SUBQUERIES & CORRELATED QUERIES (31–40)

### 31. Find customers who made at least one purchase

`SELECT c.* FROM customer c WHERE EXISTS (   SELECT 1 FROM sale s WHERE s.customer_id = c.customer_id );`

**Output (example):** Alice, Bob, Charlie (all three have sales)

---

### 32. Customers who made more than 1 purchase

`SELECT c.customer_id, c.first_name, COUNT(s.sale_id) AS purchases FROM customer c JOIN sale s ON c.customer_id = s.customer_id GROUP BY c.customer_id, c.first_name HAVING COUNT(s.sale_id) > 1;`

**Output:** none in current data (all have ≤1)

---

### 33. Items with sale price greater than average sale_price

`SELECT item_id, item_name, sale_price FROM item WHERE sale_price > (SELECT AVG(sale_price) FROM item);`

**Output:** iPhone 14 (if above avg)

---

### 34. Correlated subquery — last sale date per customer

`SELECT c.customer_id, c.first_name,   (SELECT MAX(sale_date) FROM sale s WHERE s.customer_id = c.customer_id) AS last_sale FROM customer c;`

**Output:** last_sale values or NULL

---

### 35. Delete items never sold (safe delete check)

`DELETE FROM item WHERE item_id NOT IN (SELECT item_id FROM sale_item);`

**Output:** (rows removed) — none in current data

---

### 36. Update item price using subquery (increase cheapest store items)

`UPDATE item SET sale_price = sale_price * 1.10 WHERE sale_price = (SELECT MIN(sale_price) FROM item);`

**Output:** updated rows

---

### 37. Find stores where average employee salary > X using HAVING with subquery

`SELECT store_id, AVG(salary) AS avg_salary FROM employee GROUP BY store_id HAVING AVG(salary) > 50000;`

**Output:** store 2 (if avg > 50k because of Moh)

---

### 38. Select items whose store is OPEN (subquery on store table)

`SELECT i.item_id, i.item_name FROM item i WHERE i.store_id IN (SELECT store_id FROM store WHERE status = 'OPEN');`

**Output:** items in stores with status OPEN

---

### 39. Correlated: get count of items per store next to store row

`SELECT s.store_id, s.store_name,        (SELECT COUNT(*) FROM item i WHERE i.store_id = s.store_id) AS items_count FROM store s;`

**Output:** store + items_count

---

### 40. Use scalar subquery in SELECT (max salary overall)

`SELECT e.first_name, e.salary,        (SELECT MAX(salary) FROM employee) AS max_salary_overall FROM employee e;`

**Output:** each row plus max_salary_overall

---

# #️⃣ SECTION 5 — WINDOW FUNCTIONS & ANALYTICS (41–50)

### 41. Highest paid per store using ROW_NUMBER (single row each)

`SELECT store_id, first_name, last_name, salary FROM (   SELECT e.*, ROW_NUMBER() OVER(PARTITION BY store_id ORDER BY salary DESC) AS rn   FROM employee e ) t WHERE rn = 1;`

**Output:** Sam (store 1), Moh (store 2)

---

### 42. Top 2 salaries per store

`SELECT * FROM (   SELECT e.*, ROW_NUMBER() OVER(PARTITION BY store_id ORDER BY salary DESC) AS rn   FROM employee e ) t WHERE rn <= 2 ORDER BY store_id, rn;`

**Output:** up to 2 rows per store

---

### 43. Cumulative salary per store ordered by hire_date

`SELECT employee_id, first_name, store_id, salary,        SUM(salary) OVER(PARTITION BY store_id ORDER BY hire_date                         ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total FROM employee;`

**Output:** running_total column per row

---

### 44. Row count per partition (employees per store) with window

`SELECT *, COUNT(*) OVER(PARTITION BY store_id) AS employees_in_store FROM employee;`

**Output:** each row with employees_in_store = 2 for both stores

---

### 45. Use LEAD to compare salary with next lower salary in same store

`SELECT first_name, store_id, salary,        LEAD(salary) OVER(PARTITION BY store_id ORDER BY salary DESC) AS next_salary FROM employee;`

**Output:** next_salary shows next row's salary or NULL

---

### 46. Use LAG to compute salary difference with previous row

`SELECT first_name, store_id, salary,        salary - LAG(salary) OVER(PARTITION BY store_id ORDER BY salary DESC) AS diff_from_prev FROM employee;`

**Output:** diff_from_prev per row (NULL for first in each partition)

---

### 47. NTILE(4) — quartile buckets by salary company-wide

`SELECT first_name, salary,        NTILE(4) OVER(ORDER BY salary DESC) AS quartile FROM employee;`

**Output:** bucket numbers 1..4

---

### 48. Use FIRST_VALUE to get top salary per store (repeated)

`SELECT first_name, store_id, salary,        FIRST_VALUE(salary) OVER(PARTITION BY store_id ORDER BY salary DESC) AS top_salary FROM employee;`

**Output:** each row shows top_salary for its store

---

### 49. DENSE_RANK to list ranks without gaps

`SELECT first_name, store_id, salary,        DENSE_RANK() OVER(PARTITION BY store_id ORDER BY salary DESC) AS dr FROM employee;`

**Output:** dr = 1,2,...

---

### 50. PERCENT_RANK & CUME_DIST examples (statistical)

`SELECT first_name, salary,        PERCENT_RANK() OVER(ORDER BY salary DESC) AS percent_rank,        CUME_DIST() OVER(ORDER BY salary DESC) AS cume_dist FROM employee;`

**Output:** numeric distribution values between 0..1

---

# #️⃣ SECTION 6 — CTEs, RECURSIVE CTE, VIEWS (51–60)

### 51. Simple CTE (readable step)

`WITH store_items AS (   SELECT store_id, COUNT(*) AS cnt FROM item GROUP BY store_id ) SELECT s.store_id, s.store_name, si.cnt FROM store s LEFT JOIN store_items si ON s.store_id = si.store_id;`

**Output:** store with item counts

---

### 52. Recursive CTE — generate series (numbers 1..10) (Postgres / SQL Server / MySQL 8)

`WITH RECURSIVE nums AS (   SELECT 1 AS n   UNION ALL   SELECT n+1 FROM nums WHERE n < 10 ) SELECT * FROM nums;`

**Output:** numbers 1..10

---

### 53. Recursive CTE for org chart (employees -> managers) example

`WITH RECURSIVE mgrs AS (   SELECT employee_id, first_name, manager_id FROM employee WHERE manager_id IS NULL   UNION ALL   SELECT e.employee_id, e.first_name, e.manager_id   FROM employee e   JOIN mgrs m ON e.manager_id = m.employee_id ) SELECT * FROM mgrs;`

**Output:** hierarchical rows

---

### 54. Create a view for store sales summary

`CREATE VIEW store_sales AS SELECT s.store_id, s.store_name, SUM(sale.total_amount) AS total_sales FROM store s JOIN sale ON s.store_id = sale.store_id GROUP BY s.store_id, s.store_name;`

**Output:** view created; `SELECT * FROM store_sales;` shows totals

---

### 55. Use CTE for multi-step aggregation

`WITH sale_totals AS (   SELECT store_id, SUM(total_amount) AS total_sales FROM sale GROUP BY store_id ) SELECT s.store_name, st.total_sales FROM store s JOIN sale_totals st ON s.store_id = st.store_id;`

**Output:** store_name + total_sales

---

### 56. Materialized view idea (Postgres / Oracle)

`CREATE MATERIALIZED VIEW mv_store_sales AS SELECT store_id, SUM(total_amount) AS total_sales FROM sale GROUP BY store_id;`

**Note:** not available in all DBs; used for performance.

---

### 57. Drop and recreate a view (maintenance)

`DROP VIEW IF EXISTS store_sales; CREATE VIEW store_sales AS ...`

**Output:** view refreshed

---

### 58. Parameterized view alternative — use table-valued function (SQL Server)

`-- SQL Server: use inline TVF for parameterized logic CREATE FUNCTION dbo.GetStoreSales(@min_sales DECIMAL(10,2)) RETURNS TABLE AS RETURN (   SELECT store_id, SUM(total_amount) AS total_sales   FROM sale   GROUP BY store_id   HAVING SUM(total_amount) >= @min_sales );`

**Output:** call `SELECT * FROM dbo.GetStoreSales(1000);`

---

### 59. Use CTE + window to find top store by sales

`WITH totals AS (   SELECT store_id, SUM(total_amount) AS total_sales   FROM sale GROUP BY store_id ) SELECT * FROM (   SELECT t.*, ROW_NUMBER() OVER(ORDER BY total_sales DESC) rn FROM totals t ) x WHERE rn = 1;`

**Output:** single top store

---

### 60. Use CTE for complex delete (select then delete)

`WITH to_delete AS (   SELECT item_id FROM item WHERE sale_price < cost_price ) DELETE FROM item WHERE item_id IN (SELECT item_id FROM to_delete);`

**Output:** deleted rows (if any)

---

# #️⃣ SECTION 7 — DDL, INDEXES, KEYS, NORMALIZATION (61–70)

### 61. Add a composite unique index (prevent duplicate barcode per store)

`CREATE UNIQUE INDEX ux_item_store_barcode ON item(store_id, barcode);`

**Output:** index created

---

### 62. Add foreign key constraint (if missing)

`ALTER TABLE sale ADD CONSTRAINT fk_sale_customer FOREIGN KEY (customer_id) REFERENCES customer(customer_id);`

**Output:** constraint added (if valid)

---

### 63. Create a covering index to speed a query (MySQL / Postgres)

`CREATE INDEX idx_sale_store_amount ON sale(store_id, total_amount);`

**Use:** speeds queries filtering by store_id and ordering by total_amount

---

### 64. Add NOT NULL / default columns safely

`ALTER TABLE employee ADD COLUMN status VARCHAR(10) NOT NULL DEFAULT 'ACTIVE';`

**Output:** column added with default

---

### 65. Normalize: split full address into components (example DDL)

`ALTER TABLE customer ADD COLUMN street VARCHAR(255), ADD COLUMN zipcode VARCHAR(20); -- Then migrate data and drop old address if desired`

**Output:** columns added (normalization steps follow)

---

### 66. Create a lookup/enum table for payment methods

`CREATE TABLE payment_method (   payment_method_id INT PRIMARY KEY AUTO_INCREMENT,   name VARCHAR(50) UNIQUE );`

**Use:** enforces valid payment methods via FK from sale

---

### 67. Add CHECK constraint (Postgres/Oracle/MySQL 8+)

`ALTER TABLE store ADD CONSTRAINT chk_status CHECK (status IN ('OPEN','CLOSED'));`

**Output:** ensures status validity

---

### 68. Partitioning concept (MySQL/Postgres) — example by year

`-- MySQL example: create partitioned table (syntactic example) CREATE TABLE sale_partitioned (   sale_id INT, sale_date DATE, ... ) PARTITION BY RANGE (YEAR(sale_date)) (   PARTITION p2020 VALUES LESS THAN (2021),   PARTITION p2021 VALUES LESS THAN (2022) );`

**Output:** partitioned storage for performance on large tables

---

### 69. Rebuild / analyze index (maintenance)

`ANALYZE TABLE employee;       -- MySQL VACUUM ANALYZE employee;      -- Postgres ALTER INDEX idx_name REBUILD; -- SQL Server/Oracle variant`

**Output:** optimizer statistics refreshed

---

### 70. When to denormalize (short note + example)

- **When:** reporting tables, OLAP, very frequent reads and complex joins.
    
- **Example:** create `store_sales_snapshot` table storing precomputed totals for fast reads.
    

---

# #️⃣ SECTION 8 — TRANSACTIONS, ISOLATION, TRIGGERS (71–80)

### 71. Basic transaction (ACID)

`START TRANSACTION; UPDATE account SET balance = balance - 100 WHERE account_id = 1; UPDATE account SET balance = balance + 100 WHERE account_id = 2; COMMIT;`

**Output:** atomic transfer

---

### 72. Rollback on error

`START TRANSACTION; UPDATE ...; -- if error ROLLBACK;`

**Output:** no partial changes persisted

---

### 73. Set transaction isolation level (example)

`SET TRANSACTION ISOLATION LEVEL REPEATABLE READ; -- MySQL/Postgres/SQL Server variants`

**Use:** control phenomena like dirty reads / phantom reads

---

### 74. Simple AFTER INSERT trigger (MySQL example)

`DELIMITER // CREATE TRIGGER trg_after_sale_insert AFTER INSERT ON sale FOR EACH ROW BEGIN   INSERT INTO stats(event_type, event_date, amount)   VALUES ('SALE', NEW.sale_date, NEW.total_amount); END; // DELIMITER ;`

**Output:** stats row created on sale insert

---

### 75. BEFORE INSERT trigger to validate data

`CREATE TRIGGER trg_before_employee_insert BEFORE INSERT ON employee FOR EACH ROW BEGIN   IF NEW.salary < 0 THEN     SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Salary must be non-negative';   END IF; END;`

**Output:** prevents invalid insert

---

### 76. Use SAVEPOINT for partial rollback

`START TRANSACTION; -- step 1 SAVEPOINT sp1; -- step 2 (error) ROLLBACK TO sp1; COMMIT;`

**Output:** partial undo to savepoint

---

### 77. Deadlock handling (note + example)

- Use short transactions, consistent locking order; handle deadlock errors and retry in application.
    

---

### 78. Trigger caution — side effects & performance note

- Triggers run per-row; heavy logic may slow DML. Consider stored procedures or application-level logic for complex ops.
    

---

### 79. Audit trail using trigger (insert into audit table)

`CREATE TRIGGER trg_audit_employee AFTER UPDATE ON employee FOR EACH ROW BEGIN   INSERT INTO employee_audit(employee_id, old_salary, new_salary, changed_at)   VALUES (OLD.employee_id, OLD.salary, NEW.salary, NOW()); END;`

**Output:** audit rows created

---

### 80. Use of READ ONLY transactions for reporting

`START TRANSACTION READ ONLY; SELECT ... heavy reporting query ... COMMIT;`

**Use:** optimizer / DB uses less locking

---

# #️⃣ SECTION 9 — PERFORMANCE TUNING & EXPLAIN (81–90)

### 81. Use EXPLAIN to inspect query plan (MySQL/Postgres)

`EXPLAIN SELECT * FROM sale WHERE store_id = 1;`

**Output:** shows index usage, row estimates, cost

---

### 82. Optimize join order & indexes (example)

- Ensure columns used in JOIN/WHERE are indexed (foreign keys, filter columns).
    

---

### 83. Use covering index to avoid lookups

`CREATE INDEX idx_sale_store_amount ON sale(store_id, total_amount);`

**Use:** query selecting store_id, total_amount can be served from index alone

---

### 84. Avoid SELECT * in large queries (best practice)

- Select only needed columns to reduce I/O and network transfer.
    

---

### 85. Use LIMIT / pagination with keyset for large offsets

`-- keyset pagination SELECT * FROM sale WHERE sale_id > :last_id ORDER BY sale_id LIMIT 20;`

**Use:** faster than OFFSET for large pages

---

### 86. Use ANALYZE / statistics update

`ANALYZE TABLE sale; -- MySQL VACUUM ANALYZE sale; -- Postgres`

**Output:** better optimizer choices

---

### 87. Use batch inserts/updates for large data loads

`INSERT INTO item (cols) VALUES (...), (...), (...);`

**Use:** reduces transaction overhead

---

### 88. Use EXPLAIN ANALYZE for real costs (Postgres)

`EXPLAIN ANALYZE SELECT ...;`

**Output:** actual runtime and row counts

---

### 89. Avoid functions on indexed columns in WHERE (sargability)

- Instead of `WHERE YEAR(created_at) = 2022`, use `WHERE created_at >= '2022-01-01' AND created_at < '2023-01-01'` to use index.
    

---

### 90. Denormalize read-heavy aggregates into summary tables

- Precompute frequently queried aggregates and refresh periodically to avoid heavy runtime aggregation.
    

---

# #️⃣ SECTION 10 — ADVANCED QUERIES, PIVOT, JSON, STORED PROCS (91–100)

### 91. Pivot sales per store by payment_method (Postgres crosstab or CASE)

`SELECT store_id,   SUM(CASE WHEN payment_method = 'Card' THEN total_amount ELSE 0 END) AS card_total,   SUM(CASE WHEN payment_method = 'Cash' THEN total_amount ELSE 0 END) AS cash_total FROM sale GROUP BY store_id;`

**Output:** card_total, cash_total per store

---

### 92. JSON example — return customer as JSON (Postgres / MySQL JSON)

`-- Postgres: SELECT json_build_object('id', customer_id, 'name', first_name || ' ' || last_name) AS customer_json FROM customer;`

**Output:** JSON objects per customer

---

### 93. Stored procedure example (MySQL)

`DELIMITER // CREATE PROCEDURE sp_increase_salary(IN p_emp_id INT, IN p_amount DECIMAL(10,2)) BEGIN   UPDATE employee SET salary = salary + p_amount WHERE employee_id = p_emp_id; END; // DELIMITER ;`

**Output:** call `CALL sp_increase_salary(2, 500);`

---

### 94. Upsert / INSERT ... ON DUPLICATE KEY / MERGE

`-- MySQL INSERT INTO store (store_id, store_name) VALUES (1, 'Walmart North') ON DUPLICATE KEY UPDATE store_name = VALUES(store_name);  -- Postgres INSERT INTO store (store_id, store_name) VALUES (1, 'Walmart North') ON CONFLICT (store_id) DO UPDATE SET store_name = EXCLUDED.store_name;`

**Output:** insert or update

---

### 95. Use MERGE in SQL Server / Oracle for upsert logic

`MERGE INTO store tgt USING (VALUES (1,'X')) src(id,name)   ON (tgt.store_id = src.id) WHEN MATCHED THEN UPDATE SET store_name = src.name WHEN NOT MATCHED THEN INSERT (store_id,store_name) VALUES (src.id,src.name);`

---

### 96. Window + FILTER (Postgres) for conditional aggregates

`SELECT store_id,        SUM(total_amount) FILTER(WHERE payment_method='Card') AS card_sales,        SUM(total_amount) FILTER(WHERE payment_method='Cash') AS cash_sales FROM sale GROUP BY store_id;`

**Output:** per-store conditional sums

---

### 97. Use EXCEPT / MINUS to find difference sets

`-- Postgres: EXCEPT SELECT customer_id FROM customer EXCEPT SELECT customer_id FROM sale;  -- Oracle: MINUS SELECT ... FROM customer MINUS SELECT ... FROM sale;`

**Output:** customers with no sales

---

### 98. Ranking + percentiles for bonus allocation

`SELECT employee_id, first_name, salary,        NTILE(4) OVER(ORDER BY salary DESC) AS quartile FROM employee;`

**Output:** quartile per employee

---

### 99. Find gaps in sequence (missing ids)

`SELECT t1.employee_id + 1 AS missing_from FROM employee t1 LEFT JOIN employee t2 ON t1.employee_id + 1 = t2.employee_id WHERE t2.employee_id IS NULL;`

**Output:** shows missing ids (if any)

---

### 100. Interview puzzle — get second highest unique salary (no ties)

`-- Option A: using ROW_NUMBER (one row even if duplicates) SELECT * FROM (   SELECT e.*, ROW_NUMBER() OVER(ORDER BY salary DESC) AS rn FROM employee e ) t WHERE rn = 2;  -- Option B: distinct salaries SELECT MAX(salary) AS second_highest FROM (   SELECT DISTINCT salary FROM employee ORDER BY salary DESC LIMIT 2 ) x;`

**Output:** second highest salary (e.g., 80000 if Moh is highest, Sam second)