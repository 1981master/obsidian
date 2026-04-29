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

```javascript
const users = [   { id: 1, name: "Ali" },   { id: 2, name: "Sara" }];
let result = null;
if(users[2]?.id === undefined){
    result = 'Not Exist';
}else {
   result = users[2].id;
}
console.log(result);//Not Exist
users[1].name users[0]["id"]//1 // and make sure key its string when boxing
users[1].name users[0].id//1 when we don't use or like to use string for key. 
```



---

## 1.5 Array inside Object inside Array

```javascript
// ✅ Example 1 (Normal case)
const data1 = [
  {
    orders: [{ total: 50 }, { total: 100 }]
  }
];

console.log(data1[0].orders[1].total); // 100
console.log(data1?.[0]?.orders?.[1]?.total); // 100


// ✅ Example 2 (Missing array index)
const data2 = [
  {
    orders: [{ total: 50 }]
  }
];

// console.log(data2[0].orders[1].total); // ❌ Would throw error
console.log(data2?.[0]?.orders?.[1]?.total); // undefined
❌ **No, this will NOT work.**


### 🚫 Problem: 
console.log(data1[0]['orders'].[1].total); // BAD Remove DOT
2️⃣ 
We cannot put a `.` right after bracket notation.

['orders'].[1] ❌ → **Syntax Error**

## ✅ Correct Ways

### 1️⃣ Dot + Bracket (Valid)
console.log(data1[0].orders[1].total); // 100
OR:
2️⃣ Full Bracket Notation (Also Valid)
console.log(data1[0]['orders'][1]['total']); // 100
###

## 🔥 Rule to Remember

- Use `.` for known property names → `obj.prop`
    
- Use `[]` when:
    
    - Property name is dynamic
        
    - Property has special characters
        
    - Property name is stored in a variable
        

Example:

const key = "orders"; console.log(data1[0][key][1].total);

Code: Using Dynamic access//see key
function fun(key) {
  return data1?.[0]?.[key]?.[1]?.['total'];
}

console.log(fun("orders")); // 100
console.log(fun("wrongKey")); // undefined

function fun(key) {// using just key above is best in performance than this but this valid too.
  return data1?.[0]?.[`${key}`]?.[1]?.['total'];
}

----------------------------------------------------------

// ✅ Example 3 (Missing property)
const data3 = [
  {
    items: [{ price: 20 }]
  }
];

console.log(data3?.[0]?.orders?.[0]?.total); // undefined


// ✅ Example 4 (Empty array)
const data4 = [];

console.log(data4?.[0]?.orders?.[0]?.total); // undefined


// ✅ Bonus: Default value with ??
const total = data4?.[0]?.orders?.[1]?.total ?? "Not Found";
console.log(total); // Not Found

```


---
1️⃣ **Object inside object inside object**
```java
class Address {
    String city;
}

class User {
    int id;
    String name;
    Address address;
}
```
```json
{
  "id": 1,
  "name": "Ali",
  "address": {
    "city": "New York"
  }
}

user {}
 ├── id: 1
 ├── name: "Ali"
 └── address {}
      └── city: "New York"
      
console.log(user.name);           // "Ali"
console.log(user.address.city);   // "New York"

```

2️⃣ **Array inside object inside object**
```java
class User {
    int id;
    String name;
}

class Team {
    String teamName;
    List<User> members;
}

```

```json
{
  "teamName": "Alpha",
  "members": [
    { "id": 1, "name": "Ali" },
    { "id": 2, "name": "Sara" }
  ]
}

team {}
 ├── teamName: "Alpha"
 └── members []       // array
      ├── {}          // member 0
      │    ├── id: 1
      │    └── name: "Ali"
      └── {}          // member 1
           ├── id: 2
           └── name: "Sara"
           
console.log(team.teamName);        // "Alpha"
team.members.forEach(member => {
  console.log(member.name);        // "Ali", then "Sara"
});


```

3️⃣ **Array inside object inside array** (less common, but possible)

```java
class Project {
    String projectName;
    List<User> users;
}

List<Project> projects;
```

```json
projects []      // array
 ├── {}          // project 0
 │    ├── projectName: "P1"
 │    └── users []  // array of objects
 │         ├── {}  // user 0
 │         │    ├── id: 1
 │         │    └── name: "Ali"
 │         └── {}  // user 1
 │              ├── id: 2
 │              └── name: "Sara"
 └── {}          // project 1
      ├── projectName: "P2"
      └── users []
           └── {} // user 0
                ├── id: 3
                └── name: "Maa"
                
[
  {
    "projectName": "P1",
    "users": [
      { "id": 1, "name": "Ali" },
      { "id": 2, "name": "Sara" }
    ]
  },
  {
    "projectName": "P2",
    "users": [
      { "id": 3, "name": "Maa" }
    ]
  }
]
projects.forEach(project => {
  console.log(project.projectName);
  project.users.forEach(user => console.log(user.name));
});
```

### 🔑 Key takeaway

- **Objects `{}` → named properties → access by keys**
- **Arrays `[]` → ordered lists → access by index or loop**
- Nested structures follow the Java types:
    - `POJO` → object
    - `List` → array
---

We access object/s by dot notations and then loop throw array inside object by forEach, map etc: if there is object inside of this array we access it while looping by dot notations and if object has value array we access it again by loop:
### 🔑 Rule of thumb

- Dot notation → object
- Loop → array
- Nest as deep as needed, combine the two

<mark>Array inside object inside array (deep nesting)</mark>

```javascript
const projects = [
  {
    name: "P1",
    users: [
      { id: 1, name: "Ali", hobbies: ["reading","gaming"] },
      { id: 2, name: "Sara", hobbies: ["music"] }
    ]
  }
];

projects.forEach(proj => {
  console.log(proj.name); // "P1"

  proj.users.forEach(user => {
    console.log(user.name); // "Ali", "Sara"
    
    user.hobbies.forEach(hobby => {
      console.log(hobby);  // "reading", "gaming", "music"
    });
  });
});
```

---

## 1.6 Looping / Reading Arrays

### for

`for (let i = 0; i < arr.length; i++) {   arr[i] }`
```javascript

```
### for...of (BEST)

`for (const item of arr) {   console.log(item) }`

### forEach → “do something with each item”

`arr.forEach(item => console.log(item))`
```javascript
forEach here for logging:

const numbers = [1, 2, 3];

numbers.forEach(n => {
  console.log(n * 2); // just performing an action
});
```

1) **Use it when:** you want to **perform side effects** (e.g., logging, modifying DOM, updating variables)
eg: modifying variable use forEach:
```javascript
const numbers = [1, 2, 3, 4, 5];
let sum = 0;

numbers.forEach(num => {
  sum += num; // modifying external variable
});

console.log(sum); // 15
```

✅ Here, `forEach` is perfect because we just **perform actions**, not creating a new array.  
❌ Using `map` would work, but it returns an unused array—less efficient.
eg: forEach for modifying DOM:
- `forEach` → looping over users
- Side effect → **modifying DOM**
- We **don’t need a new array**, so `map` isn’t appropriate
```javascript
<ul id="userList"></ul> 
when we need to display users use forEach:
const users = [
  { id: 1, name: "Ali" },
  { id: 2, name: "Sara" }
];

const ul = document.getElementById("userList");

users.forEach(user => {
  const li = document.createElement("li"); // create element
  li.textContent = user.name;             // set text
  ul.appendChild(li);                     // add to DOM
});

```
✅ Side effect → modifying existing objects  
❌ `map` would create a **new array** unnecessarily if we just want to update existing objects
```javascript
const members = [
  { name: "Ali", active: false },
  { name: "Sara", active: false }
];

members.forEach(member => {
  if (member.name === "Sara") {
    member.active = true; // modify object in place
  }
});

console.log(members);
/* [
  { name: "Ali", active: false },
  { name: "Sara", active: true }
] */
```
2) **Does not return a new array(use map for instead of forEach if need new array)**
3)  Returns `undefined`

### map → “transform each item into a new array”
```javascript
const numbers = [1, 2, 3];
const doubled = numbers.map(n => n * 2);

console.log(doubled); // [2, 4, 6]
```

- **Use it when:** you want to **create a new array** from an existing array
- Returns a **new array** of the same length


## Key distinction

|Feature|forEach|map|
|---|---|---|
|Purpose|Side effects (do something)|Transform array (return new)|
|Return value|`undefined`|New array|
|Use case|Logging, mutating, calling functions|Creating derived array|

### ✅ Rule of thumb

- Just **loop + do something** → `forEach`
- **Generate a new array** → `map`

---

## 1.7 Core Array Methods (READ / TRANSFORM)

### map (transform)

`arr.map(x => x.toUpperCase())`

### filter

`arr.filter(x => x !== "b")`

### find / findIndex

`users.find(u => u.id === 2) users.findIndex(u => u.id === 2)`

### reduce (VERY IMPORTANT)
1️⃣ What this does

```javascript
const arr = ["a", "b", "c"];
const result = arr.reduce((acc, val) => acc + val, "");
console.log(result); // "abc"

//Reducer best for conditional joining/acc
//Eg:
const arr = ["apple", "banana", "cherry"];
const result = arr.reduce((acc, val) => {
  if (val.startsWith("b")) acc.push(val);
  return acc;
}, []);
console.log(result); // ["banana"]

```

- ✅ Works perfectly
    
- ✅ Concatenates all elements into a single string
    
- ✅ Initial value `""` ensures the first element is handled correctly
- 
#### acc(Accumulator) in Reducer can be: 
- a **number**
    
- a **string**
    
- an **array**
    
- an **object**
    
- basically **anything**
```javascript
can be an Array:
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((acc, val) => acc + val, 0);
console.log(sum); // 10

or another Array:
const numbers = [1, 2, 3];
const doubled = numbers.reduce((acc, val) => {
  acc.push(val * 2);
  return acc;
}, []);
console.log(doubled); // [2, 4, 6]
-------------------------------------------------------------------
or Object:
// Example: Using reduce to transform an array into an object
const items = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" }
];

const obj = items.reduce((acc, val) => {
  // For each item in the array, set acc[key] = value
  acc[val.id] = val.name;        // or acc[val['id']] = val['name'];
  //or:
  //acc[val['id']] = val['name'];
  return acc;                    // always return the accumulator
}, {}); // {} is the initial value of acc

console.log(obj); // { 1: "Alice", 2: "Bob" }

// Step-by-step explanation:
// Initial acc: {}
// Iteration 1: val = { id: 1, name: "Alice" } → acc[1] = "Alice" → acc = {1: "Alice"}
// Iteration 2: val = { id: 2, name: "Bob" }   → acc[2] = "Bob"   → acc = {1: "Alice", 2: "Bob"}
// Final result returned by reduce: { 1: "Alice", 2: "Bob" }


```

```javascript
// Example: Using reduce to create an array of values from an array of objects
const items = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" }
];

// Extract all names into an array using reduce
const names = items.reduce((acc, val) => {
  acc.push(val.name); // add the current name to the accumulator array
  return acc;         // always return the accumulator
}, []);

console.log(names); // ["Alice", "Bob"]

// Bonus: Extract both id and name into nested arrays
const idNamePairs = items.reduce((acc, val) => {
  acc.push([val.id, val.name]);
  return acc;
}, []);

console.log(idNamePairs); // [[1, "Alice"], [2, "Bob"]]

```

```javascript
// Example: Using reduce to get ["Alice", "Bob"] from an array of objects
const items = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" }
];

// Using reduce to extract names
const names = items.reduce((acc, val) => {
  acc.push(val.name); // add each name to the accumulator array
  return acc;         // return accumulator for next iteration
}, []);

console.log(names); // ["Alice", "Bob"]

```

##### convert nested array to object:
```javascript
// Input: nested arrays
const arr = [[1, "Alice"], [2, "Bob"]];

// Convert to array of objects
const objArray = arr.map(([id, name]) => ({ id, name }));

console.log(objArray);
// Output: [{ id: 1, name: "Alice" }, { id: 2, name: "Bob" }]

```

2️⃣ Alternative 1: `join`

```javascript
const arr = ["a", "b", "c"];
const result = arr.join(""); 
console.log(result); // "abc"

```

##### nested array to objec
```javascript
// Input: nested arrays
const arr = [[1, "Alice"], [2, "Bob"]];

// Convert to a single object using the last entry
const obj = { id: arr[arr.length - 1][0], name: arr[arr.length - 1][1] };

console.log(obj); // { id: 2, name: "Bob" }

```

- ✅ Cleaner & simpler
    
- ✅ Reads directly as “combine into a string”
    
- ✅ Slightly more optimized internally than `reduce` for concatenation
    
- ✅ Can easily add a separator, e.g., `arr.join(", ")`

3️⃣ Alternative 2: `for` loop

```javascript
let result = "";
for (const val of arr) {
  result += val;
}

```

- ✅ Works, but more verbose
    
- ✅ Usually not preferred unless you have complex logic per iteration


## ✅ Recommendation

- **Use `join("")`** for concatenating array elements into a string — it’s the simplest, most readable, and efficient.
    
- Use `reduce` if you’re doing **more complex accumulation** (e.g., building an object, summing numbers, conditional concatenation).
---

## 1.8 Mutating Methods (CHANGE ARRAY)

```javascript
arr.push("d") 
arr.pop() 
arr.shift() arr.unshift("z") 
arr.splice(1, 1)
```

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