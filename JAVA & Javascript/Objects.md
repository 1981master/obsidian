+------------------+---------------------------+------------------------------+
| Action           | Java                      | JavaScript                   |
+------------------+---------------------------+------------------------------+
| Create Object    | class A {}                | const obj = {};              |
|                  | A o = new A();            |                              |
+------------------+---------------------------+------------------------------+
| Add property     | via fields                | obj.a = 1;                   |
|                  | o.a = 1;                  |                              |
+------------------+---------------------------+------------------------------+
| Get property     | o.a                       | obj.a  / obj['a']            |
+------------------+---------------------------+------------------------------+
| Dynamic keys     | ❌ not typical             | obj[key] = 1;                |
+------------------+---------------------------+------------------------------+
| Get keys         | via Map / reflection      | Object.keys(obj)             |
+------------------+---------------------------+------------------------------+
| Get values       | via Map / reflection      | Object.values(obj)           |
+------------------+---------------------------+------------------------------+
| Get entries      | via Map                   | Object.entries(obj)          |
+------------------+---------------------------+------------------------------+
| Merge objects    | manual / setters          | Object.assign({}, obj1,obj2) |
+------------------+---------------------------+----------------------------
--+
| Clone object     | copy constructor / manual | Object.assign({}, obj)       |
+------------------+---------------------------+------------------------------+
| Freeze object    | ❌ (no direct equivalent)  | Object.freeze(obj)           |
+------------------+---------------------------+------------------------------+

---

+------------------+---------------------+------------------------+------------------------+
| Action           | Java                | JavaScript             | TypeScript             |
+------------------+---------------------+------------------------+------------------------+
| Create Object    | class A {}          | const obj = {};        | type A = {a?: number}; |
|                  | A o = new A();      |                        | const obj: A = {};     |
+------------------+---------------------+------------------------+------------------------+
| Add property     | o.a = 1;            | obj.a = 1;             | obj.a = 1;             |
+------------------+---------------------+------------------------+------------------------+
| Get property     | o.a                 | obj.a / obj['a']       | obj.a / obj['a']       |
+------------------+---------------------+------------------------+------------------------+
| Dynamic keys     | not typical         | obj[key] = 1;          | {[k:string]:number}    |
+------------------+---------------------+------------------------+------------------------+
| Get keys         | Map/reflection      | Object.keys(obj)       | Object.keys(obj)       |
+------------------+---------------------+------------------------+------------------------+
| Get values       | Map/reflection      | Object.values(obj)     | Object.values(obj)     |
+------------------+---------------------+------------------------+------------------------+
| Get entries      | Map                 | Object.entries(obj)    | Object.entries(obj)    |
+------------------+---------------------+------------------------+------------------------+
| Merge objects    | manual              | Object.assign(...)     | {...obj1, ...obj2}     |
+------------------+---------------------+------------------------+------------------------+
| Clone object     | manual              | Object.assign({},obj)  | {...obj}               |
+------------------+---------------------+------------------------+------------------------+
| Freeze object    | none                | Object.freeze(obj)     | Object.freeze(obj)     |
+------------------+---------------------+------------------------+------------------------+

---
### 🔥 Key differences (this is the important part)

#### 1. Java object = fixed structure

In **Java**:

class Person {  
    String name;  
}

- Fields are **defined ahead of time**
- You _can’t randomly add new properties_ at runtime (normally)

---

#### 2. JavaScript object = dynamic dictionary

In **JavaScript**:

```javascript
const obj = {};  
obj.name = "John";  
obj.age = 25; // added later
```

- Objects behave like **maps/dictionaries**
- Keys can be added/removed anytime

---

### 🔑 About `Object.*` (your main question)

JavaScript has a built-in global **`Object` utility**:

```javascript
const obj = { a: 1, b: 2 };  
  
Object.keys(obj);    // ['a','b']  
Object.values(obj);  // [1,2]  
Object.entries(obj); // [['a',1],['b',2]]  
  
Object.assign({}, obj); // clone  
Object.freeze(obj);     // make immutable
```

👉 This is something Java **does NOT have directly** for normal objects.

In Java:

- You use **classes + fields**
- Or switch to a **Map** if you want dynamic key/value behavior

---

### 💡 Mental model

- Java object → like a **blueprint instance (strict, typed)**
- JavaScript object → like a **flexible Hashmap**

---

### 🚨 Important interview-style takeaway

If you try to use a Java object like a JS object:

```java
o.newField = 10; // ❌ not allowed

Closest equivalent in Java:

Map<String, Object> obj = new HashMap<>();  
obj.put("a", 1);
```

---

If you want, I can show a **“JS Object vs JS Map vs Java Map”** comparison—that’s where people usually get tripped up.

## Iterate throw Objects
+------------------+--------------------------+-----------------------------+-----------------------------+
| Action           | Java                     | JavaScript                  | TypeScript                  |
+------------------+--------------------------+-----------------------------+-----------------------------+
| Setup            | Map<String,Integer> m    | const obj = {a:1,b:2};      | const obj: {[k:string]:number}={a:1,b:2}; |
|                  | = Map.of("a",1,"b",2);   |                             |                             |
+------------------+--------------------------+-----------------------------+-----------------------------+
| Keys loop        | for(String k: m.keySet())| for(const k in obj)         | for(const k in obj)         |
|                  |                          |                             |                             |
+------------------+--------------------------+-----------------------------+-----------------------------+
| Values loop      | for(int v: m.values())   | Object.values(obj).forEach  | Object.values(obj).forEach  |
|                  |                          | (v => ...)                  | (v => ...)                  |
+------------------+--------------------------+-----------------------------+-----------------------------+
| Entries loop     | for(var e: m.entrySet()) | Object.entries(obj)         | Object.entries(obj)         |
|                  | k=e.getKey(),v=e.getVal()| .forEach(([k,v]) => ...)    | .forEach(([k,v]) => ...)    |
+------------------+--------------------------+-----------------------------+-----------------------------+
| Classic loop     | for(var e: m.entrySet()) | for(const [k,v] of          | for(const [k,v] of          |
|                  |                          | Object.entries(obj))        | Object.entries(obj))        |
+------------------+--------------------------+-----------------------------+-----------------------------+

**+----------------------+---------------------------+-----------------------------+-----------------------------+
| Case                 | Java                      | JavaScript                  | TypeScript                  |
+----------------------+---------------------------+-----------------------------+-----------------------------+
| Create              | Map<String,Object> m       | const obj = {a:1};          | let obj:{[k:string]:any}    |
|                     | = new HashMap<>();         |                             | = {a:1};                    |
+----------------------+---------------------------+-----------------------------+-----------------------------+
| Add property        | m.put("b",2);              | obj.b = 2;                  | obj.b = 2;                  |
| (dynamic key)       | m.put(key,3);              | obj[key] = 3;               | obj[key] = 3;               |
+----------------------+---------------------------+-----------------------------+-----------------------------+
| Merge objects       | Map<String,Object> m2      | const merged =              | const merged =              |
|                     | = new HashMap<>(m);        | {...obj, c:3};              | {...obj, c:3};              |
|                     | m2.put("c",3);             |                             |                             |
+----------------------+---------------------------+-----------------------------+-----------------------------+
| Clone               | Map<String,Object> copy    | const copy = {...obj};      | const copy = {...obj};      |
|                     | = new HashMap<>(m);        |                             |                             |
+----------------------+---------------------------+-----------------------------+-----------------------------+
| Iterate             | for(var e: m.entrySet()){  | for(const [k,v] of          | for(const [k,v] of          |
|                     |  k=e.getKey();v=e.getVal();| Object.entries(obj)){...}   | Object.entries(obj)){...}   |
|                     | }                         |                             |                             |
+----------------------+---------------------------+-----------------------------+-----------------------------+**
<mark>More clear way</mark>
+----------------------+-----------------------------+-----------------------------+-----------------------------+
| Case                 | Java                        | JavaScript                  | TypeScript                  |
+----------------------+-----------------------------+-----------------------------+-----------------------------+
| 1. Fixed structure   | class A { int a; }          | const obj = { a: 1 };       | type A = { a: number };     |
| (closest to Java)    | A o = new A();              | obj.a = 2;                  | const obj:A={a:1}; obj.a=2; |
+----------------------+-----------------------------+-----------------------------+-----------------------------+
| 2. Add known field   | o.a = 3;                    | obj.a = 3;                  | obj.a = 3;                  |
+----------------------+-----------------------------+-----------------------------+-----------------------------+
| 3. Map (dynamic)     | Map<String,Integer> m       | const obj = {};             | let obj:{[k:string]:number} |
|                      | = new HashMap<>();          |                             | = {};                       |
|                      | m.put("a",1);               | obj["a"] = 1;               | obj["a"] = 1;               |
+----------------------+-----------------------------+-----------------------------+-----------------------------+
| 4. Dynamic key var   | String k="b";               | const k="b";                | const k="b";                |
|                      | m.put(k,2);                 | obj[k] = 2;                 | obj[k] = 2;                 |
+----------------------+-----------------------------+-----------------------------+-----------------------------+
| 5. Computed create   | Map<String,Integer> m2      | const k="c";                | const k="c";                |
|                      | = Map.of("c",3);            | const obj = {[k]:3};        | const obj = {[k]:3};        |
+----------------------+-----------------------------+-----------------------------+-----------------------------+
| 6. Merge / add       | m.putAll(Map.of("d",4));    | Object.assign(obj,{d:4});   | {...obj, d:4}               |
+----------------------+-----------------------------+-----------------------------+-----------------------------+
| 7. Dynamic merge     | Map<String,Integer> m3      | Object.assign(obj,{[k]:5}); | {...obj, [k]:5}             |
|                      | = new HashMap<>(m);         |                             |                             |
|                      | m3.put(k,5);                |                             |                             |
+----------------------+-----------------------------+-----------------------------+-----------------------------+

---
const newObj = { ...obj, [k]: 5 };

Here’s what’s happening:

- `...obj` spreads all existing properties of `obj` into a new object.
- `[k]: 5` uses a **computed property name**, meaning the value of the variable `k` becomes the key.
- If `k` already exists in `obj`, its value will be overwritten with `5`.

### Example
### Add prop c example
const obj = { a: 1, b: 2 };  
const k = "c";  
  
const newObj = { ...obj, [k]: 5 };  
  
console.log(newObj);  
// { a: 1, b: 2, c: 5 }

### Overwriting example

const obj = { a: 1, b: 2 };  
const k = "a";  
  
const newObj = { ...obj, [k]: 5 };  
  
console.log(newObj);  
// { a: 5, b: 2 }

### Important note

This **does not mutate** the original `obj`—it creates a new object. If you actually wanted to mutate:

obj[k] = 5;

Both approaches are valid; the spread version is preferred in immutable patterns (like in React state updates).
---
## 🧠 Key idea

### Java (Map)

map.put("a", 1);

👉 explicit “put method”

---

### JavaScript / TypeScript (Object)

obj["a"] = 1;  
obj.a = 1;

👉 assignment _is the “put”_

---

## 🔑 So your statement is mostly right, but precise version is:

- ❌ JS/TS don’t have `put()` or `add()` for objects
- ✅ Instead, they use **property assignment syntax**

---

## Side-by-side mental mapping

Java Map                 JS/TS Object  
----------------------------------------  
put(k, v)        →      one put(obj[k] = v), multiple put(Object.assign(obj, { a: 1, b: 2 });)  
get(k)           →      obj[k]  
containsKey(k)   →      k in obj  
remove(k)        →      delete obj[k]
## ⚠️ Important difference

### `obj[k] = v` → single operation

- like `map.put(k, v)`

### `Object.assign(obj, source)` → batch update

- like multiple `put()` calls
---

## ⚠️ Important nuance

### `add()` DOES exist in JS/TS—but NOT for objects

It exists for other structures:

### 1. Set

const s = new Set();  
s.add(1);

### 2. Array

const arr = [];  
arr.push(1);

👉 So:

- Objects → use `obj[key] = value`
- Sets → use `add()`
- Arrays → use `push()`
## 🔁 Spread operator (related concept)

const newObj = { ...obj, a: 1 };

Equivalent idea:

Map<String,Integer> copy = new HashMap<>(map);  
copy.put("a", 1);

👉 Key difference:

- `Object.assign` → modifies existing object
- `{...obj}` → creates new object
## 🧠 Simple mental model

|JS/TS|Java equivalent|
|---|---|
|obj[k] = v|map.put(k, v)|
|Object.assign(obj, {...})|multiple map.put(...)|
|{...obj, a:1}|copy + put|

---

## 🧠 Simple way to remember

- Java: **verb methods (`put`, `get`)**
- JS/TS objects: **assignment (`=` style`)**

---

## 🔥 One-line summary

👉 In JS/TS objects, **assignment replaces `put()`**:

obj[key] = value;

---
# 🔁 Equivalent of Java `addAll() Arrays` / `putAll() Maps`

## 1) For Objects (closest to `putAll`)

### Java

map.putAll(otherMap);

### JavaScript / TypeScript

Object.assign(obj, obj2);

👉 Same idea: copy all key-value pairs into `obj`

---

### Alternative (more modern)

const merged = { ...obj1, ...obj2 };

👉 Like:

Map<String,Integer> merged = new HashMap<>(map1);  
merged.putAll(map2);

---

# 🧠 Key difference

| Operation        | Java             | JS/TS                                                                                               |
| ---------------- | ---------------- | --------------------------------------------------------------------------------------------------- |
| add one          | map.put(k,v)     | obj[k] = v, Object.assign(obj, {k: 3}), Object.assign(...object, {k: 3})                            |
| add many         | map.putAll(map2) | Object.assign(obj, obj2), Object.assign(obj, {k: 3, n: 7}), { ...obj1, ...obj2 };//create new objct |
| , add many (new) | new map + putAll | { ...obj1, ...obj2 }                                                                                |

---

# ⚠️ Important subtlety

## Object.assign → modifies original

Object.assign(obj1, obj2);

👉 obj1 is changed

---

## Spread `{...}` → creates new object

const merged = { ...obj1, ...obj2 };

👉 obj1 and obj2 unchanged

---

# 📌 For completeness (other structures)

## Arrays → `addAll` equivalent

### Java

list1.addAll(list2);

### JavaScript

list1.push(...list2);

or:

list1 = list1.concat(list2);

---

## Sets → real `addAll` exists via spread

const s1 = new Set([1,2]);  
const s2 = new Set([3,4]);  
  
const merged = new Set([...s1, ...s2]);

---

# 🔥 Final mental model

Java Map:  
  put(k,v)      → single insert  
  putAll(map2)  → batch insert  
  
JS Object:  
  obj[k]=v                  → single insert  
  Object.assign(obj,obj2)   → batch insert (mutates)  
  {...obj1,...obj2}         → batch insert (new object)