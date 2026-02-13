Build-In-Sorting
```
# 🔥 **1. Sorting Arrays (java.util.Arrays)**

### ✔ `Arrays.sort(array)`

Sorts using natural order.

Works for:

- primitives → int[], double[], char[], etc.
    
- objects that implement `Comparable`
    

---

### ✔ `Arrays.sort(array, comparator)`

Sort array of objects using comparator.

`Arrays.sort(users, Comparator.comparing(User::getAge));`

---

### ✔ `Arrays.parallelSort(array)`

Parallel version (faster on large arrays).

Supports:

- primitives
    
- object arrays
    

---

### ✔ `Arrays.parallelSort(array, from, to)`

Parallel sort for a subrange.

---

### ✔ `Arrays.sort(array, from, to)`

Sort sub-range of an array.

---

# 🔥 **2. Sorting Lists (java.util.Collections)**

### ✔ `Collections.sort(list)`

Uses natural ordering (`Comparable`).

---

### ✔ `Collections.sort(list, comparator)`

Use any comparator.

---

### ✔ `list.sort(comparator)`

The **modern and preferred** version.

`list.sort(Comparator.comparing(User::getName));`

---

# 🔥 **3. Stream Sorting (Java 8+)**

### ✔ `stream.sorted()`

Natural ordering (Comparable).

---

### ✔ `stream.sorted(comparator)`

Custom comparator.

`users.stream()      .sorted(Comparator.comparing(User::getSalary))      .toList();`

---

### ✔ `parallelStream().sorted()`

Runs sorting in parallel (careful: expensive).

---

# 🔥 **4. Collectors Sorting (during grouping, collecting)**

Sorting inside collectors:

### ✔ `Collectors.toList()`

Does NOT sort by itself — but you can place sorted() before:

`users.stream()      .sorted()      .collect(Collectors.toList());`

### ✔ `Collectors.collectingAndThen(...)`

Sorting + immutable list:

`collectingAndThen(     toList(),     list -> list.stream()                 .sorted(comparator)                 .toList() )`

### ✔ `Collectors.toMap()`

Maps do NOT preserve sort order, so use:

### ✔ `Collectors.toMap(..., ..., LinkedHashMap::new)`

Preserves insertion order after sorting.

---

# 🔥 **5. Sorting Maps (entries, keys, values)**

### ✔ Sort by keys:

`map.entrySet()    .stream()    .sorted(Map.Entry.comparingByKey())`

---

### ✔ Sort by values:

`sorted(Map.Entry.comparingByValue())`

---

### ✔ Using custom comparator:

`sorted(Map.Entry.comparingByValue(Comparator.reverseOrder()))`

---

# 🔥 **6. Special Sorting Methods**

### ✔ `Collections.reverse(list)`

Reverse order — **NOT** sorting, but related.

---

### ✔ `Collections.shuffle(list)`

Random reordering.

---

### ✔ `Collections.rotate(list, distance)`

Moves items around.

---

### ✔ `Collections.swap(list, i, j)`

Swap positions manually.

---

---

# 🔥 **7. PriorityQueue (always sorted on remove)**

### ✔ Natural ordering

`PriorityQueue<Integer> pq = new PriorityQueue<>();`

---

### ✔ Custom comparator

`new PriorityQueue<>(Comparator.comparing(User::getAge));`

Elements are **not stored sorted**, but `poll()` returns in sorted order.

---

# 🔥 **8. TreeSet / TreeMap (sorted collections)**

### ✔ TreeSet sorts automatically

By natural order or comparator.

### ✔ TreeMap sorts keys automatically

Natural order or comparator.

`new TreeSet<>(Comparator.comparing(User::getName));`

---

# 🔥 **9. Parallel & Low-Level Sorting**

### ✔ `Arrays.parallelSort(...)`

Multi-threaded quicksort/mergesort hybrid.

### ✔ ForkJoin Sorting (manual)

Advanced: custom parallel sorting using ForkJoinPool.

---

# 🔥 **FULL SUMMARY (Everything Java Provides for Sorting)**

### **Array sorting**

- `Arrays.sort`
    
- `Arrays.sort(range)`
    
- `Arrays.sort(array, comparator)`
    
- `Arrays.parallelSort`
    
- `Arrays.parallelSort(range)`
    

### **List sorting**

- `Collections.sort`
    
- `Collections.sort(comparator)`
    
- `List.sort(comparator)`
    

### **Stream sorting**

- `stream.sorted()`
    
- `stream.sorted(comparator)`
    
- `parallelStream.sorted()`
    

### **Map sorting**

- `Map.Entry.comparingByKey`
    
- `Map.Entry.comparingByValue`
    
- Sorted TreeMap
    
- Sorted TreeSet
    

### **Other reorder tools**

- `Collections.reverse`
    
- `Collections.shuffle`
    
- `Collections.rotate`
    
- `Collections.swap`
    

### **Sorted structures**

- PriorityQueue
    
- TreeSet
    
- TreeMap
    

### **Parallel / advanced**

- parallelSort algorithms
    
- ForkJoin custom sorting
  
  
  # **1. Sorting Map by Key**

Map<String, Integer> map = new HashMap<>();

map.put("Alice", 50);
map.put("Bob", 30);
map.put("Charlie", 40);

// ==============================
// Sort by key using Comparator
// ==============================
Map<String, Integer> sortedByKey =
        map.entrySet()
           .stream()
           .sorted(Comparator.comparing(Map.Entry::getKey))
           .collect(Collectors.toMap(
                   Map.Entry::getKey,
                   Map.Entry::getValue,
                   (oldValue, newValue) -> oldValue, // merge function in case of 
                   double key.
                   LinkedHashMap::new                 // preserves insertion order
           ));

System.out.println(sortedByKey);


✅ Output:

`{Alice=50, Bob=30, Charlie=40}`

---

# **2. Sorting Map by Value**

// ==============================
// Sort Map by value (ascending)
// ==============================
Map<String, Integer> sortedByValue =
        map.entrySet()
           .stream()
           .sorted(Comparator.comparing(Map.Entry::getValue))
           .collect(Collectors.toMap(
                   Map.Entry::getKey,
                   Map.Entry::getValue,
                   (oldValue, newValue) -> oldValue, // merge function
                   LinkedHashMap::new                 // preserves order
           ));

System.out.println(sortedByValue);


✅ Output:

`{Bob=30, Charlie=40, Alice=50}`

---

# **3. Sorting Map by Value in Reverse**

`Map<String, Integer> sortedByValueDesc = map.entrySet()         .stream()         .sorted(Map.Entry.<String, Integer>comparingByValue().reversed())         .collect(Collectors.toMap(                 Map.Entry::getKey,                 Map.Entry::getValue,                 (oldValue, newValue) -> oldValue,                 LinkedHashMap::new         ));  System.out.println(sortedByValueDesc);`

✅ Output:

`{Alice=50, Charlie=40, Bob=30}`

---

# **4. Multi-level Sorting (by Value then Key)**

// =======================================
// Sort Map by value, then key (ascending)
// =======================================
Map<String, Integer> sortedByValueThenKey =
        map.entrySet()
           .stream()
           .sorted(
                   Comparator.comparing(Map.Entry<String, Integer>::getValue)
                             .thenComparing(Map.Entry::getKey)
           )
           .collect(Collectors.toMap(
                   Map.Entry::getKey,
                   Map.Entry::getValue,
                   (oldValue, newValue) -> oldValue, // merge function
                   LinkedHashMap::new                 // preserves order
           ));

System.out.println(sortedByValueThenKey);


✅ Output:

`{Bob=30, Charlie=40, Alice=50}`

---

# **5. Notes / Tips**

- `Map.Entry::getKey` → sorts by key
    
- `Map.Entry::getValue` → sorts by value
    
- Use `LinkedHashMap` in `Collectors.toMap` to **preserve the sorted order**
    
- For reverse sorting, `.reversed()` works on comparators
    
- Multi-field sorting uses `.thenComparing(...)`
  
```


_proactice_
## 🎯 Goal of This Practice

You will practice sorting:

- `ArrayList`
    
- `List`
    
- `Map`
    
- Using **Streams**
    
- By **id**, **name**, **price**, **quantity**, etc.
    

---

## 📦 1️⃣ Create a Model Class

```java
public class Product {

    private int id;
    private String name;
    private double price;
    private int quantity;

    public Product(int id, String name, double price, int quantity) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    // Getters only (no setters for now)
    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public int getQuantity() {
        return quantity;
    }

    @Override
    public String toString() {
        return "Product{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", price=" + price +
                ", quantity=" + quantity +
                '}';
    }
}

```

---

## 🏗️ 2️⃣ Create a Test Class and Fill Constructor with 10 Objects

```java
import java.util.*;

public class SortPractice {

    private List<Product> products;

    public SortPractice() {
        products = new ArrayList<>();

        products.add(new Product(5, "Laptop", 1200.50, 10));
        products.add(new Product(2, "Mouse", 25.99, 100));
        products.add(new Product(8, "Keyboard", 75.49, 50));
        products.add(new Product(1, "Monitor", 300.00, 20));
        products.add(new Product(10, "USB Cable", 9.99, 200));
        products.add(new Product(3, "Webcam", 89.99, 15));
        products.add(new Product(6, "Headphones", 199.99, 30));
        products.add(new Product(4, "Chair", 150.00, 5));
        products.add(new Product(9, "Desk", 450.00, 3));
        products.add(new Product(7, "Microphone", 129.99, 12));
    }

    public static void main(String[] args) {
        SortPractice sp = new SortPractice();

        // Print original list
        sp.products.forEach(System.out::println);
    }
}

```

---

## 🧠 3️⃣ Practice Tasks (DO NOT CODE YET)

Try these **one by one** 👇  
(Ask me when you get stuck)

### 🔹 List / ArrayList

1. Sort by `id` ascending
    
2. Sort by `id` descending
    
3. Sort by `price`
    
4. Sort by `name` (A → Z)
    
5. Sort by `quantity` descending
    

---

### 🔹 Stream Sorting

6. Use `stream()` to sort by price
    
7. Use `stream()` to sort by name length
    
8. Sort by **price then quantity**
    

---

### 🔹 Map Sorting

Convert to map:

- `Map<Integer, Product>` (id → product)
    
- `Map<String, Product>` (name → product)
    

Then:  
9. Sort map by key  
10. Sort map by product price  
11. Sort map by quantity descending

---

### 🔹 Bonus (Advanced)

12. Sort using **custom Comparator class**
    
13. Sort using **lambda**
    
14. Sort using **Comparator.comparing**
    
15. Sort and collect into a **new list**