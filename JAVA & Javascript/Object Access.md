# 1️⃣ JavaScript OBJECT — ALL ACCESS METHODS

## 1.1 Basic object definition

`const user = {   id: 1,   name: "Ali",   active: true };`

### ✅ Access methods

#### 1️⃣ Dot notation (MOST COMMON)

`user.name        // "Ali" user.active      // true`

⚠️ **Rules**

- Key must be a valid identifier
    
- Cannot be dynamic
    

❌ Invalid

`user."name" user.user-name`

---

#### 2️⃣ Bracket notation (MOST FLEXIBLE)

`user["name"]     // "Ali" user["active"]  // true`

✅ **Required when**

- Key has spaces/symbols
    
- Key is dynamic
    

`const key = "name"; user[key];       // "Ali"`

---

### 1.2 Keys that are NOT valid identifiers

`const obj = {   "first-name": "Ali",   "home address": "NY",   1: "one" };  obj["first-name"] obj["home address"] obj[1] obj["1"]`

🚫 Dot notation will NOT work here.

---

## 1.3 Accessing NON-EXISTING keys

`user.age        // undefined user["age"]     // undefined`

✅ Safe (no exception)

---

## 1.4 Optional Chaining (`?.`) – SAFE ACCESS

`user.address?.city`

If `address` is `undefined` or `null`, result is `undefined`, not error.

### With bracket notation

`user.address?.["city"]`

---

## 1.5 Object Destructuring (READ ACCESS)

`const { name, active } = user;`

### Rename while destructuring

`const { name: userName } = user;`

### Default values

`const { age = 18 } = user;`

---

# 2️⃣ OBJECT INSIDE OBJECT (NESTED OBJECT)

`const user = {   id: 1,   profile: {     email: "a@test.com",     address: {       city: "NY"     }   } };`

### Access

`user.profile.email user.profile.address.city`

### Safe access

`user.profile?.address?.city`

---

# 3️⃣ OBJECT INSIDE ARRAY

`const users = [   { id: 1, name: "Ali" },   { id: 2, name: "Sara" } ];`

### Access

`users[0].name users[1]["name"]`

### Loop access

`users.forEach(u => console.log(u.name));`

---

# 4️⃣ ARRAY INSIDE OBJECT

`const data = {   tags: ["js", "java", "react"] };`

### Access

`data.tags[0]        // "js" data["tags"][1]    // "java"`

---

# 5️⃣ OBJECT → ARRAY → OBJECT (MIXED)

`const store = {   customers: [     {       id: 1,       orders: [         { total: 50 },         { total: 75 }       ]     }   ] };`

### Access

`store.customers[0].orders[1].total`

### Safe access

`store.customers?.[0]?.orders?.[1]?.total`

---

# 6️⃣ DYNAMIC ACCESS (VERY IMPORTANT)

`const obj = {   a: 10,   b: 20 };  const key = "a";  obj[key]     // 10`

⚠️ Dot notation **cannot** do this.

---

# 7️⃣ OBJECT KEYS / VALUES / ENTRIES ACCESS

`const obj = { a: 1, b: 2 };`

### Keys

`Object.keys(obj)        // ["a", "b"]`

### Values

`Object.values(obj)     // [1, 2]`

### Entries (ARRAY OF ARRAY)

`Object.entries(obj)    // [["a",1], ["b",2]]`

---

# 8️⃣ `Object.fromEntries()` (YOUR CONFUSION AREA)

`const entries = [   ["a", 1],   ["b", 2] ];  Object.fromEntries(entries); // { a: 1, b: 2 }`

❗ **Why `{}` does NOT work**

`Object.fromEntries({ a: 1 }); // ❌ because fromEntries expects ITERABLE of [key,value]`

💡 JavaScript **Map ↔ Object** bridge:

`Object.fromEntries(map) Object.entries(obj)`

---

# 9️⃣ ACCESS USING MAP (OBJECT-LIKE BUT DIFFERENT)

`const map = new Map(); map.set("a", 1);`

### Access

`map.get("a") map.has("a")`

🚫 Dot/bracket does NOT work

`map.a       // undefined map["a"]    // undefined`

---

# 🔟 OBJECT WITH SYMBOL KEYS

`const sym = Symbol("id");  const obj = {   [sym]: 123 };`

### Access

`obj[sym]`

🚫 Not accessible via `Object.keys`

---

# 1️⃣1️⃣ JSON OBJECT ACCESS (Same as Object)

`const json = JSON.parse('{"name":"Ali"}');  json.name json["name"]`

---

# 1️⃣2️⃣ PROTOTYPE ACCESS (ADVANCED)

`obj.toString() obj.__proto__ Object.getPrototypeOf(obj)`

---

# 1️⃣3️⃣ DESTRUCTURING NESTED OBJECTS

`const user = {   profile: {     email: "a@test.com"   } };  const {   profile: { email } } = user;`

---

# 1️⃣4️⃣ SPREAD ACCESS (COPY / MERGE)

`const copy = { ...user };`

Nested is still referenced (shallow copy).

---

# 1️⃣5️⃣ FOR…IN ACCESS

`for (const key in user) {   console.log(key, user[key]); }`

---

# 1️⃣6️⃣ REFLECT API

`Reflect.get(user, "name") Reflect.has(user, "name")`

---

# 1️⃣7️⃣ DEEP ACCESS BY STRING PATH

`const path = "profile.address.city";  path.split(".").reduce((o, k) => o?.[k], user);`

---

# 🔴 SUMMARY MENTAL MODEL

|Structure|Access|
|---|---|
|Object|`obj.key` / `obj["key"]`|
|Array|`arr[index]`|
|Object in Array|`arr[i].key`|
|Array in Object|`obj.key[i]`|
|Deep Mixed|`obj.a[0].b.c`|
|Safe|`?.`|
|Dynamic|`[]`|
|Object ↔ Array|`entries / fromEntries`|
|Map|`get()`|