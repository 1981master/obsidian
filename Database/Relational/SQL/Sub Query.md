# **1️⃣ What is a Subquery?**

A **subquery** (or inner query) is a query **nested inside another query**.

- It runs first, and its result is used by the outer query.
    
- Can return a **single value**, **single row**, or **a table**.
    

### **Types of Subqueries**

1. **Scalar subquery** → returns a single value
    
2. **Row subquery** → returns a single row
    
3. **Table subquery** → returns multiple rows/columns
    

---

### **Example: Subquery in WHERE**

```sql
-- Get employees who work in the store with highest salary SELECT first_name, last_name FROM employee WHERE store_id = (     SELECT store_id     FROM employee     ORDER BY salary DESC     LIMIT 1 );
```


- Inner query `(SELECT store_id ...)` executes first
    
- Outer query uses its result to filter employees
    

---

### **Example: Subquery as a derived table**

```sql
-- Get top salary per store SELECT * FROM (     
SELECT first_name, last_name, store_id,            
RANK() OVER( PARTITION BY store_id ORDER BY salary DESC) AS rank_in_store     
FROM employee ) emp_sub 
WHERE rank_in_store = 1;
```

- Inner query calculates `RANK()` and assigns column alias
    
- Outer query filters rows where rank = 1
    

---

# **2️⃣ What is a CTE (Common Table Expression)?**

A **CTE** is a **named temporary result set** that exists for the duration of a query.

- Think of it as giving a **subquery a name**, but cleaner.
    
- Can improve readability, especially for complex queries.
    
- Often used with `WITH` keyword.
    

### **Syntax**

```sql
WITH cte_name AS (     
SELECT column1, column2     
FROM table_name     
WHERE condition ) 
SELECT * 
FROM cte_name 
WHERE condition2;
```


---

### **Example: CTE with RANK()**

`WITH ranked_employees AS (     SELECT first_name, last_name, store_id,            RANK() OVER(PARTITION BY store_id ORDER BY salary DESC) AS rank_in_store     FROM employee ) SELECT * FROM ranked_employees WHERE rank_in_store = 1;`

- `ranked_employees` is like a temporary table
    
- Column alias `rank_in_store` can now be used in outer query
    

---

# **3️⃣ Key Differences Between Subquery and CTE**

|Feature|Subquery|CTE|
|---|---|---|
|Syntax|Inline, nested|Declared with `WITH`|
|Readability|Can be messy if complex|Much cleaner and readable|
|Reuse|Hard to reuse|Can reference the CTE multiple times in query|
|Recursion|Usually no|Supports recursive queries (e.g., hierarchy)|

---

# **4️⃣ When to Use**

- **Subquery:** Quick one-off computations, filtering, or scalar values
    
- **CTE:** Complex queries, multiple layers, repeated reference, readability, or recursion
    

---

If you want, I can make a **visual diagram showing Subquery vs CTE vs Derived Table** with **window functions**, so you can see how aliases and filtering work — it’s very handy for interviews.

Do you want me to make that?

##### You said:

yes

###### ChatGPT said:

Perfect! Let’s make a clear **visual explanation** for Subquery vs CTE vs Derived Table, showing **how they work, their scope, and alias usage**. I’ll describe it in a Markdown-friendly way so you can use it directly in Obsidian.

---

# **Visual Guide: Subquery vs Derived Table vs CTE**

``# SQL Subquery / Derived Table / CTE Comparison  ## 1️⃣ Subquery - Nested query inside another query - Executes first - Can return:  - Scalar (single value)  - Row (single row)  - Table (multiple rows/columns)  ### Example: SELECT first_name, last_name FROM employee WHERE store_id = (     SELECT store_id     FROM employee     ORDER BY salary DESC     LIMIT 1 );  **Flow:** 1. Inner query runs → returns a single store_id 2. Outer query filters employees based on that store_id  **Notes:** - Column aliases from inner query **cannot** be used in WHERE of same subquery - Simple, but can get messy if nested multiple times  ---  ## 2️⃣ Derived Table (Subquery in FROM with alias) - Subquery returns a table - Must have a **table alias** - Column aliases can be used in outer query  ### Example: SELECT * FROM (     SELECT first_name, last_name, store_id,            RANK() OVER(PARTITION BY store_id ORDER BY salary DESC) AS rank_in_store     FROM employee ) emp_sub WHERE rank_in_store = 1;  **Flow:** 1. Inner query calculates RANK() → column alias `rank_in_store` 2. Outer query filters using alias 3. Table alias `emp_sub` is mandatory  **Notes:** - Very useful with window functions - Helps filter top N per group  ---  ## 3️⃣ CTE (Common Table Expression) - Named temporary result set using `WITH` - Exists only during the query execution - Can be reused multiple times in the query - Cleaner and more readable than nested subqueries  ### Example: WITH ranked_employees AS (     SELECT first_name, last_name, store_id,            RANK() OVER(PARTITION BY store_id ORDER BY salary DESC) AS rank_in_store     FROM employee ) SELECT * FROM ranked_employees WHERE rank_in_store = 1;  **Flow:** 1. CTE executes first → temporary table `ranked_employees` 2. Outer query references CTE directly 3. Column aliases from CTE can be used freely  **Notes:** - Preferred for complex queries - Supports recursion in some DBs (Oracle, PostgreSQL, SQL Server) - Improves readability and maintainability  ---  ## ✅ Comparison Table  | Feature                  | Subquery             | Derived Table                | CTE                        | |---------------------------|--------------------|-----------------------------|----------------------------| | Syntax                   | Inline, nested      | Subquery in FROM            | WITH keyword               | | Alias requirement        | Optional for scalar | Mandatory (table alias)     | Named CTE                  | | Column alias usage        | Limited             | Can use in outer query      | Can use in outer query     | | Reusability              | No                  | No                          | Yes                        | | Readability              | Low if nested       | Medium                      | High                       | | Supports recursion        | ❌                  | ❌                          | ✅ in some DBs             |``

---

### ✅ Key Takeaways

- **Subquery:** quick filters, single-use, can get messy
    
- **Derived Table:** good for intermediate results and filtering window functions
    
- **CTE:** clean, readable, reusable, supports recursion
    

---

If you want, I can also make a **diagram with arrows** showing **execution order**: WHERE → SELECT → Derived Table → CTE → ORDER BY, with column and table aliases — this is perfect for visual memory in interviews.

Do you want me to make that diagram?