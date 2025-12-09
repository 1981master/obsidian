## Column Alias Support Across Databases

**WHERE**  
- MySQL: ❌ No  
- Oracle: ❌ No  
- SQL Server: ❌ No  
- PostgreSQL: ❌ No  
**Notes:** Must use original column name; alias not recognized.

**SELECT**  
- MySQL: ✅ Yes  
- Oracle: ✅ Yes  
- SQL Server: ✅ Yes  
- PostgreSQL: ✅ Yes  
**Notes:** Assign alias to expression or column.

**ORDER BY**  
- MySQL: ✅ Yes  
- Oracle: ✅ Yes  
- SQL Server: ✅ Yes  
- PostgreSQL: ✅ Yes  
**Notes:** Alias allowed.

**GROUP BY**  
- MySQL: ❌ No  
- Oracle: ❌ No  
- SQL Server: ❌ No  
- PostgreSQL: ❌ No  
**Notes:** Must use original column; alias usually not allowed.

**HAVING**  
- MySQL: ✅ Yes  
- Oracle: ❌ No  
- SQL Server: ✅ Yes  
- PostgreSQL: ✅ Yes  
**Notes:** MySQL, SQL Server, PostgreSQL allow alias; Oracle requires expression.

**Subquery / CTE**  
- MySQL: ✅ Yes  
- Oracle: ✅ Yes  
- SQL Server: ✅ Yes  
- PostgreSQL: ✅ Yes  
**Notes:** Alias visible outside derived table / CTE.
==============================
# **1️⃣ Column Aliases in WHERE Clause**

- **Not allowed** in most RDBMS because **WHERE is evaluated before SELECT**
    
- You **must use the original column name** in the WHERE clause.
    

**Example in Oracle / SQL Server / PostgreSQL / MySQL:**

`SELECT employee_id AS ID, first_name FROM employee WHERE ID = 1;  -- ❌ ERROR`

- Alias `ID` is not recognized in WHERE
    

✅ Correct:

`SELECT employee_id AS ID, first_name FROM employee WHERE employee_id = 1;  -- ✅ works`

---

# **2️⃣ Column Aliases in ORDER BY**

- Allowed in almost all RDBMS
    

`SELECT employee_id AS ID, first_name FROM employee ORDER BY ID;  -- ✅ works`

---

# **3️⃣ Column Aliases in GROUP BY / HAVING**

- **GROUP BY:** usually you need original column name
    
- **HAVING:** some databases allow alias, some require expression
    

`-- Oracle / MySQL / PostgreSQL SELECT department_id AS dept, COUNT(*) AS emp_count FROM employee GROUP BY department_id HAVING COUNT(*) > 5;       -- ✅ standard -- HAVING dept > 5  ❌ usually not allowed`

---

# **4️⃣ Workaround if you want to use alias**

- Use a **subquery or CTE**:
    

`-- Works in Oracle, MySQL, SQL Server, PostgreSQL SELECT * FROM (     SELECT employee_id AS ID, first_name     FROM employee ) emp_sub WHERE ID = 1;`

- Outer query can reference the alias because it **already exists in derived table**.