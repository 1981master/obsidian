```

# ✅ **1. Primitive compare Methods (static compare)**

These compare two primitive values:

- `Integer.compare(int a, int b)`
    
- `Long.compare(long a, long b)`
    
- `Double.compare(double a, double b)`
    
- `Float.compare(float a, float b)`
    
- `Short.compare(short a, short b)`
    
- `Byte.compare(byte a, byte b)`
    
- `Character.compare(char a, char b)`
    
- `Boolean.compare(boolean a, boolean b)`
    

✔ Return -1, 0, or +1  
✔ Handle edge cases (Double: NaN, -0.0, Infinity)

---

# ✅ **2. Comparable<T> — compareTo()**

Classes that implement natural ordering:

- `String.compareTo(String)`
    
- `Integer.compareTo(Integer)`
    
- `Double.compareTo(Double)`
    
- `LocalDate.compareTo(LocalDate)`
    
- `BigDecimal.compareTo(BigDecimal)`
    
- Custom classes implementing:
    

`class User implements Comparable<User> {     public int compareTo(User other) {         return Integer.compare(this.age, other.age);     } }`

✔ Used automatically in sorting  
✔ Natural order of objects

---

# ✅ **3. Comparator — comparing methods**

### **Comparator.comparing(field)**

General comparator for objects.

### Optimized primitives:

- `Comparator.comparingInt(...)`
    
- `Comparator.comparingLong(...)`
    
- `Comparator.comparingDouble(...)`
    

### Custom comparator:

- `Comparator.comparing(field, customComparator)`
    

Example:

`Comparator<User> c = Comparator.comparing(User::getName);`

---

# ✅ **4. Comparator — thenComparing methods**

Used for **multi-field sorting**:

- `thenComparing(...)`
    
- `thenComparingInt(...)`
    
- `thenComparingLong(...)`
    
- `thenComparingDouble(...)`
    
- `thenComparing(field, customComparator)`
    

---

# ✅ **5. Comparator Ordering Tools**

- `.reversed()`  
    Reverse sort direction.
    
- `Comparator.reverseOrder()`  
    Reverse natural order.
    
- `Comparator.naturalOrder()`  
    Natural Comparable order.
    

---

# ✅ **6. Null-handling Comparators**

Handle null values safely:

- `Comparator.nullsFirst(comparator)`
    
- `Comparator.nullsLast(comparator)`
    

Example:

`Comparator.nullsLast(Comparator.comparing(User::getName))`

---

# ✅ **7. Comparator Constants & Static Methods**

### **Comparing with identity**

- `Comparator.identity()`  
    Compares objects by identity hashcode (rarely used).
    

### **Comparing enums**

Enums are naturally Comparable.

---

# ✅ **8. Manual comparison inside lambdas**

You can always manually compare:

`(a, b) -> Double.compare(a.getSalary(), b.getSalary())`

Or multi-field:

`(u1, u2) -> {     int r = Integer.compare(u1.getAge(), u2.getAge());     if (r != 0) return r;     return u1.getName().compareTo(u2.getName()); }`

---

# ✅ **9. Objects utility methods**

### **Objects.compare(a, b, comparator)**

Uses comparator or handles nulls.

`Objects.compare(a, b, Comparator.naturalOrder());`

### **Objects.equals(a, b)** (related but not sorting)

Null-safe equals.

---

# ⭐ **FULL LIST SUMMARY (everything Java provides)**

### ✔ Primitive compare

### ✔ Comparable.compareTo()

### ✔ Comparator.comparing

### ✔ Comparator.comparingInt/Long/Double

### ✔ Comparator.thenComparing variants

### ✔ Comparator.naturalOrder

### ✔ Comparator.reverseOrder

### ✔ Comparator.reversed

### ✔ Comparator.nullsFirst

### ✔ Comparator.nullsLast

### ✔ Comparator.comparing with custom comparator

### ✔ Manual comparisons with compare methods

### ✔ Objects.compare

### ✔ String compareTo + case-insensitive orders

### ✔ BigDecimal compareTo

### ✔ Enum compareTo

**That’s the ENTIRE Java comparison toolkit.  
There is no other major comparing API in Java.**




# 🔥 Summary Table — Everything you asked for
# 🔥 Comparator & Compare Methods — Complete Summary

## 1. Primitive Compare Methods
Used to compare primitive values:

- `Integer.compare(a, b)`
- `Double.compare(a, b)`
- `Long.compare(a, b)`
- `Boolean.compare(a, b)`

---

## 2. Basic Field Comparing
Creates a comparator based on a field:

- `Comparator.comparing(User::getName)`

---

## 3. Optimized Primitive Comparing
Faster versions for primitive fields:

- `Comparator.comparingInt(User::getAge)`
- `Comparator.comparingLong(User::getId)`
- `Comparator.comparingDouble(User::getSalary)`

---

## 4. Multi-Field Comparisons
Used for sorting by more than one field:

- `thenComparing(User::getName)`
- `thenComparingInt(User::getAge)`
- `thenComparingDouble(User::getSalary)`

---

## 5. Null Handling
Safely sort fields that may be null:

- `Comparator.nullsFirst(...)`
- `Comparator.nullsLast(...)`

---

## 6. Ordering Helpers
Change sort direction or style:

- `.reversed()`
- `Comparator.naturalOrder()`
- `Comparator.reverseOrder()`

---

## 7. Custom Comparators
Use your own comparator for a field:

- `Comparator.comparing(User::getName, String.CASE_INSENSITIVE_ORDER)`

---

## 8. Manual Comparison Lambda
For full control:

- `(a, b) -> Double.compare(a.getSalary(), b.getSalary())`

---

## 9. Java Comparable’s compareTo()
Used when classes implement `Comparable<T>`:

- `"Alice".compareTo("Bob")`
- `LocalDate.now().compareTo(otherDate)`
- `BigDecimal.valueOf(a).compareTo(b)`
  
# Comparing on Maps
class User {
    private String name;
    private Map<String, Integer> scores;

    public User(String name, Map<String, Integer> scores) {
        this.name = name;
        this.scores = scores;
    }

    public String getName() { return name; }
    public Map<String, Integer> getScores() { return scores; }

    @Override
    public String toString() {
        return name + " " + scores;
    }
}
2. Comparing by a Map property
You cannot directly use Comparator.comparing(User::getScores), because Map does not implement Comparable.
You need to extract some value from the map (like size, sum of values, a specific key).

Example 1 — Compare by Map size
java
Copy code
List<User> users = new ArrayList<>();
users.add(new User("Alice", Map.of("Math", 90, "English", 80)));
users.add(new User("Bob", Map.of("Math", 70)));
users.add(new User("Charlie", Map.of("Math", 80, "English", 85, "Science", 95)));

users.sort(Comparator.comparing(u -> u.getScores().size()));

users.forEach(System.out::println);
✅ Output:

Copy code
Bob {Math=70}
Alice {Math=90, English=80}
Charlie {Math=80, English=85, Science=95}
Example 2 — Compare by a specific key in Map
java
Copy code
users.sort(Comparator.comparing(u -> u.getScores().getOrDefault("Math", 0)));

users.forEach(System.out::println);
✅ Output:

Copy code
Bob {Math=70}
Charlie {Math=80, English=85, Science=95}
Alice {Math=90, English=80}

```