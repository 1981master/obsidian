# 2️⃣ JSON — stringify, parse & EVERYTHING AROUND IT

---

## 2.1 What JSON REALLY Is

✔️ **Data format**  
✔️ Text-based  
❌ Not JS object  
❌ No methods

`{   "name": "Ali",   "age": 30 }`

---

## 2.2 JSON.stringify()

### Basic

`JSON.stringify({ a: 1 }); // '{"a":1}'`

---

### Pretty Print

`JSON.stringify(obj, null, 2);`

---

### Filter Properties (replacer)

`JSON.stringify(obj, ["id", "name"]);`

OR function:

`JSON.stringify(obj, (key, value) =>   typeof value === "string" ? value.toUpperCase() : value );`

---

### What stringify REMOVES

`JSON.stringify({   a: undefined,   b: () => {},   c: Symbol("x") }); // "{}"`

❌ Lost data

---

## 2.3 JSON.parse()

`const obj = JSON.parse(jsonString);`

---

### Reviver (Transform while parsing)

`JSON.parse(json, (key, value) => {   if (key === "date") return new Date(value);   return value; });`

---

## 2.4 Dates Problem (VERY COMMON BUG)

`const obj = { date: new Date() };  JSON.stringify(obj); // date becomes string`

Fix on parse:

`new Date(parsed.date)`

---

## 2.5 Circular Reference ❌

`const a = {}; a.self = a;  JSON.stringify(a); // ❌ TypeError: Converting circular structure to JSON`

Solution:

- `structuredClone`
    
- Custom serializer
    
- Libraries
    

---

## 2.6 JSON vs JS Object

|Feature|JS Object|JSON|
|---|---|---|
|Methods|✅|❌|
|Date|✅|❌|
|Map|✅|❌|
|Trailing comma|✅|❌|
|Comments|✅|❌|

---

## 2.7 Backend → Frontend Flow (REAL LIFE)

### Backend (Spring Boot)

`return ResponseEntity.ok(userDTO);`

### Over the wire

`{   "id": 1,   "name": "Ali" }`

### Frontend

`axios.get("/user").then(res => {   console.log(res.data.name); });`

---

## 2.8 NEVER DO THIS ❌

`JSON.parse(response.data)`

Axios already parsed it.

---

## 2.9 When to Use JSON.stringify()

|Case|Why|
|---|---|
|LocalStorage|Only strings|
|Deep clone (simple)|Quick|
|Logging|Readable|
|Sending HTTP|Required|

---

## 2.🔟 JSON Cheat Sheet

`JSON.stringify(obj) JSON.stringify(obj, null, 2) JSON.parse(str) structuredClone(obj)`

---

# 🧠 FINAL RULES YOU SHOULD MEMORIZE

### Deep vs Shallow

- Spread = shallow
    
- JSON trick = deep but limited
    
- structuredClone = best
    

### JSON

- JSON ≠ Object
    
- stringify loses types
    
- parse restores only data
    
- backend already sends parsed JSON