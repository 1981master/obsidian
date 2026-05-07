# 🔥 1. `groupingBy` (Most Important)

## ✅ Basic grouping

```
Map<String, List<User>> usersByCity =    users.stream()         .collect(Collectors.groupingBy(User::getCity));
```

👉 Result:

```
{  "NY": [user1, user2],  "LA": [user3]}
```

---

## 🔥 Group + Count (VERY COMMON INTERVIEW)

```
Map<String, Long> countByCity =    users.stream()         .collect(Collectors.groupingBy(             User::getCity,             Collectors.counting()         ));
```

👉 Instead of `List<User>` → you get counts

---

## 🔥 Group + Mapping (Transform inside grouping)

```
Map<String, List<String>> namesByCity =    users.stream()         .collect(Collectors.groupingBy(             User::getCity,             Collectors.mapping(User::getName, Collectors.toList())         ));
```

👉 Result:

```
"NY" → ["Ali", "John"]
```

---

## 🔥 Group + Max / Min (Advanced)

```
Map<String, Optional<User>> highestPaidByDept =    users.stream()         .collect(Collectors.groupingBy(             User::getDepartment,             Collectors.maxBy(Comparator.comparing(User::getSalary))         ));
```

👉 Each group gives **Optional<User>**

---

## 🔥 Clean version (remove Optional)

```
Map<String, User> highestPaidByDept =    users.stream()         .collect(Collectors.groupingBy(             User::getDepartment,             Collectors.collectingAndThen(                 Collectors.maxBy(Comparator.comparing(User::getSalary)),                 Optional::get             )         ));
```

⚠️ Interview note: mention **Optional safety**

---

# 🔥 2. Multi-Level Grouping (Nested grouping)

```
Map<String, Map<String, List<User>>> data =    users.stream()         .collect(Collectors.groupingBy(             User::getDepartment,             Collectors.groupingBy(User::getCity)         ));
```

👉 Result:

```
{  "IT": {    "NY": [...],    "LA": [...]  }}
```

---

# 🔥 3. `partitioningBy` (Boolean split)

## ✅ Basic

```
Map<Boolean, List<User>> activeUsers =    users.stream()         .collect(Collectors.partitioningBy(User::isActive));
```

👉 Result:

```
true  → active usersfalse → inactive users
```

---

## 🔥 Partition + Count

```
Map<Boolean, Long> count =    users.stream()         .collect(Collectors.partitioningBy(             User::isActive,             Collectors.counting()         ));
```

---

## 🔥 Partition vs Grouping (INTERVIEW TRAP)

|Feature|`groupingBy`|`partitioningBy`|
|---|---|---|
|Keys|Any type|Only Boolean|
|Output keys|Dynamic|Always `true/false`|
|Performance|Slightly heavier|Optimized for 2 groups|

👉 If condition is **boolean → ALWAYS prefer `partitioningBy`**

---

# 🔥 4. `groupingBy` + `summing / averaging`

```
Map<String, Double> avgSalary =    users.stream()         .collect(Collectors.groupingBy(             User::getDepartment,             Collectors.averagingDouble(User::getSalary)         ));
```

---

## 🔥 Sum example

```
Map<String, Double> totalSalary =    users.stream()         .collect(Collectors.groupingBy(             User::getDepartment,             Collectors.summingDouble(User::getSalary)         ));
```

---

# 🔥 5. `groupingBy` + `toMap` (Advanced transformation)

```
Map<String, Map<Long, User>> result =    users.stream()         .collect(Collectors.groupingBy(             User::getDepartment,             Collectors.toMap(User::getId, user -> user)         ));
```

---

# 🔥 6. Custom Collector Logic (Power move)

## Example: Join names per department

```
Map<String, String> names =    users.stream()         .collect(Collectors.groupingBy(             User::getDepartment,             Collectors.mapping(                 User::getName,                 Collectors.joining(", ")             )         ));
```

👉 Result:

```
"IT" → "Ali, John, Sara"
```

---

# 🔥 7. Real-world scenario (VERY IMPORTANT)

## Group orders by status + total price

```
Map<String, Double> revenueByStatus =    orders.stream()          .collect(Collectors.groupingBy(              Order::getStatus,              Collectors.summingDouble(Order::getPrice)          ));
```

---

# ⚠️ Common Mistakes (Interview Killers)

### ❌ Using grouping instead of DB query

```
userRepository.findAll().stream() // BAD for large data
```

👉 Always prefer:

```
SELECT department, COUNT(*) FROM users GROUP BY department;
```

---

### ❌ Ignoring Optional in maxBy

```
Optional<User> u = ...u.get(); // risky
```

---

### ❌ Over-nesting

If your stream looks like:

```
groupingBy(... groupingBy(... mapping(...)))
```

👉 Might be too complex → consider refactoring

---

# 🧠 Mental Model

Think:

- `groupingBy` → **SQL GROUP BY**
- `partitioningBy` → **WHERE condition split**
- `mapping` → **SELECT transformation**
- `summing/counting` → **aggregation**

---

# 🏁 Final Takeaway

> **Streams shine when you combine grouping + downstream collectors to express SQL-like logic in Java—but don’t replace the database for heavy operations.**