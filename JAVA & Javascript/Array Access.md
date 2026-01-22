# 1️⃣ ARRAYS — **ALL ACCESS + ALL IMPORTANT METHODS**

## 1.1 What an Array REALLY is in JavaScript

`const arr = ["a", "b", "c"];`

👉 Arrays are **objects with numeric keys**

`{   0: "a",   1: "b",   2: "c",   length: 3 }`

That’s why:

- `arr[0]` works
    
- `arr.length` works
    
- `typeof arr === "object"`
    

---

## 1.2 Accessing Array Elements

### Index access

`arr[0]        // "a" arr[2]        // "c"`

### Last element

`arr[arr.length - 1] arr.at(-1)        // modern & clean ✅`

### Optional chaining

`arr?.[0]`

---

## 1.3 Array inside Array (2D Array – like Java)

`const matrix = [   [1, 2],   [3, 4] ];`

`matrix[0][1]   // 2`

✔️ **Same mental model as Java 2D array**

---

## 1.4 Object inside Array

`const users = [   { id: 1, name: "Ali" },   { id: 2, name: "Sara" } ];`

`users[1].name users[0]["id"]`

---

## 1.5 Array inside Object inside Array

`const data = [   {     orders: [{ total: 50 }, { total: 100 }]   } ];`

`data[0].orders[1].total`

Safe:

`data?.[0]?.orders?.[1]?.total`

---

## 1.6 Looping / Reading Arrays

### for

`for (let i = 0; i < arr.length; i++) {   arr[i] }`

### for...of (BEST)

`for (const item of arr) {   console.log(item) }`

### forEach

`arr.forEach(item => console.log(item))`

---

## 1.7 Core Array Methods (READ / TRANSFORM)

### map (transform)

`arr.map(x => x.toUpperCase())`

### filter

`arr.filter(x => x !== "b")`

### find / findIndex

`users.find(u => u.id === 2) users.findIndex(u => u.id === 2)`

### reduce (VERY IMPORTANT)

`arr.reduce((acc, val) => acc + val, "")`

---

## 1.8 Mutating Methods (CHANGE ARRAY)

`arr.push("d") arr.pop() arr.shift() arr.unshift("z") arr.splice(1, 1)`

⚠️ React warning: **mutation causes bugs**

---

## 1.9 Non-mutating (SAFE)

`arr.slice(0, 2) arr.concat(["x"])`

---

## 1.🔟 Array ↔ Object Conversion

### Array → Object

`Object.fromEntries([   ["a", 1],   ["b", 2] ])`

### Object → Array

`Object.entries({ a: 1 })`

---

# 2️⃣ MAP / SET / WEAKMAP / WEAKSET

## 2.1 Map (KEY → VALUE)

`const map = new Map(); map.set("a", 1); map.set(1, "number");`

### Access

`map.get("a") map.has("a") map.delete("a")`

❌ NOT allowed

`map.a map["a"]`

### Loop

`for (const [k, v] of map) {   console.log(k, v) }`

### Convert

`Object.fromEntries(map) new Map(Object.entries(obj))`

---

## 2.2 Set (UNIQUE VALUES)

`const set = new Set([1, 2, 2, 3]);`

`set.has(2) set.add(4) set.delete(1)`

Convert:

`[...set]`

---

## 2.3 WeakMap (OBJECT KEYS ONLY)

`const wm = new WeakMap(); const obj = {}; wm.set(obj, "data");`

✔️ Garbage-collected  
❌ No loop  
❌ No size

---

## 2.4 WeakSet

`const ws = new WeakSet(); ws.add(obj);`

✔️ Track object existence  
❌ No iteration

---

## 2.5 When to Use What

|Structure|Use case|
|---|---|
|Object|JSON, backend data|
|Map|dynamic keys, frequent add/remove|
|Set|unique values|
|WeakMap|private object metadata|
|Array|ordered list|

---

# 3️⃣ JAVA vs JAVASCRIPT — SIDE-BY-SIDE

## 3.1 Object vs Class

|Java|JavaScript|
|---|---|
|Class-based|Prototype-based|
|`User u = new User()`|`{}` or `class`|
|Fixed fields|Dynamic keys|

---

## 3.2 Array

|Java|JavaScript|
|---|---|
|`int[] arr`|`[]`|
|Fixed size|Dynamic|
|`arr.length`|`arr.length`|
|`arr[0]`|`arr[0]`|

---

## 3.3 Map

|Java|JavaScript|
|---|---|
|`HashMap<K,V>`|`Map`|
|`get(key)`|`get(key)`|
|Strong typing|Dynamic|

---

## 3.4 Object Access

|Java|JavaScript|
|---|---|
|`user.getName()`|`user.name`|
|Encapsulation|Open by default|

---

## 3.5 JSON Handling

|Java|JavaScript|
|---|---|
|Jackson / Gson|Native|
|DTO required|Plain object|
|Typed|Untyped|

---

# 4️⃣ REAL BACKEND → FRONTEND JSON ACCESS PATTERNS

## 4.1 Typical Backend Response (Spring Boot)

`{   "id": 1,   "name": "Ali",   "roles": ["ADMIN", "USER"],   "orders": [     { "id": 10, "total": 50 }   ] }`

---

## 4.2 Frontend Access (React / JS)

`response.data.name response.data.roles[0] response.data.orders[0].total`

Safe:

`response.data?.orders?.[0]?.total`

---

## 4.3 Mapping Backend → UI

`users.map(u => ({   label: u.name,   value: u.id }))`

---

## 4.4 NEVER Do Logic Only in UI

❌ Bad:

`frontend calculates totals frontend filters security rules`

✅ Good:

- Backend: validation, filtering, security
    
- Frontend: rendering only
    

---

## 4.5 Common Bugs (You’ve Hit These)

|Bug|Cause|
|---|---|
|`undefined`|Wrong path|
|CORS|Backend config|
|Empty UI|Async not awaited|
|fromEntries error|Not iterable|

---

# 🧠 FINAL MENTAL MODEL

```text
Object → key
Array  → index 
Map    → get() 
Set    → has() 
JSON   → object + array
```