# NULL HANDLING FUNCTIONS

```text
NVL(expr, replacement)
NVL2(expr, value_if_not_null, value_if_null)
NULLIF(expr1, expr2)
COALESCE(expr1, expr2, expr3, ...)

```

Example:

`NVL(salary, 0)`

---

# 🔹 STRING (CHARACTER) FUNCTIONS

```sql
SUBSTR(string, start, length)
INSTR(string, substring [, start [, occurrence]])
LENGTH(string)
TRIM([LEADING | TRAILING | BOTH] char FROM string)
LTRIM(string [, char])
RTRIM(string [, char])
UPPER(string)
LOWER(string)
INITCAP(string)
REPLACE(string, search, replacement)
CONCAT(str1, str2)
LPAD(string, length [, pad])
RPAD(string, length [, pad])
TRANSLATE(string, from_chars, to_chars)
REGEXP_SUBSTR(string, pattern)
REGEXP_REPLACE(string, pattern, replacement)
REGEXP_LIKE(string, pattern)

```

---

# 🔹 NUMBER FUNCTIONS

```sql
ABS(n)
CEIL(n)
FLOOR(n)
ROUND(n [, decimals])
TRUNC(n [, decimals])
MOD(m, n)
POWER(m, n)
SQRT(n)
SIGN(n)
EXP(n)
LN(n)
LOG(base, n)

```

---

# 🔹 DATE & TIME FUNCTIONS

```sql
SYSDATE
SYSTIMESTAMP
CURRENT_DATE
CURRENT_TIMESTAMP
ADD_MONTHS(date, n)
MONTHS_BETWEEN(date1, date2)
NEXT_DAY(date, 'DAY')
LAST_DAY(date)
EXTRACT(YEAR | MONTH | DAY FROM date)
TRUNC(date [, format])
ROUND(date [, format])

```

Example:

`ADD_MONTHS(SYSDATE, 3)`

---

# 🔹 CONVERSION FUNCTIONS

```sql
TO_CHAR(date_or_number [, format])
TO_DATE(string, format)
TO_NUMBER(string)
CAST(expr AS datatype)

```

Example:

`TO_CHAR(SYSDATE, 'YYYY-MM-DD')`

---

# 🔹 CONDITIONAL / LOGIC FUNCTIONS

```sql
CASE WHEN condition THEN value ELSE value END
DECODE(expr, search, result [, default])

```

Example:

```sql
CASE WHEN salary > 5000 THEN 'HIGH' ELSE 'LOW' END
```


---

# 🔹 AGGREGATE FUNCTIONS

```sql
COUNT(* | expr)
SUM(expr)
AVG(expr)
MIN(expr)
MAX(expr)
LISTAGG(expr, delimiter)

```

Example:

`LISTAGG(name, ', ') WITHIN GROUP (ORDER BY name)`

---

# 🔹 ANALYTIC (WINDOW) FUNCTIONS ⭐

```sql
ROW_NUMBER()
RANK()
DENSE_RANK()
LEAD(expr [, offset])
LAG(expr [, offset])
SUM() OVER (PARTITION BY col)
AVG() OVER (...)

```

Example:

`ROW_NUMBER() OVER (PARTITION BY dept ORDER BY salary DESC)`

---

# 🔹 SYSTEM / METADATA FUNCTIONS

```sql
USER
UID
SYS_CONTEXT(namespace, parameter)
DBMS_RANDOM.VALUE

```

---

# 🔹 COLLECTION / JSON FUNCTIONS (MODERN ORACLE)

```sql
JSON_VALUE(json, path)
JSON_QUERY(json, path)
JSON_TABLE(json, path COLUMNS (...))

```

---

# 🔹 HIERARCHICAL FUNCTIONS

```sql
CONNECT BY
START WITH
LEVEL
SYS_CONNECT_BY_PATH

```

---

# 🔹 COMPARISON FUNCTIONS

`GREATEST(expr1, expr2, ...) LEAST(expr1, expr2, ...)`

---

# 🔹 SECURITY / HASHING

`DBMS_CRYPTO.HASH STANDARD_HASH`

---

# 🔥 MOST USED (MEMORIZE FOR INTERVIEWS)

```sql
NVL
SUBSTR
INSTR
TO_CHAR
TO_DATE
CASE
COUNT
SUM
ROW_NUMBER
ADD_MONTHS

```

---

## TL;DR 🧠

- Oracle has **hundreds** of built-ins
    
- Learn them by **category**
    
- `NVL + SUBSTR + TO_CHAR + CASE` = 🔑 daily SQL
    
- Analytic functions = ⭐ senior-level SQL
    

---

If you want next:

- 📌 **Top 20 interview questions using these**
    
- 📌 **Real queries combining 5–6 functions**
    
- 📌 **Oracle vs MySQL vs PostgreSQL functions**
    
- 📌 **Regex functions deep dive**