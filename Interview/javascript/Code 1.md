```javascript
// JavaScript Practice Playground
// You can edit this file directly and practice coding here step by step

/****************************
 * TASK 1
 * Double each number in array
 ****************************/

function doubleArray(arr) {
  if (!Array.isArray(arr)) return [];

  let result = [];
  for (let i of arr) {
    result.push(i * 2);
  }

  return result;
}

function doubleArrayMap(arr) {
  if (!Array.isArray(arr)) return [];

  return arr.map(item => item * 2);
}

/****************************
 * TASK 2
 * Get only even numbers
 ****************************/

function getEvenNumbersLoop(arr) {
  if (!Array.isArray(arr)) return [];

  let result = [];
  for (let i of arr) {
    if (i % 2 === 0) result.push(i);
  }

  return result;
}

function getEvenNumbers(arr) {
  if (!Array.isArray(arr)) return [];

  return arr.filter(item => item % 2 === 0);
}

/****************************
 * TASK 3
 * Sum of array (loop version)
 * Input: [1,2,3,4]
 * Output: 10
 ****************************/

function sumArray(arr) {
  if (!Array.isArray(arr)) return 0;

  let sum = 0;
  for (let i of arr) {
    sum += i;
  }

  return sum;
}

/****************************
 * TASK 4
 * Sum of array (reduce version)
 ****************************/

function sumArrayReduce(arr) {
  if (!Array.isArray(arr)) return 0;

  return arr.reduce((acc, curr) => acc + curr, 0);
}

// Try your functions here:
console.log(sumArray([1,2,3,4]));
console.log(sumArrayReduce([1,2,3,4]));

/****************************
 * TASK 5
 * FIND PRACTICE (fixed)
 ****************************/

const numbers = [3, 7, 10, 15];
const users = [
  { id: 1, name: "Ali" },
  { id: 2, name: "Sara" },
  { id: 3, name: "John" }
];

// 1. first number > 8
const result1 = Array.isArray(numbers)
  ? numbers.find(item => item > 8)
  : undefined;

// 2. user with name "Sara"
const result2 = Array.isArray(users)
  ? users.find(user => user.name === "Sara")
  : undefined;

// 3. first odd number
const result3 = Array.isArray(numbers)
  ? numbers.find(item => item % 2 !== 0)
  : undefined;

console.log("find results:", result1, result2, result3);

/****************************
 * TASK 6
 * UNDEFINED vs NULL HANDLING
 ****************************/

// helper: check if value is null or undefined
function isNil(value) {
  return value === null || value === undefined;
}

// safe find: always returns null instead of undefined
function safeFind(arr, predicate) {
  if (!Array.isArray(arr)) return null;

  const result = arr.find(predicate);
  return result ?? null;
}

// examples
const testNumbers = [1, 2, 3];

const safeResult = safeFind(testNumbers, n => n > 10);
console.log("safeFind result:", safeResult);

console.log("isNil(undefined):", isNil(undefined));
console.log("isNil(null):", isNil(null));


```

---
```javascript
## 🔴 What you wrote:

arr.forEach(item => item * 2)

This does **nothing to the array**.

---

## 🧠 Why?

`forEach()`:

- **does NOT return anything**
- **does NOT create a new array**
- just runs a function for each item

So:

item * 2

is calculated… and then **thrown away**.

---

## 🔥 Important rule

|Method|Returns new array|Modifies original|
|---|---|---|
|`map()`|✅ yes|❌ no|
|`forEach()`|❌ no|❌ (unless you do it manually)|

---

## ⚠️ When does `forEach` change the array?

Only if you explicitly modify it:

arr.forEach((item, index) => {  
  arr[index] = item * 2;  
});

👉 Now the original array **is modified**

---

## 🧠 Mental model

- `map()` → “give me a transformed copy”
- `forEach()` → “just loop, I’ll handle side effects”

---

## 🔥 Best practice

If your goal is:

- transform data → **use `map()`**
- side effects (logging, API calls, etc.) → **use `forEach()`**

```