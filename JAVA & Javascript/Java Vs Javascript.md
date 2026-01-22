# **Java vs JavaScript Cheat Sheet**

---

## **1️⃣ Objects / Maps**

|Concept|JavaScript|Java|
|---|---|---|
|Object / Map|`{ a:1, b:2 }`|`Map<String,Integer> map = new HashMap<>()`|
|Add element|`obj.c = 3`|`map.put("c", 3)`|
|Get element|`obj.a` or `obj["a"]`|`map.get("a")`|
|Check existence|`'a' in obj` or `obj.hasOwnProperty('a')`|`map.containsKey("a")`|
|Delete element|`delete obj.a`|`map.remove("a")`|
|Size|`Object.keys(obj).length`|`map.size()`|

---

## **2️⃣ Array of entries / 2D array**

|Concept|JavaScript|Java|
|---|---|---|
|Object → array of entries|`Object.entries(obj)` → `[ [key,value], ... ]`|`map.entrySet().stream()` or `new Object[][] { {"a",1}, {"b",2} }`|
|Array of arrays → Object / Map|`Object.fromEntries(arr)`|`Arrays.stream(arr).collect(Collectors.toMap(...))`|
|Access element|`arr[0][0] // key, arr[0][1] // value`|`arr[0][0] // key, arr[0][1] // value`|
|List of entries|`map([ [k,v] ])`|`List<AbstractMap.SimpleEntry<String,Integer>>`|

---

## **3️⃣ Looping / Iteration**

|Type|JS|Java|
|---|---|---|
|Old-school for|`for(let i=0;i<arr.length;i++)`|`for(int i=0;i<arr.length;i++)`|
|For-of / enhanced for|`for(const [k,v] of Object.entries(obj))`|`for(Map.Entry<String,Integer> entry : map.entrySet())`|
|For-in / keys|`for(let k in obj)`|`for(String k : map.keySet())`|
|forEach|`Object.entries(obj).forEach(([k,v]) => {...})`|`map.forEach((k,v) -> {...})`|
|map / transform|`Object.entries(obj).map(([k,v]) => ...)` → new array|`map.entrySet().stream().map(entry -> ...).collect(Collectors.toList())`|
|filter / subset|`Object.entries(obj).filter(([k,v]) => v>1)` → new array|`map.entrySet().stream().filter(entry -> entry.getValue()>1).collect(Collectors.toMap(Map.Entry::getKey,Map.Entry::getValue))`|

---

## **4️⃣ Access & Destructuring**

|Concept|JS|Java|
|---|---|---|
|Destructure entry|`[key,value] of Object.entries(obj)`|`Map.Entry<K,V> entry` → `entry.getKey(), entry.getValue()`|
|Access key|`key` or `entry[0]`|`entry.getKey()`|
|Access value|`value` or `entry[1]`|`entry.getValue()`|

---

## **5️⃣ Map / Filter / Reduce**

|Method|JS|Java|
|---|---|---|
|Map / transform|`.map(([k,v]) => v*2)` → new array|`.stream().map(entry -> entry.getValue()*2).collect(Collectors.toList())`|
|Filter / select|`.filter(([k,v]) => v>1)`|`.stream().filter(entry -> entry.getValue()>1).collect(Collectors.toMap(...))`|
|Reduce / combine|`.reduce((acc,[k,v])=>acc+v,0)`|`.stream().map(Map.Entry::getValue).reduce(0,Integer::sum)`|

---

## **6️⃣ Notes for Java Devs moving to JS**

1. **No strict typing** → `obj.a = "string"` is fine.
    
2. **`==` vs `===`** → JS has weak equality (`==`) vs strict equality (`===`).
    
3. **Array methods** always return a new array (`map`, `filter`), but `forEach` does **not**.
    
4. **Destructuring**: `[key,value]` for arrays of arrays or entries is like Java’s `Map.Entry`.
    
5. **Objects are unordered**, Maps (`Map`) are ordered by insertion in JS.
    
6. **Converting between object and array of entries**:
    
    - `Object.entries(obj)` → array of arrays
        
    - `Object.fromEntries(array)` → object
        
7. In Java, you must **call getters** (`getKey()`, `getValue()`) when iterating `Map.Entry`.
    

---

## **7️⃣ Conversion Summary**

| Action                     | JS                                                | Java                                                                                    |
| -------------------------- | ------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Object → array of entries  | `Object.entries(obj)`                             | `map.entrySet().stream().toList()`                                                      |
| Array of entries → Object  | `Object.fromEntries(arr)`                         | `Arrays.stream(arr).collect(Collectors.toMap(...))`                                     |
| Transform while converting | `Object.fromEntries(arr.map(([k,v]) => [k,v*2]))` | `Arrays.stream(arr).collect(Collectors.toMap(e -> (String)e[0], e -> (Integer)e[1]*2))` |

## **1️⃣ Data Types**

|Concept|Java|JavaScript|Notes|
|---|---|---|---|
|Numbers|`int, double, long`|`Number` (all floats internally)|No integer type in JS, `Number.MAX_SAFE_INTEGER` for large integers|
|Strings|`String`|`String`|Mutable in Java, immutable in JS (strings are immutable in both)|
|Booleans|`boolean`|`Boolean`|JS has truthy/falsy behavior|
|Arrays|`int[]` or `ArrayList<Integer>`|`Array`|JS arrays can hold mixed types, are dynamic|
|Objects|Classes / POJOs|`{ key: value }`|JS objects can be used like maps; prototype-based|
|Null/Undefined|`null`|`null` / `undefined`|Undefined is “unassigned” in JS, null is intentional empty|

---

## **2️⃣ Variables**

|Concept|Java|JavaScript|Notes|
|---|---|---|---|
|Declaration|`int x = 5;`|`let x = 5;` or `const y = 3`|`const` = constant, `let` = block-scoped variable|
|Scope|Class/method/block|`var` (function), `let/const` (block)|`var` is function-scoped, often confusing for Java devs|
|Reassignment|Allowed unless `final`|Allowed unless `const`|JS is more flexible, but can lead to bugs|

---

## **3️⃣ Loops**

|Concept|Java|JavaScript|
|---|---|---|
|For loop|`for(int i=0;i<n;i++)`|`for(let i=0;i<n;i++)`|
|Enhanced for / for-each|`for(String s : list)`|`for (const x of arr)`|
|While|`while(cond)`|`while(cond)`|
|Do-while|`do { } while(cond)`|`do { } while(cond)`|
|Iterating objects/maps|`for(Map.Entry<K,V> e : map.entrySet())`|`for(const [k,v] of Object.entries(obj))`|

---

## **4️⃣ Functions / Methods**

|Concept|Java|JavaScript|Notes|
|---|---|---|---|
|Method declaration|`int sum(int a,int b){ return a+b; }`|`function sum(a,b){ return a+b; }`|JS functions are first-class objects|
|Arrow function|N/A|`(a,b)=>a+b`|Shorter, lexical `this`|
|Anonymous function|`new Runnable(){ public void run(){} }`|`() => {}`|JS is functional by nature|
|Overloading|Allowed|Not natively (JS uses default params or rest `...args`)|Common mistake for Java devs|

---

## **5️⃣ Objects & Classes**

|Concept|Java|JavaScript|
|---|---|---|
|Class|`class Cat { int age; }`|`class Cat { constructor(age){ this.age = age } }`|
|Inheritance|`extends`|`extends` (ES6 classes)|
|Interfaces|`interface`|JS: no native interface; use duck typing or TypeScript|
|Object literals|N/A|`{ name: "John", age: 10 }`|
|Map / HashMap|`Map<K,V>`|`Map` or plain object `{}`|
|EntrySet|`map.entrySet()`|`Object.entries(obj)`|

---

## **6️⃣ Collections**

|Concept|Java|JavaScript|
|---|---|---|
|Array|`int[]` / `ArrayList`|`Array`|
|Map|`HashMap`, `TreeMap`|`Map`, `Object`|
|Set|`HashSet`|`Set`|
|Stream / functional|`stream().map(...).filter(...)`|`array.map(...).filter(...)`|
|Filter / map / reduce|`.stream().filter(...).map(...).collect(...)`|`.filter(...).map(...).reduce(...)`|

---

## **7️⃣ Equality / Comparison**

|Concept|Java|JavaScript|Notes|
|---|---|---|---|
|Primitive equality|`==`|`==` / `===`|JS `==` is type coercion, `===` strict|
|Object equality|`.equals()`|`===` or custom comparison|JS compares object references|
|Null checks|`obj != null`|`obj != null` or `obj !== undefined`|JS has `undefined` and `null`|

---

## **8️⃣ Error Handling**

|Concept|Java|JavaScript|
|---|---|---|
|Try/catch|`try { } catch(Exception e) {}`|`try { } catch(e) {}`|
|Throwing errors|`throw new RuntimeException("msg")`|`throw new Error("msg")`|
|Checked exceptions|Yes|No (all runtime)|

---

## **9️⃣ Modules / Imports**

|Concept|Java|JavaScript|
|---|---|---|
|Import class|`import java.util.List;`|`import React from 'react'`|
|Export|N/A|`export default` / `export const`|
|Package|`package com.app;`|folder structure + modules|

---

## **10️⃣ Null / Optional Chaining**

|Concept|Java|JavaScript|
|---|---|---|
|Optional|`Optional<String> opt`|`obj?.key`|
|Safe access|`if(obj!=null)`|`obj?.property`|

---

## **11️⃣ Misc / Common Gotchas for Java Devs**

- JavaScript is **loosely typed** → variables can change type
    
- Functions are **first-class objects** → can be passed around
    
- No method overloading → use default params or rest `...args`
    
- Arrays are **dynamic**
    
- Object keys are **always strings** (unless using `Map`)
    
- Equality: always prefer `===` over `==`
    
- `forEach` does **not return a new array**, use `map` for transformation