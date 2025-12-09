# 4️⃣ **Other window functions often used with `ROW_NUMBER` / `RANK`**

|Function|What it does|Use cases|
|---|---|---|
|`FIRST_VALUE(column)`|First value in the window|Earliest sale, first hire, first order per customer|
|`LAST_VALUE(column)`|Last value in the window|Latest sale, most recent event|
|`NTH_VALUE(column, n)`|n-th value in the window|Pick 2nd highest score, 3rd order, etc.|
|`LEAD(column, n)`|Value **n rows after** current|Compare current row with next row, calculate difference|
|`LAG(column, n)`|Value **n rows before** current|Compare current row with previous row, running changes|
|`NTILE(n)`|Split rows into n buckets|Quartiles, deciles, top 10%, etc.|
|`SUM(column) OVER()`|Running or partitioned sum|Cumulative totals, running balance|
|`AVG(column) OVER()`|Running or partitioned average|Running average, per group average|
|`COUNT(*) OVER()`|Count rows in partition|Total employees per department, total orders per customer|
|`MIN/MAX(column) OVER()`|Partitioned min/max|Highest sale per group, earliest hire|


### Sample `employee` table:

|employee_id|first_name|store_id|salary|hire_date|
|---|---|---|---|---|
|1|Sam|1|80000|2020-01-01|
|2|John|1|35000|2021-03-15|
|3|Lara|2|30000|2022-08-20|
|4|Moh|2|3333333|2022-08-20|

---

## 1️⃣ `FIRST_VALUE(column)` – first value in the window

`SELECT first_name, store_id, salary,        FIRST_VALUE(salary) OVER(PARTITION BY store_id ORDER BY salary DESC) AS highest_salary_in_store FROM employee;`

**Output:**

|first_name|store_id|salary|highest_salary_in_store|
|---|---|---|---|
|Sam|1|80000|80000|
|John|1|35000|80000|
|Moh|2|3333333|3333333|
|Lara|2|30000|3333333|

> Gives the **first value in the ordered window** per store.

---

## 2️⃣ `LAST_VALUE(column)` – last value in the window

`SELECT first_name, store_id, salary,        LAST_VALUE(salary) OVER(PARTITION BY store_id ORDER BY salary DESC                                ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS lowest_salary_in_store FROM employee;`

**Output:**

|first_name|store_id|salary|lowest_salary_in_store|
|---|---|---|---|
|Sam|1|80000|35000|
|John|1|35000|35000|
|Moh|2|3333333|30000|
|Lara|2|30000|30000|

> Last value requires specifying **frame** to include all rows.

---

## 3️⃣ `NTH_VALUE(column, n)` – n-th value in the window

`SELECT first_name, store_id, salary,        NTH_VALUE(salary, 2) OVER(PARTITION BY store_id ORDER BY salary DESC                                  ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS second_highest_salary FROM employee;`

**Output:**

|first_name|store_id|salary|second_highest_salary|
|---|---|---|---|
|Sam|1|80000|35000|
|John|1|35000|35000|
|Moh|2|3333333|30000|
|Lara|2|30000|30000|

> Picks the **n-th value** per partition.

---

## 4️⃣ `LEAD(column, n)` – value n rows **after**

`SELECT first_name, store_id, salary,        LEAD(salary, 1) OVER(PARTITION BY store_id ORDER BY salary DESC) AS next_salary FROM employee;`

**Output:**

|first_name|store_id|salary|next_salary|
|---|---|---|---|
|Sam|1|80000|35000|
|John|1|35000|NULL|
|Moh|2|3333333|30000|
|Lara|2|30000|NULL|

> Shows **next row’s salary** per store.

---

## 5️⃣ `LAG(column, n)` – value n rows **before**

`SELECT first_name, store_id, salary,        LAG(salary, 1) OVER(PARTITION BY store_id ORDER BY salary DESC) AS previous_salary FROM employee;`

**Output:**

|first_name|store_id|salary|previous_salary|
|---|---|---|---|
|Sam|1|80000|NULL|
|John|1|35000|80000|
|Moh|2|3333333|NULL|
|Lara|2|30000|3333333|

> Shows **previous row’s salary** per store.

---

## 6️⃣ `NTILE(n)` – split rows into buckets

`SELECT first_name, store_id, salary,        NTILE(2) OVER(PARTITION BY store_id ORDER BY salary DESC) AS bucket FROM employee;`

**Output:**

|first_name|store_id|salary|bucket|
|---|---|---|---|
|Sam|1|80000|1|
|John|1|35000|2|
|Moh|2|3333333|1|
|Lara|2|30000|2|

> Divides employees into **2 buckets per store** (like quartiles if n=4).

---

## 7️⃣ `SUM(column) OVER()` – cumulative sum

`SELECT first_name, store_id, salary,        SUM(salary) OVER(PARTITION BY store_id ORDER BY salary DESC) AS cumulative_salary FROM employee;`

**Output:**

|first_name|store_id|salary|cumulative_salary|
|---|---|---|---|
|Sam|1|80000|80000|
|John|1|35000|115000|
|Moh|2|3333333|3333333|
|Lara|2|30000|3363333|

> Running total **per store**.

---

## 8️⃣ `AVG(column) OVER()` – running / partitioned average

`SELECT first_name, store_id, salary,        AVG(salary) OVER(PARTITION BY store_id) AS avg_salary_in_store FROM employee;`

**Output:**

|first_name|store_id|salary|avg_salary_in_store|
|---|---|---|---|
|Sam|1|80000|57500|
|John|1|35000|57500|
|Moh|2|3333333|1686666.5|
|Lara|2|30000|1686666.5|

---

## 9️⃣ `COUNT(*) OVER()` – count rows in partition

`SELECT first_name, store_id,        COUNT(*) OVER(PARTITION BY store_id) AS num_employees FROM employee;`

**Output:**

|first_name|store_id|num_employees|
|---|---|---|
|Sam|1|2|
|John|1|2|
|Moh|2|2|
|Lara|2|2|

---

## 🔟 `MIN/MAX(column) OVER()` – partitioned min / max

`SELECT first_name, store_id, salary,        MAX(salary) OVER(PARTITION BY store_id) AS max_salary,        MIN(salary) OVER(PARTITION BY store_id) AS min_salary FROM employee;`

**Output:**

|first_name|store_id|salary|max_salary|min_salary|
|---|---|---|---|---|
|Sam|1|80000|80000|35000|
|John|1|35000|80000|35000|
|Moh|2|3333333|3333333|30000|
|Lara|2|30000|3333333|30000|

---

✅ These examples cover **all the key window functions** you mentioned.

If you want, I can make a **single visual cheat sheet** with **columns showing input, function, and output** for **all 10 window functions** — perfect for quick reference.

Do you want me to do that?

##### You said:

what if we need just the total salary in each department

###### ChatGPT said:

If you only need **total salary per department**, the cleanest and most common way is **GROUP BY** — not a window function.

---

# ✅ **1. Total salary per department (simple, correct way)**

`SELECT store_id,        SUM(salary) AS total_salary FROM employee GROUP BY store_id ORDER BY store_id;`

### ✔ Output example

|store_id|total_salary|
|---|---|
|1|115000|
|2|3363333|

---

# ✅ **2. Total salary per department WITH window function**

(If you want the total **repeated for each row**)

`SELECT first_name, store_id, salary,        SUM(salary) OVER(PARTITION BY store_id) AS total_salary_in_store FROM employee ORDER BY store_id, salary DESC;`

### ✔ Output example

|first_name|store_id|salary|total_salary_in_store|
|---|---|---|---|
|Sam|1|80000|115000|
|John|1|35000|115000|
|Moh|2|3333333|3363333|
|Lara|2|30000|3363333|

---

# 🔍 When to use each?

### ✔ **Use GROUP BY**

When you want _one row per group_  
→ totals, averages, counts

### ✔ **Use window functions**

When you want _every employee row_, but also show totals next to each row.