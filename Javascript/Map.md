##### Nested Object use Flatten
```javascript
const totalSum = customers
  .flatMap(customer => customer.orders)
  .flatMap(order => order.items)
  .reduce((sum, item) => sum + item.total, 0);
  //See below
```

```javascript
/********************************************************************
 MAP() MENTAL MODEL
---------------------------------------------------------------------
map() returns []
nested map() returns nested arrays
number of maps = number of array layers

1 map   -> []
2 maps  -> [[]]
3 maps  -> [[[]]]
N maps  -> N levels of arrays

IMPORTANT:
If you use {} you MUST return.
********************************************************************/


/********************************************************************
EXAMPLE 1 — ONE MAP
********************************************************************/

const oneMap = [1, 2, 3].map(x => x * 2);

console.log("One map:", oneMap);
// [2, 4, 6]
// Structure: []


/********************************************************************
EXAMPLE 2 — TWO MAPS (Nested Arrays)
********************************************************************/

const dataTwo = [
  { numbers: [1, 2] },
  { numbers: [3, 4] }
];

const twoMaps = dataTwo.map(item =>
  item.numbers.map(n => n * 2)
);

console.log("Two maps:", twoMaps);
// [[2, 4], [6, 8]]
// Structure:
// [
//   [],
//   []
// ]


/********************************************************************
EXAMPLE 3 — THREE MAPS (Deep Nested Objects)
********************************************************************/

const dataThree = [
  {
    name: "Store A",
    departments: [
      {
        name: "Electronics",
        products: [
          { price: 100 },
          { price: 200 }
        ]
      }
    ]
  }
];

const threeMaps = dataThree.map(store =>
  store.departments.map(dept =>
    dept.products.map(product => product.price)
  )
);

console.log("Three maps:", threeMaps);
// [[[100, 200]]]
// Structure:
// [
//   [
//     []
//   ]
// ]


/********************************************************************
EXAMPLE 4 — REALISTIC NESTED OBJECT (Orders Example)
********************************************************************/

const ordersData = [
  {
    customer: "John",
    orders: [
      {
        id: 1,
        items: [
          { name: "Phone", total: 500 },
          { name: "Case", total: 50 }
        ]
      }
    ]
  }
];

const nestedTotals = ordersData.map(customer =>
  customer.orders.map(order =>
    order.items.map(item => item.total)
  )
);

console.log("Nested totals:", nestedTotals);
// [[[500, 50]]]


/********************************************************************
HOW TO AVOID DEEP NESTING
********************************************************************/

// Using flatMap (removes ONE level)

const flatTotals = ordersData
  .flatMap(customer => customer.orders)
  .flatMap(order => order.items)
  .map(item => item.total);

console.log("Flattened totals:", flatTotals);
// [500, 50]


/********************************************************************
IMPORTANT RETURN RULE
********************************************************************/

// ❌ WRONG
[1,2,3].map(x => { x * 2 }); // returns [undefined, undefined, undefined]

// ✅ CORRECT
[1,2,3].map(x => { return x * 2 });

// ✅ IMPLICIT RETURN
[1,2,3].map(x => x * 2);


/********************************************************************
FINAL FORMULA
---------------------------------------------------------------------
Each map() creates a new []
Nested map() creates nested arrays
Use flatMap() to remove one level
Use flat() to remove levels manually
********************************************************************/

```

----
```javascript
/********************************************************************
VISUAL TREE DIAGRAM (Nested Object Example)
*********************************************************************

Data Structure:

customers
│
├── customer
│    ├── orders
│    │     ├── order
│    │     │     ├── items
│    │     │     │     ├── item { total: 100 }
│    │     │     │     ├── item { total: 200 }
│    │
Result shape with map():
customers.map(
  orders.map(
    items.map()
  )
)

= [[[100, 200]]]

Each map() = one new []
3 maps = [[[ ]]]


********************************************************************/


/********************************************************************
DATA EXAMPLE (Deeply Nested)
********************************************************************/

const customers = [
  {
    name: "John",
    orders: [
      {
        id: 1,
        items: [
          { name: "Phone", total: 500 },
          { name: "Case", total: 50 }
        ]
      }
    ]
  }
];


/********************************************************************
1️⃣ JAVASCRIPT: map vs flatMap
********************************************************************/

// ❌ Using 3 maps → nested arrays
const nestedTotals = customers.map(customer =>
  customer.orders.map(order =>
    order.items.map(item => item.total)
  )
);

console.log("JS nested result:", nestedTotals);
// [[[500, 50]]]


// ✅ Using flatMap → removes ONE level each time
const flatTotals = customers
  .flatMap(customer => customer.orders)
  .flatMap(order => order.items)
  .map(item => item.total);

console.log("JS flat result:", flatTotals);
// [500, 50]


/********************************************************************
2️⃣ JAVASCRIPT: TOTAL SUM FROM DEEPLY NESTED ARRAY
********************************************************************/

const totalSum = customers
  .flatMap(customer => customer.orders)
  .flatMap(order => order.items)
  .reduce((sum, item) => sum + item.total, 0);

console.log("JS total sum:", totalSum);
// 550


/********************************************************************
3️⃣ JAVA STREAM COMPARISON
********************************************************************/

/*
Java version of same logic:

List<Integer> totals =
    customers.stream()
        .flatMap(c -> c.getOrders().stream())
        .flatMap(o -> o.getItems().stream())
        .map(Item::getTotal)
        .toList();

Integer totalSum =
    customers.stream()
        .flatMap(c -> c.getOrders().stream())
        .flatMap(o -> o.getItems().stream())
        .map(Item::getTotal)
        .reduce(0, Integer::sum);


IMPORTANT DIFFERENCE:

Java:
- map() does NOT create nested List automatically
- Streams are lazy
- Nothing executes until terminal operation (toList, reduce)

JavaScript:
- map() immediately creates REAL arrays
- Nested map() = nested arrays
- Execution is eager
*/


/********************************************************************
MENTAL MODEL SUMMARY
*********************************************************************

JS:
map()      → returns []
flatMap()  → returns [] and removes ONE level
reduce()   → returns single value

N maps = N array levels

Java:
map()      → transforms elements
flatMap()  → flattens streams
Streams are lazy until terminal operation

********************************************************************/

```

---
##### Performance Java Vs JavaScript
```javascript
/********************************************************************
🔥 PERFORMANCE COMPARISON: JAVASCRIPT map/flatMap vs JAVA STREAMS
*********************************************************************/

GOAL:
Compare execution model, memory behavior, laziness, parallelism,
and real-world performance implications.

---------------------------------------------------------------------
1️⃣ EXECUTION MODEL
---------------------------------------------------------------------

JAVASCRIPT (Array.map / flatMap)
--------------------------------
const result = array
  .map(x => x * 2)
  .filter(x => x > 10)
  .map(x => x + 1);

✔ EAGER execution
✔ Each step creates a NEW REAL ARRAY
✔ Memory allocated at each step
✔ Executes immediately

Memory behavior:
Step1 -> new []
Step2 -> new []
Step3 -> new []
Total = multiple intermediate arrays


JAVA STREAMS
------------
List<Integer> result = list.stream()
    .map(x -> x * 2)
    .filter(x -> x > 10)
    .map(x -> x + 1)
    .toList();

✔ LAZY execution
✔ No intermediate collections created
✔ Operations fused together internally
✔ Executes only at terminal operation (.toList())

Memory behavior:
Pipeline built first
Single pass during terminal execution
No intermediate Lists created


---------------------------------------------------------------------
2️⃣ INTERMEDIATE ARRAY CREATION COST
---------------------------------------------------------------------

JS:

const result = bigArray
  .map(f1)    // creates new array (size N)
  .map(f2)    // creates new array (size N)
  .map(f3);   // creates new array (size N)

Time Complexity:
O(N) per step
Total ≈ O(3N)

Memory:
~3N additional storage temporarily

Java Streams:

bigList.stream()
  .map(f1)
  .map(f2)
  .map(f3)
  .toList();

Time Complexity:
O(N) total (single traversal)

Memory:
Only final list allocated


---------------------------------------------------------------------
3️⃣ flatMap COMPARISON
---------------------------------------------------------------------

JS flatMap:

array.flatMap(x => x.items)

✔ Removes ONE level
✔ Still creates new array immediately
✔ Eager execution


Java flatMap:

stream.flatMap(x -> x.getItems().stream())

✔ Flattens lazily
✔ No intermediate collections
✔ Combined in single traversal


---------------------------------------------------------------------
4️⃣ PARALLELISM
---------------------------------------------------------------------

Java Streams:

list.parallelStream()
    .map(...)
    .reduce(...);

✔ Multi-core parallel execution
✔ Automatic workload splitting
✔ Can significantly improve large data performance

JavaScript:

✔ Single-threaded (main thread)
✔ No built-in parallel map
✔ Requires Web Workers for parallelism
✔ More manual work


---------------------------------------------------------------------
5️⃣ REAL-WORLD PERFORMANCE SUMMARY
---------------------------------------------------------------------

Small Data (UI, typical frontend):
JS performance difference = negligible
Readability matters more than micro-optimization

Large Data (millions of elements):
Java Streams are more memory-efficient
Java Streams can parallelize
Java Streams avoid intermediate collection overhead


---------------------------------------------------------------------
6️⃣ PRACTICAL RULES
---------------------------------------------------------------------

Frontend (React / Browser):
✔ Use map freely
✔ Use flatMap when structure requires
✔ Avoid unnecessary deep chaining on huge arrays
✔ For massive datasets -> process on backend

Backend (Java / Spring):
✔ Prefer Stream pipelines
✔ Use parallelStream carefully
✔ Streams are more scalable for large datasets


---------------------------------------------------------------------
7️⃣ BIG CONCEPTUAL DIFFERENCE
---------------------------------------------------------------------

JavaScript:
- Arrays are REAL materialized collections
- map() returns a real array immediately
- Eager execution

Java:
- Stream is a pipeline abstraction
- map() defines transformation
- Nothing executes until terminal operation
- Lazy execution


---------------------------------------------------------------------
FINAL MENTAL MODEL
---------------------------------------------------------------------

JS:
map() = create new []
map().map().map() = multiple arrays allocated

Java:
map() = define transformation
All steps fused into ONE traversal

Performance Winner (large scale backend):
→ Java Streams

Performance Winner (UI simplicity):
→ JavaScript Arrays

*********************************************************************/

```