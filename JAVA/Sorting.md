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

`Map<String, Integer> map = new HashMap<>(); map.put("Alice", 50); map.put("Bob", 30); map.put("Charlie", 40);  // Sort by key using Comparator.comparing Map<String, Integer> sortedByKey = map.entrySet()         .stream()         .sorted(Comparator.comparing(Map.Entry::getKey))         .collect(Collectors.toMap(                 Map.Entry::getKey,                 Map.Entry::getValue,                 (oldValue, newValue) -> oldValue, // merge function                 LinkedHashMap::new // preserves insertion order         ));  System.out.println(sortedByKey);`

✅ Output:

`{Alice=50, Bob=30, Charlie=40}`

---

# **2. Sorting Map by Value**

`Map<String, Integer> sortedByValue = map.entrySet()         .stream()         .sorted(Comparator.comparing(Map.Entry::getValue))         .collect(Collectors.toMap(                 Map.Entry::getKey,                 Map.Entry::getValue,                 (oldValue, newValue) -> oldValue,                 LinkedHashMap::new         ));  System.out.println(sortedByValue);`

✅ Output:

`{Bob=30, Charlie=40, Alice=50}`

---

# **3. Sorting Map by Value in Reverse**

`Map<String, Integer> sortedByValueDesc = map.entrySet()         .stream()         .sorted(Map.Entry.<String, Integer>comparingByValue().reversed())         .collect(Collectors.toMap(                 Map.Entry::getKey,                 Map.Entry::getValue,                 (oldValue, newValue) -> oldValue,                 LinkedHashMap::new         ));  System.out.println(sortedByValueDesc);`

✅ Output:

`{Alice=50, Charlie=40, Bob=30}`

---

# **4. Multi-level Sorting (by Value then Key)**

`Map<String, Integer> sortedByValueThenKey = map.entrySet()         .stream()         .sorted(             Comparator.comparing(Map.Entry<String, Integer>::getValue)                       .thenComparing(Map.Entry::getKey)         )         .collect(Collectors.toMap(                 Map.Entry::getKey,                 Map.Entry::getValue,                 (oldValue, newValue) -> oldValue,                 LinkedHashMap::new         ));  System.out.println(sortedByValueThenKey);`

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