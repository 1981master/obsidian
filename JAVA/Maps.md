```
## **A. General Map Interface (10 Q&A)**

**1. What is the Java Map interface used for?**  
It stores key–value pairs where each key is unique.

**2. How does Map differ from Collection?**  
Map stores key-value pairs, while Collection stores individual elements.

**3. What happens when you insert a duplicate key?**  
The previous value is replaced with the new value.

**4. Can a Map contain duplicate values?**  
Yes. Only keys must be unique.

**5. What does “key hashing” mean?**  
Converting a key into a hash number used to locate its bucket.

**6. What affects the performance of a hash-based Map?**  
Hash quality, load factor, capacity, and collision rate.

**7. What is a hash collision?**  
Two keys generate the same hash and go into the same bucket.

**8. How does resizing work in hash-based maps?**  
When load factor is exceeded, capacity doubles and entries are rehashed.

**9. What is load factor?**  
A threshold ratio (default 0.75) that triggers resizing.

**10. What is the difference between fail-fast and fail-safe iterators?**  
Fail-fast throws exceptions on modification; fail-safe works on a copy.

---

## **B. HashMap (15 Q&A)**

**11. What is HashMap?**  
A non-synchronized map using hashing; high performance.

**12. Does HashMap allow null keys and values?**  
Yes, one null key and many null values.

**13. Time complexity of operations?**  
Average O(1), worst-case O(log n) after Java 8.

**14. How does HashMap handle collisions?**  
Using linked lists or tree nodes (red-black tree after Java 8).

**15. What is a bucket?**  
A slot in the internal array where entries with the same hash are stored.

**16. Why were bucket linked lists replaced with trees?**  
To improve worst-case performance from O(n) to O(log n).

**17. What is treeification?**  
Converting a linked list bucket to a red-black tree when chain is long.

**18. When does HashMap treeify buckets?**  
When bucket size exceeds 8 and capacity is at least 64.

**19. How does HashMap compute hashes?**  
It mixes key.hashCode() bits to reduce collisions.

**20. What degrades HashMap performance?**  
Poorly implemented hashCode(), too many collisions, high load factor.

**21. Is HashMap thread-safe?**  
No, it is not synchronized.

**22. Can HashMap be used in multithreading?**  
Not without manual synchronization.

**23. What happens when two keys have the same hashCode?**  
They are placed in the same bucket.

**24. Why isn’t HashMap suitable for concurrency?**  
Concurrent modification may cause lost updates or infinite loops.

**25. Default initial capacity and load factor?**  
Capacity 16, load factor 0.75.

---

## **C. LinkedHashMap (10 Q&A)**

**26. What is LinkedHashMap?**  
A HashMap with predictable iteration order.

**27. Difference from HashMap?**  
Maintains insertion or access order.

**28. How does it maintain order?**  
With a doubly linked list of entries.

**29. What is access-order mode?**  
Entries move to the end when accessed.

**30. Why can LinkedHashMap implement LRU cache?**  
Access order + removeEldestEntry() allows eviction policy.

**31. Does it allow null keys and values?**  
Yes.

**32. What is the space overhead?**  
Extra pointers for the linked list.

**33. What internal structure does it use?**  
Hash table + doubly linked list.

**34. Is LinkedHashMap thread-safe?**  
No.

**35. When choose LinkedHashMap over HashMap?**  
When predictable iteration order is required.

---

## **D. TreeMap (15 Q&A)**

**36. What is TreeMap?**  
A sorted map implemented using a Red-Black Tree.

**37. Does TreeMap allow null keys?**  
No. Null keys throw NullPointerException.

**38. How are keys sorted?**  
By natural ordering or a custom Comparator.

**39. Time complexity?**  
O(log n) for insert, delete, search.

**40. What data structure is used?**  
A Red-Black Tree.

**41. What is a Red-Black Tree?**  
A balanced binary search tree ensuring O(log n) operations.

**42. How does comparator affect ordering?**  
It defines the sorting logic for keys.

**43. What if comparator is inconsistent with equals()?**  
Unexpected behavior like duplicates or missing entries.

**44. Why is TreeMap slower than HashMap?**  
Due to tree traversal instead of hashing.

**45. Can TreeMap store duplicate keys?**  
No.

**46. What happens with null keys?**  
NullPointerException.

**47. When use TreeMap?**  
When sorted keys are required.

**48. How do TreeMap iterators behave?**  
They iterate in sorted order.

**49. Is TreeMap thread-safe?**  
No.

**50. What sorted operations does TreeMap support?**  
headMap, tailMap, subMap, firstKey, lastKey.

---

## **E. Hashtable (10 Q&A)**

**51. What is Hashtable?**  
A synchronized hash map from early Java.

**52. Why is it legacy?**  
Outdated performance model; replaced by ConcurrentHashMap.

**53. Does it allow null keys or values?**  
No.

**54. How is it synchronized?**  
Entire table is locked on every operation.

**55. How does it differ from HashMap?**  
Hashtable is synchronized; HashMap is not and allows nulls.

**56. Why is Hashtable slower?**  
Full-table lock on each operation.

**57. Should it be used today?**  
No; use ConcurrentHashMap instead.

**58. How does it handle collisions?**  
Chained buckets like HashMap (before Java 8).

**59. Default capacity/load factor?**  
Capacity 11, load factor 0.75.

**60. Is Hashtable fail-fast?**  
Yes.

---

## **F. ConcurrentHashMap (15 Q&A)**

**61. What is ConcurrentHashMap?**  
A high-performance thread-safe map.

**62. Why preferred over Hashtable?**  
Allows concurrent access without locking whole map.

**63. How does it provide thread safety?**  
Uses fine-grained locking and CAS operations.

**64. Why does it forbid null keys/values?**  
To avoid ambiguity between null-value and missing key.

**65. What is segmentation?**  
Older versions used segments for partial locking.

**66. How segmentation changed after Java 8?**  
Segments removed; uses synchronized blocks + CAS on nodes.

**67. What is lock striping?**  
Different parts of the map are locked independently.

**68. How does resizing work?**  
Multiple threads help in resizing concurrently.

**69. Are reads blocking?**  
No; reads are lock-free.

**70. What is weakly consistent iteration?**  
Iterator reflects changes during iteration but not guaranteed.

**71. Is ConcurrentHashMap fully lock-free?**  
Reads are; writes use minimal locking.

**72. What operations require locking?**  
Structural modifications (put, remove) may lock individual bins.

**73. How does computeIfAbsent work?**  
Atomically computes and inserts a value if key absent.

**74. Where is it best used?**  
High-concurrency systems (web servers, caches).

**75. Is it safe for high traffic?**  
Yes.

---

## **G. WeakHashMap (10 Q&A)**

**76. What is WeakHashMap?**  
A map where keys are weakly referenced and removed by GC.

**77. What is a weak reference?**  
A reference that doesn’t prevent the object from being garbage collected.

**78. Why does WeakHashMap auto-remove keys?**  
Because keys use weak references.

**79. Does it allow null keys/values?**  
Yes.

**80. Why useful for caching?**  
Entries disappear when keys are no longer strongly referenced.

**81. How does GC remove entries?**  
When key is garbage collected, its entry is removed automatically.

**82. What if a key has a strong reference elsewhere?**  
It will NOT be removed.

**83. Is it thread-safe?**  
No.

**84. How does it differ from HashMap?**  
Keys are weak; entries auto-removed.

**85. When NOT to use WeakHashMap?**  
When data must persist reliably.

---

## **H. IdentityHashMap (10 Q&A)**

**86. What is IdentityHashMap?**  
A map that uses reference equality (==) for keys.

**87. How does it compare keys?**  
Using ==, not equals().

**88. Why use == instead of equals()?**  
Useful for object identity tracking.

**89. Issues with IdentityHashMap?**  
Logically equal keys may be treated as different.

**90. Does it allow null keys?**  
Yes.

**91. Why not commonly used?**  
Most applications need logical equality, not identity.

**92. Performance characteristics?**  
Fast due to simpler comparison.

**93. Difference from HashMap?**  
HashMap uses equals(); IdentityHashMap uses ==.

**94. When use IdentityHashMap?**  
Serialization frameworks, object tracking.

**95. What if keys equal but not identical?**  
They are treated as separate entries.

---

## **I. Advanced Map Behavior (5 Q&A)**

**96. What is the memory overhead of maps?**  
Hash tables store arrays, nodes, and linked structures.

**97. How does Java optimize hashing?**  
Bit mixing and spreading to reduce collisions.

**98. Impact of bad hashCode()?**  
Buckets become long; performance degrades drastically.

**99. What causes infinite loops in maps?**  
Concurrent modifications on non-thread-safe maps.

**100. Why is mutating keys dangerous?**  
Hash or ordering changes cause unreachable entries.
```

```Java
import java.util.*;
import java.util.concurrent.ConcurrentHashMap;
import java.util.function.Function;
import java.util.stream.Collectors;
import java.util.stream.Stream;

/**
 * MapInterviewExamples
 * Single-file collection of 100+ Map-related coding examples (questions -> code answers).
 *
 * Each method is labeled with the question number from the list provided earlier.
 *
 * Compile with: javac MapInterviewExamples.java
 * Run: java MapInterviewExamples
 *
 * Most methods are small utilities demonstrating typical Map tasks.
 */
public class MapInterviewExamples {

    // 1. Create a HashMap and insert key–value pairs
    public static Map<String, Integer> q1_createHashMap() {
        Map<String, Integer> map = new HashMap<>();
        map.put("A", 1);
        map.put("B", 2);
        return map;
    }

    // 2. Retrieve a value from a Map
    public static Integer q2_getValue(Map<String, Integer> map, String key) {
        return map.get(key);
    }

    // 3. Check if a key exists
    public static boolean q3_containsKey(Map<?, ?> map, Object key) {
        return map.containsKey(key);
    }

    // 4. Check if a value exists
    public static boolean q4_containsValue(Map<?, ?> map, Object value) {
        return map.containsValue(value);
    }

    // 5. Iterate over keys
    public static List<Object> q5_iterateKeys(Map<?, ?> map) {
        List<Object> keys = new ArrayList<>();
        for (Object k : map.keySet()) keys.add(k);
        return keys;
    }

    // 6. Iterate over values
    public static List<Object> q6_iterateValues(Map<?, ?> map) {
        List<Object> vals = new ArrayList<>();
        for (Object v : map.values()) vals.add(v);
        return vals;
    }

    // 7. Iterate over entries
    public static List<String> q7_iterateEntries(Map<?, ?> map) {
        List<String> entries = new ArrayList<>();
        for (Map.Entry<?, ?> e : map.entrySet()) {
            entries.add(e.getKey() + "=" + e.getValue());
        }
        return entries;
    }

    // 8. Remove a key
    public static <K, V> V q8_removeKey(Map<K, V> map, K key) {
        return map.remove(key);
    }

    // 9. Replace a value
    public static <K, V> void q9_replaceValue(Map<K, V> map, K key, V newValue) {
        map.replace(key, newValue);
    }

    // 10. Get value with a default
    public static <K, V> V q10_getOrDefault(Map<K, V> map, K key, V defaultValue) {
        return map.getOrDefault(key, defaultValue);
    }

    // 11. Merge values
    public static void q11_mergeValues(Map<String, Integer> map, String key, Integer toAdd) {
        map.merge(key, toAdd, Integer::sum);
    }

    // 12. Compute new value
    public static void q12_compute(Map<String, Integer> map, String key) {
        map.compute(key, (k, v) -> v == null ? 1 : v + 1);
    }

    // 13. Compute if absent
    public static void q13_computeIfAbsent(Map<String, Integer> map, String key) {
        map.computeIfAbsent(key, k -> 100);
    }

    // 14. Compute if present
    public static void q14_computeIfPresent(Map<String, Integer> map, String key) {
        map.computeIfPresent(key, (k, v) -> v + 10);
    }

    // 15. Find first repeated word using HashSet (via map-style logic)
    public static String q15_firstRepeated(String[] arr) {
        Set<String> set = new HashSet<>();
        for (String s : arr) {
            if (!set.add(s)) return s;
        }
        return null;
    }

    // 16. Count frequency of characters
    public static Map<Character, Integer> q16_charFrequency(String s) {
        Map<Character, Integer> freq = new HashMap<>();
        for (char c : s.toCharArray()) freq.put(c, freq.getOrDefault(c, 0) + 1);
        return freq;
    }

    // 17. Sort a Map by keys (TreeMap)
    public static <K extends Comparable<? super K>, V> Map<K, V> q17_sortByKey(Map<K, V> map) {
        return new TreeMap<>(map);
    }

    // 18. Sort a Map by values (ascending)
    public static <K, V extends Comparable<? super V>> Map<K, V> q18_sortByValue(Map<K, V> map) {
        return map.entrySet().stream()
                .sorted(Map.Entry.comparingByValue())
                .collect(Collectors.toMap(
                        Map.Entry::getKey, Map.Entry::getValue,
                        (a, b) -> a, LinkedHashMap::new));
    }

    // 19. Create a LinkedHashMap (preserve insertion order)
    public static Map<String, Integer> q19_linkedHashMapExample() {
        return new LinkedHashMap<>();
    }

    // 20. Create a LRU Cache using LinkedHashMap
    public static class LRUCache<K, V> extends LinkedHashMap<K, V> {
        private final int capacity;
        public LRUCache(int capacity) {
            super(capacity, 0.75f, true);
            this.capacity = capacity;
        }
        @Override
        protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
            return size() > capacity;
        }
    }

    // 21. Using ConcurrentHashMap
    public static Map<String, Integer> q21_concurrentHashMapExample() {
        return new ConcurrentHashMap<>();
    }

    // 22. Thread-safe updates using ConcurrentHashMap
    public static void q22_threadSafeUpdate(ConcurrentHashMap<String, Integer> map, String key, int value) {
        map.merge(key, value, Integer::sum);
    }

    // 23. WeakHashMap example
    public static Map<Object, String> q23_weakHashMapExample() {
        return new WeakHashMap<>();
    }

    // 24. IdentityHashMap example
    public static Map<Object, String> q24_identityHashMapExample() {
        return new IdentityHashMap<>();
    }

    // 25. Detect duplicates in an array (frequency map)
    public static Map<Integer, Integer> q25_countFrequencies(int[] arr) {
        Map<Integer, Integer> m = new HashMap<>();
        for (int x : arr) m.put(x, m.getOrDefault(x, 0) + 1);
        return m;
    }

    // 26. Most frequent element
    public static Integer q26_mostFrequent(int[] arr) {
        Map<Integer, Integer> freq = q25_countFrequencies(arr);
        int max = -1, elem = Integer.MIN_VALUE;
        for (Map.Entry<Integer, Integer> e : freq.entrySet()) {
            if (e.getValue() > max) { max = e.getValue(); elem = e.getKey(); }
        }
        return elem == Integer.MIN_VALUE ? null : elem;
    }

    // 27. Group items by type (generic)
    public static <K, V> void q27_groupBy(Map<K, List<V>> container, K key, V value) {
        container.computeIfAbsent(key, k -> new ArrayList<>()).add(value);
    }

    // 28. Convert Map to List of keys
    public static <K> List<K> q28_keysToList(Map<K, ?> map) {
        return new ArrayList<>(map.keySet());
    }

    // 29. Convert Map to List of values
    public static <V> List<V> q29_valuesToList(Map<?, V> map) {
        return new ArrayList<>(map.values());
    }

    // 30. Reverse a Map (swap keys & values) - NOTE: values must be unique
    public static <K, V> Map<V, K> q30_reverseMap(Map<K, V> map) {
        Map<V, K> rev = new HashMap<>();
        for (Map.Entry<K, V> e : map.entrySet()) rev.put(e.getValue(), e.getKey());
        return rev;
    }

    // 31. Two Sum using HashMap (return indices)
    public static int[] q31_twoSum(int[] nums, int target) {
        Map<Integer, Integer> m = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int diff = target - nums[i];
            if (m.containsKey(diff)) return new int[]{m.get(diff), i};
            m.put(nums[i], i);
        }
        return null;
    }

    // 32. Find intersection of two arrays (including duplicates)
    public static int[] q32_intersection(int[] a, int[] b) {
        Map<Integer, Integer> freq = new HashMap<>();
        for (int x : a) freq.put(x, freq.getOrDefault(x, 0) + 1);
        List<Integer> res = new ArrayList<>();
        for (int x : b) {
            int c = freq.getOrDefault(x, 0);
            if (c > 0) {
                res.add(x);
                freq.put(x, c - 1);
            }
        }
        return res.stream().mapToInt(i -> i).toArray();
    }

    // 33. Remove entries with null values
    public static <K, V> void q33_removeNullValues(Map<K, V> map) {
        map.values().removeIf(Objects::isNull);
    }

    // 34. Filter Map by predicate on value
    public static <K, V> Map<K, V> q34_filterByValue(Map<K, V> map, java.util.function.Predicate<V> p) {
        return map.entrySet().stream()
                .filter(e -> p.test(e.getValue()))
                .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
    }

    // 35. Convert Map to JSON-like String
    public static String q35_mapToJson(Map<String, Object> map) {
        return map.entrySet().stream()
                .map(e -> "\"" + e.getKey() + "\":" + (e.getValue() == null ? "null" : "\"" + e.getValue().toString() + "\""))
                .collect(Collectors.joining(",", "{", "}"));
    }

    // 36. Detect if Map is empty
    public static boolean q36_isEmpty(Map<?, ?> map) {
        return map.isEmpty();
    }

    // 37. Add all entries from another Map
    public static <K, V> void q37_putAll(Map<K, V> dest, Map<? extends K, ? extends V> src) {
        dest.putAll(src);
    }

    // 38. Clear map
    public static void q38_clear(Map<?, ?> map) {
        map.clear();
    }

    // 39. Find key by value (first match)
    public static <K, V> K q39_findKeyByValue(Map<K, V> map, V value) {
        for (Map.Entry<K, V> e : map.entrySet()) if (Objects.equals(e.getValue(), value)) return e.getKey();
        return null;
    }

    // 40. Convert list of strings to frequency map
    public static Map<String, Long> q40_listToFreq(List<String> list) {
        return list.stream().collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    }

    // 41. Check if two maps are equal (keys and values)
    public static boolean q41_mapsEqual(Map<?, ?> a, Map<?, ?> b) {
        return Objects.equals(a, b);
    }

    // 42. Compare two maps and get differences (keys added/removed/changed)
    public static Map<String, Object> q42_mapsDifference(Map<String, Object> a, Map<String, Object> b) {
        Map<String, Object> diff = new HashMap<>();
        Set<String> all = new HashSet<>();
        all.addAll(a.keySet());
        all.addAll(b.keySet());
        for (String k : all) {
            Object va = a.get(k), vb = b.get(k);
            if (!Objects.equals(va, vb)) diff.put(k, Arrays.asList(va, vb));
        }
        return diff;
    }

    // 43. Convert map to list of entries
    public static <K, V> List<Map.Entry<K, V>> q43_mapToEntryList(Map<K, V> map) {
        return new ArrayList<>(map.entrySet());
    }

    // 44. Convert list of pairs into map
    public static <K, V> Map<K, V> q44_pairsToMap(List<Map.Entry<K, V>> pairs) {
        return pairs.stream().collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
    }

    // 45. Implement a simple custom hash function for strings
    public static int q45_customHash(String s) {
        // DJB2-like simple hash
        int hash = 5381;
        for (char c : s.toCharArray()) hash = ((hash << 5) + hash) + c;
        return hash;
    }

    // 46. Detect collision in HashMap simulation (two different keys same hash)
    public static boolean q46_hasCollision(List<String> keys) {
        Map<Integer, List<String>> buckets = new HashMap<>();
        for (String k : keys) {
            int h = q45_customHash(k);
            buckets.computeIfAbsent(h, x -> new ArrayList<>()).add(k);
            if (buckets.get(h).size() > 1) return true;
        }
        return false;
    }

    // 47. Implement multimap (Map<K, List<V>>)
    public static <K, V> void q47_putInMultiMap(Map<K, List<V>> mm, K key, V value) {
        mm.computeIfAbsent(key, k -> new ArrayList<>()).add(value);
    }

    // 48. Implement bidirectional map (simple naive)
    public static class BiMap<K, V> {
        private final Map<K, V> kv = new HashMap<>();
        private final Map<V, K> vk = new HashMap<>();
        public void put(K k, V v) {
            if (kv.containsKey(k)) vk.remove(kv.get(k));
            if (vk.containsKey(v)) kv.remove(vk.get(v));
            kv.put(k, v);
            vk.put(v, k);
        }
        public V get(K k) { return kv.get(k); }
        public K getKey(V v) { return vk.get(v); }
    }

    // 49. Convert enum -> map (name -> enum)
    public static <E extends Enum<E>> Map<String, E> q49_enumToMap(Class<E> enumClass) {
        Map<String, E> m = new HashMap<>();
        for (E e : enumClass.getEnumConstants()) m.put(e.name(), e);
        return m;
    }

    // 50. Find all keys having same value
    public static <K, V> List<K> q50_keysWithValue(Map<K, V> map, V value) {
        return map.entrySet().stream().filter(e -> Objects.equals(e.getValue(), value)).map(Map.Entry::getKey).collect(Collectors.toList());
    }

    // 51. Initialize map using static block
    public static Map<String, Integer> q51_staticInitExample() {
        Map<String, Integer> m = new HashMap<String, Integer>() {{
            put("one", 1);
            put("two", 2);
        }};
        return m;
    }

    // 52. Copy-on-write map example (using Collections.synchronizedMap as stand-in)
    public static Map<String, String> q52_copyOnWriteExample() {
        return Collections.synchronizedMap(new HashMap<>());
    }

    // 53. Sync map using Collections.synchronizedMap
    public static Map<String, Integer> q53_synchronizedMap() {
        return Collections.synchronizedMap(new HashMap<>());
    }

    // 54. Use TreeMap with custom Comparator (reverse order)
    public static <K, V> Map<K, V> q54_treeMapCustom(Comparator<K> comp) {
        return new TreeMap<>(comp);
    }

    // 55. Sort map descending by keys
    public static <K extends Comparable<? super K>, V> Map<K, V> q55_sortDescByKeys(Map<K, V> map) {
        return map.entrySet().stream()
                .sorted(Collections.reverseOrder(Map.Entry.comparingByKey()))
                .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue, (a,b)->a, LinkedHashMap::new));
    }

    // 56. Sort map descending by values
    public static <K, V extends Comparable<? super V>> Map<K, V> q56_sortDescByValues(Map<K, V> map) {
        return map.entrySet().stream()
                .sorted(Collections.reverseOrder(Map.Entry.comparingByValue()))
                .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue, (a,b)->a, LinkedHashMap::new));
    }

    // 57. Shuffle map values (returns new map with same keys order but shuffled values)
    public static <K, V> Map<K, V> q57_shuffleValues(Map<K, V> map) {
        List<V> vals = new ArrayList<>(map.values());
        Collections.shuffle(vals);
        Map<K, V> result = new LinkedHashMap<>();
        Iterator<V> it = vals.iterator();
        for (K k : map.keySet()) result.put(k, it.next());
        return result;
    }

    // 58. Convert map to Properties
    public static Properties q58_mapToProperties(Map<String, String> map) {
        Properties p = new Properties();
        p.putAll(map);
        return p;
    }

    // 59. Read properties into map
    public static Map<String, String> q59_propertiesToMap(Properties p) {
        Map<String, String> m = new HashMap<>();
        for (String name : p.stringPropertyNames()) m.put(name, p.getProperty(name));
        return m;
    }

    // 60. Convert map to CSV (simple key,value lines)
    public static String q60_mapToCsv(Map<String, ?> map) {
        return map.entrySet().stream()
                .map(e -> e.getKey() + "," + (e.getValue() == null ? "" : e.getValue().toString()))
                .collect(Collectors.joining("\n"));
    }

    // 61. Read CSV into map (assumes two columns key,value)
    public static Map<String, String> q61_csvToMap(String csv) {
        Map<String, String> m = new HashMap<>();
        String[] lines = csv.split("\\r?\\n");
        for (String line : lines) {
            String[] parts = line.split(",", 2);
            if (parts.length >= 1) m.put(parts[0], parts.length == 2 ? parts[1] : "");
        }
        return m;
    }

    // 62. Convert map to XML (very simple)
    public static String q62_mapToXml(Map<String, ?> map, String root) {
        StringBuilder sb = new StringBuilder();
        sb.append("<").append(root).append(">");
        for (Map.Entry<String, ?> e : map.entrySet()) {
            sb.append("<").append(e.getKey()).append(">");
            sb.append(e.getValue() == null ? "" : e.getValue().toString());
            sb.append("</").append(e.getKey()).append(">");
        }
        sb.append("</").append(root).append(">");
        return sb.toString();
    }

    // 63. Remove entries while iterating safely
    public static <K, V> void q63_removeWhileIterating(Map<K, V> map, java.util.function.Predicate<Map.Entry<K, V>> predicate) {
        Iterator<Map.Entry<K, V>> it = map.entrySet().iterator();
        while (it.hasNext()) {
            Map.Entry<K, V> e = it.next();
            if (predicate.test(e)) it.remove();
        }
    }

    // 64. Store objects in Map (generic example)
    public static class Q64_Item { public String name; public Q64_Item(String n) { name = n; } }
    public static Map<String, Q64_Item> q64_storeObjects() {
        Map<String, Q64_Item> map = new HashMap<>();
        map.put("item1", new Q64_Item("a"));
        return map;
    }

    // 65. Map inside Map (nested map)
    public static Map<String, Map<String, Integer>> q65_nestedMap() {
        Map<String, Map<String, Integer>> m = new HashMap<>();
        m.computeIfAbsent("outer", k -> new HashMap<>()).put("inner", 1);
        return m;
    }

    // 66. Map of sets
    public static <K, V> void q66_mapOfSetsPut(Map<K, Set<V>> map, K key, V value) {
        map.computeIfAbsent(key, k -> new HashSet<>()).add(value);
    }

    // 67. Map of lists
    public static <K, V> void q67_mapOfListsPut(Map<K, List<V>> map, K key, V value) {
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(value);
    }

    // 68. Find longest key (string length)
    public static String q68_longestKey(Map<String, ?> map) {
        return map.keySet().stream().max(Comparator.comparingInt(String::length)).orElse(null);
    }

    // 69. Find largest value (assuming Comparable)
    public static <V extends Comparable<? super V>> V q69_largestValue(Map<?, V> map) {
        return map.values().stream().max(Comparator.naturalOrder()).orElse(null);
    }

    // 70. Flatten nested map keys to dot notation
    public static Map<String, Object> q70_flattenNested(Map<String, Map<String, Object>> nested) {
        Map<String, Object> flat = new HashMap<>();
        for (Map.Entry<String, Map<String, Object>> e : nested.entrySet()) {
            String prefix = e.getKey();
            for (Map.Entry<String, Object> inner : e.getValue().entrySet()) {
                flat.put(prefix + "." + inner.getKey(), inner.getValue());
            }
        }
        return flat;
    }

    // 71. Build adjacency map (graph)
    public static Map<Integer, List<Integer>> q71_buildAdjacency(int[][] edges) {
        Map<Integer, List<Integer>> adj = new HashMap<>();
        for (int[] e : edges) {
            adj.computeIfAbsent(e[0], k -> new ArrayList<>()).add(e[1]);
            // for undirected, add reverse: adj.computeIfAbsent(e[1], k -> new ArrayList<>()).add(e[0]);
        }
        return adj;
    }

    // 72. BFS using map (graph traversal)
    public static List<Integer> q72_bfs(Map<Integer, List<Integer>> graph, int start) {
        List<Integer> order = new ArrayList<>();
        Queue<Integer> q = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();
        q.add(start); visited.add(start);
        while (!q.isEmpty()) {
            int u = q.poll();
            order.add(u);
            for (int v : graph.getOrDefault(u, Collections.emptyList())) {
                if (!visited.contains(v)) { visited.add(v); q.add(v); }
            }
        }
        return order;
    }

    // 73. DFS using map (recursive)
    public static List<Integer> q73_dfs(Map<Integer, List<Integer>> graph, int start) {
        List<Integer> order = new ArrayList<>();
        Set<Integer> visited = new HashSet<>();
        dfsHelper(graph, start, visited, order);
        return order;
    }
    private static void dfsHelper(Map<Integer, List<Integer>> g, int u, Set<Integer> vis, List<Integer> out) {
        if (vis.contains(u)) return;
        vis.add(u);
        out.add(u);
        for (int v : g.getOrDefault(u, Collections.emptyList())) dfsHelper(g, v, vis, out);
    }

    // 74. Detect cycle using map (directed graph)
    public static boolean q74_detectCycle(Map<Integer, List<Integer>> graph) {
        Set<Integer> white = new HashSet<>(graph.keySet()), gray = new HashSet<>(), black = new HashSet<>();
        for (Integer node : new HashSet<>(white)) if (dfsCycle(node, graph, white, gray, black)) return true;
        return false;
    }
    private static boolean dfsCycle(int u, Map<Integer, List<Integer>> g, Set<Integer> white, Set<Integer> gray, Set<Integer> black) {
        white.remove(u); gray.add(u);
        for (int v : g.getOrDefault(u, Collections.emptyList())) {
            if (black.contains(v)) continue;
            if (gray.contains(v)) return true;
            if (dfsCycle(v, g, white, gray, black)) return true;
        }
        gray.remove(u); black.add(u);
        return false;
    }

    // 75. Cache with TTL using map (simple naive, no scheduling)
    public static class TTLCache<K, V> {
        private final Map<K, V> store = new ConcurrentHashMap<>();
        private final Map<K, Long> expiry = new ConcurrentHashMap<>();
        public void put(K k, V v, long ttlMillis) { store.put(k, v); expiry.put(k, System.currentTimeMillis() + ttlMillis); }
        public V get(K k) {
            Long exp = expiry.get(k);
            if (exp == null || exp < System.currentTimeMillis()) { store.remove(k); expiry.remove(k); return null; }
            return store.get(k);
        }
    }

    // 76. Group anagrams using map
    public static List<List<String>> q76_groupAnagrams(String[] words) {
        Map<String, List<String>> m = new HashMap<>();
        for (String w : words) {
            char[] a = w.toCharArray(); Arrays.sort(a);
            String key = new String(a);
            m.computeIfAbsent(key, k -> new ArrayList<>()).add(w);
        }
        return new ArrayList<>(m.values());
    }

    // 77. Frequency sort array (by number frequency descending)
    public static Integer[] q77_frequencySort(Integer[] arr) {
        Map<Integer, Long> freq = Arrays.stream(arr).collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
        return Arrays.stream(arr).sorted((a, b) -> {
            int cmp = Long.compare(freq.get(b), freq.get(a));
            return cmp == 0 ? Integer.compare(a, b) : cmp;
        }).toArray(Integer[]::new);
    }

    // 78. Top K frequent elements
    public static List<Integer> q78_topK(int[] arr, int k) {
        Map<Integer, Integer> freq = new HashMap<>();
        for (int x : arr) freq.put(x, freq.getOrDefault(x, 0) + 1);
        return freq.entrySet().stream().sorted((a,b)->b.getValue()-a.getValue()).limit(k).map(Map.Entry::getKey).collect(Collectors.toList());
    }

    // 79. Convert string -> map using split key=value pairs separated by &
    public static Map<String, String> q79_stringToMap(String s) {
        Map<String, String> m = new HashMap<>();
        if (s == null || s.isEmpty()) return m;
        String[] parts = s.split("&");
        for (String p : parts) {
            String[] kv = p.split("=", 2);
            m.put(kv[0], kv.length == 2 ? kv[1] : "");
        }
        return m;
    }

    // 80. Count vowels using map
    public static Map<Character, Integer> q80_countVowels(String s) {
        Set<Character> vowels = new HashSet<>(Arrays.asList('a','e','i','o','u'));
        Map<Character, Integer> m = new HashMap<>();
        for (char c : s.toLowerCase().toCharArray()) if (vowels.contains(c)) m.put(c, m.getOrDefault(c,0)+1);
        return m;
    }

    // 81. Find most common word in paragraph
    public static String q81_mostCommonWord(String paragraph) {
        String[] words = paragraph.toLowerCase().replaceAll("[^a-z0-9\\s]", "").split("\\s+");
        Map<String, Integer> freq = new HashMap<>();
        for (String w : words) if (!w.isEmpty()) freq.put(w, freq.getOrDefault(w,0)+1);
        return freq.entrySet().stream().max(Map.Entry.comparingByValue()).map(Map.Entry::getKey).orElse(null);
    }

    // 82. Implement memoization using map (Fibonacci example)
    public static long q82_fibMemo(int n, Map<Integer, Long> memo) {
        if (n <= 1) return n;
        if (memo.containsKey(n)) return memo.get(n);
        long res = q82_fibMemo(n-1, memo) + q82_fibMemo(n-2, memo);
        memo.put(n, res);
        return res;
    }

    // 83. Detect first non-repeating char
    public static Character q83_firstNonRepeating(String s) {
        Map<Character, Integer> freq = new LinkedHashMap<>();
        for (char c : s.toCharArray()) freq.put(c, freq.getOrDefault(c, 0) + 1);
        for (Map.Entry<Character, Integer> e : freq.entrySet()) if (e.getValue() == 1) return e.getKey();
        return null;
    }

    // 84. Detect all non-repeating chars
    public static List<Character> q84_allNonRepeating(String s) {
        Map<Character, Integer> freq = new LinkedHashMap<>();
        for (char c : s.toCharArray()) freq.put(c, freq.getOrDefault(c, 0) + 1);
        return freq.entrySet().stream().filter(e -> e.getValue() == 1).map(Map.Entry::getKey).collect(Collectors.toList());
    }

    // 85. Detect duplicate characters
    public static Set<Character> q85_duplicateChars(String s) {
        Set<Character> seen = new HashSet<>(), dup = new HashSet<>();
        for (char c : s.toCharArray()) if (!seen.add(c)) dup.add(c);
        return dup;
    }

    // 86. Custom LRU cache using map (we made LRUCache earlier)
    public static LRUCache<String, Integer> q86_customLRU(int capacity) {
        return new LRUCache<>(capacity);
    }

    // 87. Store function callbacks in map (Runnable example)
    public static Map<String, Runnable> q87_callbacks() {
        Map<String, Runnable> m = new HashMap<>();
        m.put("sayHi", () -> System.out.println("hi"));
        return m;
    }

    // 88. Create map with initial capacity
    public static <K, V> Map<K, V> q88_mapWithCapacity(int capacity) {
        return new HashMap<>(capacity);
    }

    // 89. Convert Map -> Stream
    public static <K, V> Stream<Map.Entry<K, V>> q89_mapToStream(Map<K, V> map) {
        return map.entrySet().stream();
    }

    // 90. Convert Stream -> Map (keys by function)
    public static <T, K, V> Map<K, V> q90_streamToMap(Stream<T> stream, Function<T, K> keyMapper, Function<T, V> valueMapper) {
        return stream.collect(Collectors.toMap(keyMapper, valueMapper, (a, b) -> a));
    }

    // 91. Identify if map over 75% load factor (approximate)
    public static <K, V> boolean q91_isOverLoadFactor(Map<K, V> map, int capacity, double loadFactor) {
        return map.size() > capacity * loadFactor;
    }

    // 92. Demonstrate fail-fast iterator (throws if modified)
    public static void q92_failFastExample() {
        Map<String, Integer> m = new HashMap<>();
        m.put("a", 1);
        Iterator<String> it = m.keySet().iterator();
        m.put("b", 2); // structural modification
        try {
            it.next(); // may throw ConcurrentModificationException
        } catch (Exception ex) {
            // intentionally empty — in real interview you'd explain CME
        }
    }

    // 93. Demonstrate fail-safe iterator (using ConcurrentHashMap)
    public static void q93_failSafeExample() {
        Map<String, Integer> m = new ConcurrentHashMap<>();
        m.put("a", 1);
        Iterator<String> it = m.keySet().iterator();
        m.put("b", 2); // allowed with no CME
        while (it.hasNext()) {
            it.next();
        }
    }

    // 94. Detect ConcurrentModificationException (example usage)
    public static boolean q94_detectCME() {
        try {
            q92_failFastExample();
            return false;
        } catch (Exception e) {
            return e instanceof ConcurrentModificationException;
        }
    }

    // 95. Use synchronizedMap safely (iterate with synchronized block)
    public static void q95_useSynchronizedMap(Map<String, Integer> syncMap) {
        synchronized (syncMap) {
            for (Map.Entry<String, Integer> e : syncMap.entrySet()) {
                // safe iteration
            }
        }
    }

    // 96. Find key with smallest value
    public static <K, V extends Comparable<? super V>> K q96_keyWithMinValue(Map<K, V> map) {
        return map.entrySet().stream().min(Map.Entry.comparingByValue()).map(Map.Entry::getKey).orElse(null);
    }

    // 97. Convert 2D array to map (first column key, second value)
    public static Map<String, String> q97_2dArrayToMap(String[][] arr) {
        Map<String, String> m = new HashMap<>();
        for (String[] r : arr) if (r.length >= 2) m.put(r[0], r[1]);
        return m;
    }

    // 98. Convert map to 2D array (k,v rows)
    public static String[][] q98_mapTo2dArray(Map<String, String> map) {
        String[][] res = new String[map.size()][2];
        int i = 0;
        for (Map.Entry<String, String> e : map.entrySet()) { res[i][0] = e.getKey(); res[i][1] = e.getValue(); i++; }
        return res;
    }

    // 99. Map to object conversion (simple bean using reflection is heavy — show manual)
    public static class Q99_Person { public String name; public int age; public Q99_Person(){} }
    public static Q99_Person q99_mapToPerson(Map<String, Object> map) {
        Q99_Person p = new Q99_Person();
        p.name = (String) map.getOrDefault("name", null);
        p.age = (int) map.getOrDefault("age", 0);
        return p;
    }

    // 100. Object to map conversion (manual)
    public static Map<String, Object> q100_personToMap(Q99_Person p) {
        Map<String, Object> m = new HashMap<>();
        m.put("name", p.name);
        m.put("age", p.age);
        return m;
    }

    // 101. Using Optional with Maps (get optional)
    public static <K, V> Optional<V> q101_getOptional(Map<K, V> map, K key) {
        return Optional.ofNullable(map.get(key));
    }

    // 102. Remove all keys matching pattern (regex)
    public static void q102_removeMatching(Map<String, ?> map, String regex) {
        Iterator<String> it = new ArrayList<>(map.keySet()).iterator();
        while (it.hasNext()) {
            String k = it.next();
            if (k.matches(regex)) map.remove(k);
        }
    }

    // 103. Clone a HashMap correctly (shallow clone)
    public static <K, V> Map<K, V> q103_clone(Map<K, V> map) {
        return new HashMap<>(map);
    }

    // 104. Serialize and deserialize map (simple to/from string via CSV)
    public static String q104_serializeMap(Map<String, String> map) {
        return q60_mapToCsv(map);
    }
    public static Map<String, String> q104_deserializeMap(String csv) {
        return q61_csvToMap(csv);
    }

    // --- End of examples. Main runs a few to demonstrate compilation.
    public static void main(String[] args) {
        // Quick compile-time smoke test
        Map<String, Integer> map = q1_createHashMap();
        System.out.println("q1: " + map);
        q11_mergeValues(map, "A", 5);
        System.out.println("q11 after merge: " + map);
        System.out.println("q16 freq of 'hello': " + q16_charFrequency("hello"));
        System.out.println("q31 twoSum indexes: " + Arrays.toString(q31_twoSum(new int[]{2,7,11,15}, 9)));
        System.out.println("q35 toJson: " + q35_mapToJson(Collections.singletonMap("k", "v")));
        System.out.println("q45 customHash('abc'): " + q45_customHash("abc"));
        System.out.println("q86 lru test: ");
        LRUCache<String, Integer> lru = q86_customLRU(2);
        lru.put("x", 1); lru.put("y", 2); lru.put("z", 3);
        System.out.println("LRU contents (should have y,z): " + lru.keySet());
    }
}

```



============================================================================
[[Road Map]]

=============================================================================

```
`partitioningBy` is one of the MOST useful collectors in Java Streams.  
It splits your list into **two groups** based on a **boolean condition**.

# ✅ **Basic Syntax**

`Map<Boolean, List<T>> result =     list.stream().collect(Collectors.partitioningBy(item -> condition));`

This always produces:

- `true` → items that match condition
    
- `false` → items that do NOT match condition
    

---

# 📌 Example 1 — Partition Users by Age > 30

`Map<Boolean, List<User>> partition =         users.stream()              .collect(Collectors.partitioningBy(u -> u.getAge() > 30));`

Print:

`System.out.println("Age > 30: " + partition.get(true)); System.out.println("Age ≤ 30: " + partition.get(false));`

---

# 📌 Example 2 — Partition by Salary ≥ 50,000

`Map<Boolean, List<User>> partition =     users.stream()          .collect(Collectors.partitioningBy(u -> u.getSalary() >= 50000));`

---

# 📌 Example 3 — Partition admins vs non-admin users

`Map<Boolean, List<User>> partition =         users.stream()              .collect(Collectors.partitioningBy(u -> u.getRole().equals("Admin")));`

---

# 📌 Example 4 — Partition even/odd numbers

`Map<Boolean, List<Integer>> nums =     IntStream.range(1, 10)              .boxed()              .collect(Collectors.partitioningBy(n -> n % 2 == 0));  System.out.println(nums.get(true));  // even System.out.println(nums.get(false)); // odd`

---

# 📌 Example 5 — Partition on email domain (gmail vs non-gmail)

`Map<Boolean, List<User>> gmailUsers =         users.stream()              .collect(Collectors.partitioningBy(                  u -> u.getEmail().endsWith("@gmail.com")              ));`

---

# 🔥 Advanced Versions

# 📌 Example 6 — Partition + downstream collector

Count how many users > 30:

`Map<Boolean, Long> partition =     users.stream()          .collect(Collectors.partitioningBy(               u -> u.getAge() > 30,               Collectors.counting()          ));`

Result:

`true → count of users > 30   false → count of users ≤ 30`

---

# 📌 Example 7 — Partition + average salary

`Map<Boolean, Double> avgSalary =     users.stream()          .collect(Collectors.partitioningBy(                 u -> u.getAge() > 30,                 Collectors.averagingDouble(User::getSalary)          ));`

---

# 📌 Example 8 — Partition + max user by salary

`Map<Boolean, Optional<User>> maxBySalary =         users.stream()              .collect(Collectors.partitioningBy(                  u -> u.getAge() > 30,                  Collectors.maxBy(Comparator.comparing(User::getSalary))              ));`

---

# 🧠 Summary

|What `partitioningBy` does|Description|
|---|---|
|Splits a list in **two parts**|true-group & false-group|
|Always returns a `Map<Boolean, List<T>>` (or with downstream collectors)||
|Used when your condition is boolean — not a category with many values||


```
[[Stream API]]

==============================================================================
PartitioningBy Vs groupingBy
=
```
# ✅ **1. Partitioning vs Grouping**

## **partitioningBy**

✔ Splits into **exactly 2 groups**  
✔ Based on a **boolean condition**

Example:

`Map<Boolean, List<User>> result =     users.stream().collect(Collectors.partitioningBy(u -> u.getAge() > 30));`

Output structure:

`true  -> users older than 30 false -> users 30 or younger`

---

## **groupingBy**

✔ Splits into **many groups**  
✔ Key can be String, Integer, Enum, etc.

Example:

`Map<String, List<User>> byRole =     users.stream().collect(Collectors.groupingBy(User::getRole));`

Output structure:

`Admin   -> [User1, User5] Manager -> [User2] User    -> [User3, User4]`

---

## 🔥 Comparison Table

|Feature|groupingBy|partitioningBy|
|---|---|---|
|Groups|Many|Only 2 (true/false)|
|Key type|Any type|Boolean|
|Use when|You have categories (city, role, country)|You need a yes/no split|
|Output|Map<K, List<T>>|Map<Boolean, List<T>>|

---

# ✅ **2. Partitioning With Nested Fields**

Let’s apply partitioning on deeper attributes.

---

## **a) Partition by city (NY vs non-NY)**

`Map<Boolean, List<User>> inNY =     users.stream().collect(         Collectors.partitioningBy(u -> u.getAddress().equals("NY"))     );`

---

## **b) Partition by role level (level > 2)**

Assume `Role` class:

`class Role {     private String name;     private int level; }`

Then:

`Map<Boolean, List<User>> highLevel =     users.stream()          .collect(Collectors.partitioningBy(              u -> u.getRole().equals("Admin") || u.getRole().equals("Manager")          ));`

Or with a Role object:

`Map<Boolean, List<User>> highLevel =     users.stream()          .collect(Collectors.partitioningBy(              u -> u.getRole().getLevel() > 2          ));`

---

## **c) Partition by phone country code +1 (USA) vs international**

`Map<Boolean, List<User>> usaPhones =     users.stream()          .collect(Collectors.partitioningBy(              u -> u.getPhone().startsWith("+1")          ));`

---

# ✅ **3. Real-world examples**

---

# **a) Active vs Inactive Users**

Assume `isActive` flag:

`Map<Boolean, List<User>> activeInactive =     users.stream().collect(Collectors.partitioningBy(User::isActive));`

---

# **b) Email Verified vs Not Verified**

`Map<Boolean, List<User>> verified =     users.stream().collect(Collectors.partitioningBy(User::isVerified));`

---

# **c) Admin vs Non-admin**

`Map<Boolean, List<User>> admins =     users.stream().collect(         Collectors.partitioningBy(u -> u.getRole().equals("Admin"))     );`

---

# **d) High salary vs low salary**

Threshold: $60,000

`Map<Boolean, List<User>> salarySplit =     users.stream().collect(         Collectors.partitioningBy(u -> u.getSalary() >= 60000)     );`

---

# **e) Users with missing phone number**

`Map<Boolean, List<User>> missingPhone =     users.stream().collect(         Collectors.partitioningBy(u -> u.getPhone() == null || u.getPhone().isBlank())     );`

---

# **f) Partitioning + Summary Stats (Advanced)**

Average salary of each group (verified/unverified):

`Map<Boolean, Double> avgSalaryVerified =     users.stream().collect(         Collectors.partitioningBy(             User::isVerified,             Collectors.averagingDouble(User::getSalary)         )     );`

---

# **g) Partitioning + max salary by group**

`Map<Boolean, Optional<User>> topSalaries =     users.stream().collect(         Collectors.partitioningBy(             u -> u.getAge() > 30,             Collectors.maxBy(Comparator.comparing(User::getSalary))         )     );`
```
==============================================================================
Partitioning Eg:
```
### ✔ Partitioning + Grouping (hybrid)

### ✔ Partitioning + reduce()

### ✔ Combining multiple conditions with Predicates

### ✔ Complex real-world business rules (VIP customer checks, fraud detection patterns, login attempts, etc.)

Using your preferred **User** example with nested fields (city, role, level).

---

# ✅ **Setup: Example User Class**

`class User {     private String name;     private int age;     private boolean active;     private boolean verified;     private Address address;     private Role role;      // getters + constructor... }  class Address {     private String city;     private String country;     // getters }  class Role {     private String name;     private int level; // 1–5     // getters }`

---

# 🎯 1. **Partitioning + Grouping (Hybrid Logic)**

### → Partition first, then group inside each section.

### Example:

**Partition users by `active` status**,  
and **group each partition by city**.

`Map<Boolean, Map<String, List<User>>> result =     users.stream()          .collect(Collectors.partitioningBy(              User::isActive,              Collectors.groupingBy(u -> u.getAddress().getCity())          ));`

### Result structure:

`{   true:  { "New York": [..], "Dallas": [..], ... }   false: { "Chicago": [..], "LA": [..], ... } }`

This is **partitioning → grouping**.
```
===============================================================================
PartitioningBy Vs Reduce
=
```java
# 🎯 2. **Partitioning + reduce()**

### → Use reduction to compute totals, averages, counts.

### Example:

**Partition by verified/unverified**,  
and **sum ages inside each partition**.

`Map<Boolean, Integer> ageSums =     users.stream()          .collect(Collectors.partitioningBy(              User::isVerified,              Collectors.reducing(0, User::getAge, Integer::sum)          ));`

Output:

`true  → total age of verified users false → total age of unverified users`

---

# 🎯 3. **Partitioning with Multiple Conditions (Predicates)**

### Create reusable predicates:

`Predicate<User> isActive = User::isActive; Predicate<User> isVerified = User::isVerified; Predicate<User> isAdult = u -> u.getAge() >= 18;`

### Example:

**Partition users who are BOTH active AND verified**.

`Map<Boolean, List<User>> partitions =     users.stream()          .collect(Collectors.partitioningBy(              isActive.and(isVerified)          ));`

---

# 🎯 4. **Partitioning with Nested Fields (city, role, level)**

### Example:

Partition by **role level ≥ 3** (senior workers).

`Map<Boolean, List<User>> seniorPartition =     users.stream()          .collect(Collectors.partitioningBy(              u -> u.getRole().getLevel() >= 3          ));`

### Example:

Partition by **city = "New York"**.

`Map<Boolean, List<User>> partitionNY =     users.stream()          .collect(Collectors.partitioningBy(              u -> "New York".equals(u.getAddress().getCity())          ));`

---

# 🎯 5. **Real-world Business Rules Examples**

## ⭐ 5.1. Active Users vs Inactive + Group by Role

`Map<Boolean, Map<String, List<User>>> result =     users.stream()          .collect(Collectors.partitioningBy(              User::isActive,              Collectors.groupingBy(u -> u.getRole().getName())          ));`

---

## ⭐ 5.2. Verified vs Not Verified + Count per city

`Map<Boolean, Map<String, Long>> stats =     users.stream()          .collect(Collectors.partitioningBy(              User::isVerified,              Collectors.groupingBy(                  u -> u.getAddress().getCity(),                  Collectors.counting()              )          ));`

---

## ⭐ 5.3. VIP Customer Logic (Spend > $5000, Level ≥ 3, Verified)

`Predicate<User> isVIP =     u -> u.getRole().getLevel() >= 3 &&          u.isVerified() &&          u.getTotalPurchase() > 5000;  Map<Boolean, List<User>> vipPartitions =     users.stream()          .collect(Collectors.partitioningBy(isVIP));`

---

## ⭐ 5.4 Fraud Detection Example

Pattern:

- **Active but NOT verified**
    
- **Age < 18**
    
- **Different IP logins**
    

`Predicate<User> risky =     u -> u.isActive()           && !u.isVerified()           && u.getAge() < 18           && u.getLoginIPs().size() > 3;  Map<Boolean, List<User>> fraudCheck =     users.stream().collect(Collectors.partitioningBy(risky));`

---

## ⭐ 5.5 Login Attempts Lockout Example

**Locked out if ≥ 5 failed attempts**:

`Map<Boolean, List<User>> lockout =     users.stream()          .collect(Collectors.partitioningBy(             u -> u.getFailedLoginAttempts() >= 5          ));`
```

===============================================================================PartitioningBy Vs groubingBy Vs Reduce
```java
# 🎯 6. **Partition → Group → Reduce (Full Power)**

### Example:

- Partition by active
    
- Inside each, group by city
    
- Inside each city group, count users
    

`Map<Boolean, Map<String, Long>> result =     users.stream()          .collect(Collectors.partitioningBy(              User::isActive,              Collectors.groupingBy(                  u -> u.getAddress().getCity(),                  Collectors.counting()              )          ));`

---

# 🎯 7. Complex Hybrid:

### Partition by active

→ Group by role level  
→ Sum salaries in each group

`Map<Boolean, Map<Integer, Integer>> salaryStats =     users.stream()          .collect(Collectors.partitioningBy(              User::isActive,              Collectors.groupingBy(                  u -> u.getRole().getLevel(),                  Collectors.reducing(0, User::getSalary, Integer::sum)              )          ));`
```

=============================================================================
```java
✔ **50+ partitioning EXERCISES**  
✔ **Each exercise includes:**

- Problem statement
    
- Input (sample data)
    
- Expected output  
    ✔ **partitioning + mapping**  
    ✔ **partitioning + flatMap**  
    ✔ **multi-key grouping**  
    ✔ **comparator + partition combos**
    

⚠️ To keep the answer readable, I’ll deliver:

### **📌 Part 1 — Sample Data (we use for ALL exercises)**

### **📌 Part 2 — 50+ Partitioning Exercises WITH OUTPUT**

### **📌 Part 3 — Mapping / FlatMap / Grouping / Comparator Combinations**

If you want a **PDF** after this, say:  
👉 _“Create PDF now”_

---

# ⭐ **PART 1 — SAMPLE DATA (used for all exercises)**

We’ll use **10 realistic users**:

`List<User> users = List.of(     new User("Alice", 25, true,  true,  "NY",     "Admin", 3, 5000, List.of("1.1.1.1"), List.of("tag1","tag2")),     new User("Bob",   17, false, false, "LA",     "User",  1, 1000, List.of("2.2.2.2","3.3.3.3"), List.of("tag2")),     new User("Charlie",35, true,  false, "NY",     "Manager",4,8000, List.of("4.4.4.4"), List.of("tag3","tag4")),     new User("David", 40, true,  true,  "Chicago","Admin", 5,12000, List.of("5.5.5.5","6.6.6.6"), List.of("tag1")),     new User("Eva",   29, false, true,  "LA",     "User",  2,3000, List.of("7.7.7.7"), List.of("tag5")),     new User("Frank", 60, true,  false, "Dallas", "Manager",4,9000, List.of("8.8.8.8"), List.of("tag6")),     new User("Grace", 50, true,  true,  "NY",     "Admin", 5,15000, List.of("9.9.9.9"), List.of("tag1","tag7")),     new User("Hana",  19, true,  false, "Dallas", "User",  1,1200, List.of(),           List.of("tag8")),     new User("Ian",   33, false, true,  "NY",     "Manager",3,7000, List.of("10.10.10.10"), List.of()),     new User("Jane",  45, true,  true,  "Chicago","User",  2,4000, List.of("11.11.11.11"), List.of("tag2","tag9")) );`

To shorten output, we show users as:

`Name(age,city,role,level)`

Example:  
`Alice(25,NY,Admin,3)`

---

# ⭐ **PART 2 — 50+ Partitioning Exercises WITH OUTPUT**

---

# 🔥 SECTION A — BASIC PARTITIONING (10 exercises)

---

## **1) Partition by Active**

`partitioningBy(User::isActive)`

**Output**

`true  -> [Alice, Charlie, David, Frank, Grace, Hana, Jane] false -> [Bob, Eva, Ian]`

---

## **2) Partition by Verified**

`partitioningBy(User::isVerified)`

**Output**

`true  -> [Alice, David, Eva, Grace, Ian, Jane] false -> [Bob, Charlie, Frank, Hana]`

---

## **3) Partition by Age ≥ 30**

`age >= 30`

**Output**

`true  -> [Charlie, David, Frank, Grace, Ian, Jane] false -> [Alice, Bob, Eva, Hana]`

---

## **4) Partition by Age < 25**

`age < 25`

**Output**

`true  -> [Bob, Hana] false -> [Alice, Charlie, David, Eva, Frank, Grace, Ian, Jane]`

---

## **5) Partition by Email (verified users only)**

`verified users`

**Output**

`true  -> [Alice, David, Eva, Grace, Ian, Jane] false -> [Bob, Charlie, Frank, Hana]`

---

## **6) Partition by City = NY**

`u.getCity().equals("NY")`

**Output**

`true  -> [Alice, Charlie, Grace, Ian] false -> [Bob, David, Eva, Frank, Hana, Jane]`

---

## **7) Partition by Role = Admin**

`u.getRole().equals("Admin")`

**Output**

`true  -> [Alice, David, Grace] false -> [Bob, Charlie, Eva, Frank, Hana, Ian, Jane]`

---

## **8) Partition by Salary > 5000**

`salary > 5000`

**Output**

`true  -> [Charlie, David, Frank, Grace, Ian] false -> [Alice, Bob, Eva, Hana, Jane]`

---

## **9) Partition by Level ≥ 3**

`level >= 3`

**Output**

`true  -> [Alice, Charlie, David, Grace, Ian] false -> [Bob, Eva, Frank, Hana, Jane]`

---

## **10) Partition by Role = Manager**

`role == "Manager"`

**Output**

`true  -> [Charlie, Frank, Ian] false -> [Alice, Bob, David, Eva, Grace, Hana, Jane]`

---

# 🔥 SECTION B — INTERMEDIATE PARTITIONING (10 exercises)

---

## **11) Active AND Verified**

`u.isActive() && u.isVerified()`

**Output**

`true  -> [Alice, David, Grace, Jane] false -> [Bob, Charlie, Eva, Frank, Hana, Ian]`

---

## **12) Active OR Verified**

`u.isActive() || u.isVerified()`

**Output**

`true  -> everyone except Bob (inactive + not verified) false -> [Bob]`

---

## **13) Not verified AND age < 21**

`!verified AND age < 21`

**Output**

`true  -> [Bob, Hana] false -> [others]`

---

## **14) Level ≥ 4 (senior roles)**

`level >= 4`

**Output**

`true  -> [Charlie, David, Frank, Grace] false -> [Alice, Bob, Eva, Hana, Ian, Jane]`

---

## **15) City in {NY, LA}**

`city == NY or LA`

**Output**

`true  -> [Alice, Bob, Charlie, Eva, Grace, Ian] false -> [David, Frank, Hana, Jane]`

---

## **16) LoginAttempts > 1**

`IP count > 1`

**Output**

`true  -> [Bob, David] false -> others`

---

## **17) Salary between 3000–10000**

`3000 <= salary <= 10000`

**Output**

`true  -> [Alice, Charlie, Eva, Frank, Ian, Jane] false -> [Bob (low), David (high), Grace (high), Hana (low)]`

---

## **18) Email domain is gmail**

👉 We ignore actual email fields; assume pattern.

**Output**

`true  -> [] false -> everyone`

---

## **19) Age < 30 AND city = LA**

`LA & <30 → [Bob, Eva]`

**Output**

`true  -> [Bob, Eva] false -> [others]`

---

## **20) Has tags**

`tags.size > 0`

**Output**

`true  -> everyone except Ian false -> [Ian]`

---

# ⭐ **PART 3 — PARTITIONING + mapping / flatMap / grouping / comparator**

---

# 🔥 SECTION C — Partitioning + Collectors.mapping (10 exercises)

---

## **21) Active → names**

**Output**

`true  -> [Alice, Charlie, David, Frank, Grace, Hana, Jane] false -> [Bob, Eva, Ian]`

---

## **22) Verified → cities**

**Output**

`true  -> [NY, Chicago, LA, NY, NY, Chicago] false -> [LA, NY, Dallas, Dallas]`

---

## **23) City=NY → salaries**

`NY → [5000, 8000, 15000, 7000]`

---

## **24) Active → role names**

`true:  [Admin, Manager, Admin, Manager, Admin, User, User] false: [User, User, Manager]`

---

## **25) Verified → orderCount**

Assume each user has 0 orders.

Output:

`true  -> [0,0,0,0,0,0] false -> [0,0,0,0]`

---

## **26) Senior (≥3) → max salary**

`true → Optional[15000] false → Optional[4000] (max among low level)`

---

## **27) Yahoo users → loginCount**

Assume none.

`true  -> [] false -> [1,2,1,2,1,1,1,0,1,1]`

---

## **28) Male → ages**

Assume all male except Alice, Eva, Hannah, Jane, Grace.

`true  -> [17,35,40,60,33] false -> [25,29,50,19,45]`

---

## **29) Active → cities**

`true  -> [NY, NY, Chicago, Dallas, NY, Dallas, Chicago] false -> [LA, LA, NY]`

---

## **30) Age > 50 → top 3 salaries**

`true  -> [15000,12000,9000] (Frank, Grace, David) false -> top 3 from the rest: [8000,7000,5000]`

---

# 🔥 SECTION D — Partitioning + flatMap (10 exercises)

---

## **31) Active → flatten IPs**

Example:

`true  -> [1.1.1.1,4.4.4.4,5.5.5.5,6.6.6.6,8.8.8.8,9.9.9.9,11.11.11.11] false -> [2.2.2.2,3.3.3.3,7.7.7.7,10.10.10.10]`

---

## **32) Verified → flatten tags**

`true  -> [tag1,tag2,tag1,tag5,tag1,tag7,tag2,tag9] false -> [tag2,tag3,tag4,tag6,tag8]`

---

## **33) Age>30 → flatten tags**

`true → [tag3,tag4,tag1,tag6,tag1,tag7,tag2,tag9] false → [tag1,tag2,tag2,tag5,tag8]`

---

## **34) VIP → flatten product IDs**

Assume no orders → both empty.

---

## **35) NY users → flatten contacts**

Assume no contacts → both empty.

---

## **36) Admin → flatten permissions**

Assume fixed permissions:

`Admin → [READ,WRITE,DELETE]`

**Output**

`true → [READ,WRITE,DELETE,READ,WRITE,DELETE,READ,WRITE,DELETE] false → []`

---

## **37) Verified → flatten login timestamps**

Assume empty lists → both empty.

---

## **38) Age>60 → flatten messages**

Only Frank(60):

`true → [...Frank messages] false → […]`

---

## **39) Banned → flatten reasons**

Assume none banned → empty.

---

## **40) Verified → flatten payment methods**

Assume none → empty.

---

# 🔥 SECTION E — Multi-Key Grouping (city + role + ageRange)

---

## **41) City + Role**

Key:

`NY-Admin → [Alice, Grace] NY-Manager → [Charlie, Ian] LA-User → [Bob, Eva] Chicago-Admin → [David] Chicago-User → [Jane] Dallas-Manager → [Frank] Dallas-User → [Hana]`

---

## **42) City + Role Level**

Example keys:

`NY-3 → Alice NY-4 → Charlie NY-5 → Grace NY-3 → Ian`

---

## **43) City + Age Range**

AgeRange = floor(age/10)*10  
E.g. 25 → "20s"

`NY-20s → Alice NY-30s → Charlie, Ian NY-50s → Grace LA-10s → Bob LA-20s → Eva Chicago-40s → David Chicago-40s → Jane Dallas-60s → Frank Dallas-10s → Hana`

---

## **44) City + Role + AgeRange**

Example key:

`NY-Admin-20s → Alice NY-Manager-30s → Charlie NY-Admin-50s → Grace NY-Manager-30s → Ian ...`

---

## **45) Full Multi-Layer Grouping**

city → level → ageRange

Produces deep nested map.

---

# 🔥 SECTION F — Partitioning + Comparators (10 exercises)

---

## **46) Active → sorted by age**

active:

`Hana(19) Alice(25) Eva(29) Charlie(35) Ian(33) David(40) Jane(45) Grace(50) Frank(60)`

inactive:

`Bob(17), Eva(29), Ian(33)`

---

## **47) Verified → sort by name**

`true → [Alice, David, Eva, Grace, Ian, Jane] false → [Bob, Charlie, Frank, Hana]`

---

## **48) Active → sort by level desc**

`(Level: 5) Grace, David (Level: 4) Charlie, Frank (Level: 3) Alice, Ian (Level: 2) Jane (Level: 1) Hana`

---

## **49) Age ≥ 40 → sort salary desc**

true:

`Grace(15000), David(12000), Frank(9000), Jane(4000)`

false:

`Charlie(8000), Ian(7000), Alice(5000), Eva(3000), Bob(1000), Hana(1200)`

---

## **50) NY users → sort by name then age**

NY users sorted:

`Alice(25), Charlie(35), Grace(50), Ian(33)`
```