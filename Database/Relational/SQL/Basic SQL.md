```SQL
## **1. Create a Table**

**Problem:** Create a table `Customers` with columns: `id`, `name`, `email`. `id` is primary key.

### Table: _None yet_

### SQL:

`CREATE TABLE Customers (     id INT PRIMARY KEY,     name VARCHAR(50),     email VARCHAR(50) );`

**Comment:**  
DDL command `CREATE TABLE` defines the structure of the database. `PRIMARY KEY` ensures `id` is unique.

---

## **2. Insert Rows**

**Problem:** Insert 3 customers into `Customers`.

### SQL:

`INSERT INTO Customers (id, name, email) VALUES (1, 'Alice', 'alice@mail.com'), (2, 'Bob', 'bob@mail.com'), (3, 'Charlie', 'charlie@mail.com');`

**Comment:**  
DML `INSERT` adds data to the table.

---

## **3. Select All Data**

**Problem:** Display all customer records.

### SQL:

`SELECT * FROM Customers;`

**Comment:**  
Simple DQL `SELECT` retrieves all data.

---

## **4. Update a Row**

**Problem:** Update Bob’s email to `bob@newmail.com`.

### SQL:

`UPDATE Customers SET email = 'bob@newmail.com' WHERE id = 2;`

**Comment:**  
DML `UPDATE` modifies specific rows using `WHERE`.

---

## **5. Delete a Row**

**Problem:** Delete Charlie from `Customers`.

### SQL:

`DELETE FROM Customers WHERE id = 3;`

**Comment:**  
DML `DELETE` removes specific rows.

---

## **6. Create Orders Table**

**Problem:** Create table `Orders` with `order_id`, `customer_id`, `product`.

### SQL:

`CREATE TABLE Orders (     order_id INT PRIMARY KEY,     customer_id INT,     product VARCHAR(50) );`

**Comment:**  
Define `Orders` table. `customer_id` will later be FK.

---

## **7. Insert Orders**

**Problem:** Insert 3 orders.

### SQL:

`INSERT INTO Orders (order_id, customer_id, product) VALUES (1, 1, 'Keyboard'), (2, 2, 'Mouse'), (3, 1, 'Monitor');`

**Comment:**  
Two orders for Alice (id=1), one for Bob.

---

## **8. INNER JOIN Customers + Orders**

**Problem:** List all customers and their orders.

### SQL:

`SELECT c.name, o.product FROM Customers c INNER JOIN Orders o ON c.id = o.customer_id;`

**Comment:**  
Inner join shows only customers with orders.

---

## **9. LEFT JOIN Customers + Orders**

**Problem:** List all customers, show NULL if no order.

### SQL:

`SELECT c.name, o.product FROM Customers c LEFT JOIN Orders o ON c.id = o.customer_id;`

**Comment:**  
Left join keeps all customers; orders are NULL if missing.

---

## **10. Aggregate Function – COUNT**

**Problem:** Count orders per customer.

### SQL:

`SELECT c.name, COUNT(o.order_id) AS total_orders FROM Customers c LEFT JOIN Orders o ON c.id = o.customer_id GROUP BY c.name;`

**Comment:**  
`COUNT` counts orders. LEFT JOIN ensures customers with 0 orders are included.

---

## **11. MAX / MIN**

**Problem:** Find the most expensive product.

### Table: Products

|product_id|name|price|
|---|---|---|
|1|Keyboard|25|
|2|Mouse|15|
|3|Monitor|120|

### SQL:

`SELECT MAX(price) AS max_price FROM Products;`

**Comment:**  
`MAX` finds largest value in a column.

---

## **12. SUM**

**Problem:** Total price of all products.

### SQL:

`SELECT SUM(price) AS total_price FROM Products;`

**Comment:**  
`SUM` calculates total value.

---

## **13. DISTINCT**

**Problem:** List all unique product names.

### SQL:

`SELECT DISTINCT name FROM Products;`

**Comment:**  
Removes duplicates.

---

## **14. WHERE Clause**

**Problem:** Find products with price > 20.

### SQL:

`SELECT * FROM Products WHERE price > 20;`

**Comment:**  
Filters rows based on condition.

---

## **15. ORDER BY**

**Problem:** List products by price descending.

### SQL:

`SELECT * FROM Products ORDER BY price DESC;`

**Comment:**  
Sort results.

---

## **16. LIMIT**

**Problem:** Show top 2 expensive products.

### SQL:

`SELECT * FROM Products ORDER BY price DESC LIMIT 2;`

**Comment:**  
`LIMIT` restricts rows returned.

---

## **17. CREATE TABLE with FOREIGN KEY**

**Problem:** Make `Orders.customer_id` a foreign key referencing `Customers.id`.

### SQL:

`ALTER TABLE Orders ADD CONSTRAINT fk_customer FOREIGN KEY (customer_id) REFERENCES Customers(id);`

**Comment:**  
Ensures referential integrity.

---

## **18. Subquery – Simple**

**Problem:** List customers who placed at least one order.

### SQL:

`SELECT * FROM Customers WHERE id IN (SELECT customer_id FROM Orders);`

**Comment:**  
Subquery finds matching customer_ids.

---

## **19. EXISTS**

**Problem:** Same as above using EXISTS.

### SQL:

`SELECT * FROM Customers c WHERE EXISTS (     SELECT 1 FROM Orders o WHERE o.customer_id = c.id );`

**Comment:**  
`EXISTS` checks if subquery returns rows.

---

## **20. Aliases**

**Problem:** Show customer names and product with aliases.

### SQL:

`SELECT c.name AS customer_name, o.product AS order_item FROM Customers c JOIN Orders o ON c.id = o.customer_id;`

**Comment:**  
Aliases improve readability.

---

## **21. IN Clause**

**Problem:** Find orders for Alice or Bob.

### SQL:

`SELECT * FROM Orders WHERE customer_id IN (1, 2);`

**Comment:**  
`IN` simplifies multiple OR conditions.

---

## **22. NOT IN Clause**

**Problem:** Orders not made by Alice.

### SQL:

`SELECT * FROM Orders WHERE customer_id NOT IN (1);`

**Comment:**  
Excludes specific customer_ids.

---

## **23. BETWEEN**

**Problem:** Products priced between 20 and 100.

### SQL:

`SELECT * FROM Products WHERE price BETWEEN 20 AND 100;`

**Comment:**  
Range filter.

---

## **24. LIKE**

**Problem:** Products containing 'o'.

### SQL:

`SELECT * FROM Products WHERE name LIKE '%o%';`

**Comment:**  
Pattern matching with wildcard `%`.

---

## **25. CASE**

**Problem:** Show product price category (Cheap, Expensive).

### SQL:

`SELECT name, price, CASE     WHEN price < 20 THEN 'Cheap'     WHEN price >= 20 THEN 'Expensive' END AS price_category FROM Products;`

**Comment:**  
`CASE` adds conditional logic.

---

## **26. SELF JOIN**

**Problem:** Employees table, show employee and manager.

### Employees Table

|emp_id|name|manager_id|
|---|---|---|
|1|Alice|NULL|
|2|Bob|1|
|3|Charlie|1|

### SQL:

`SELECT e.name AS employee, m.name AS manager FROM Employees e LEFT JOIN Employees m ON e.manager_id = m.emp_id;`

**Comment:**  
Join table with itself for hierarchical data.

---

## **27. CROSS JOIN**

**Problem:** Pair each customer with each product.

### SQL:

`SELECT c.name, p.name AS product_name FROM Customers c CROSS JOIN Products p;`

**Comment:**  
Produces all combinations (3 × 3 = 9 rows).

---

## **28. FULL OUTER JOIN**

**Problem:** Show all customers and all orders, even unmatched.

### SQL (PostgreSQL):

`SELECT c.name, o.product FROM Customers c FULL OUTER JOIN Orders o ON c.id = o.customer_id;`

**Comment:**  
Returns all rows from both tables.

---

## **29. GROUP BY with HAVING**

**Problem:** Customers with more than 1 order.

### SQL:

`SELECT c.name, COUNT(o.order_id) AS total_orders FROM Customers c JOIN Orders o ON c.id = o.customer_id GROUP BY c.name HAVING COUNT(o.order_id) > 1;`

**Comment:**  
`HAVING` filters aggregated rows.

---

## **30. DROP Table**

**Problem:** Delete table `Products`.

### SQL:

`DROP TABLE Products;`
```