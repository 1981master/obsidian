# **Java vs JavaScript: Data Structures Cheat Sheet**

---

## **1️⃣ Arrays / Lists**

|Feature|Java|JavaScript|Notes|
|---|---|---|---|
|Declaration|`int[] arr = new int[5];`|`let arr = [1,2,3];`|JS arrays are dynamic and can hold mixed types|
|Access|`arr[0]`|`arr[0]`|0-indexed|
|Length|`arr.length`|`arr.length`|Same|
|Add element|`ArrayList<Integer> list = new ArrayList<>(); list.add(5);`|`arr.push(5);`|`push` adds to end, `unshift` adds to start|
|Remove element|`list.remove(0);`|`arr.splice(0,1);`|Splice removes by index|
|Iterate|`for(int i=0;i<arr.length;i++)`|`for(let i=0;i<arr.length;i++)`|Standard for-loop|
|Enhanced iteration|`for(Integer x : list)`|`for(const x of arr)`|JS `for..of` is like Java enhanced for|
|Map / Transform|`list.stream().map(x->x*2).collect(Collectors.toList())`|`arr.map(x => x*2)`|Returns new collection|
|Filter|`list.stream().filter(x->x>5).collect(...)`|`arr.filter(x => x>5)`|Returns new array|
|Reduce / Sum|`list.stream().reduce(0,Integer::sum)`|`arr.reduce((acc,x)=>acc+x,0)`|Returns single value|

---

## **2️⃣ Maps / Objects**

|Feature|Java|JavaScript|Notes|
|---|---|---|---|
|Declaration|`Map<String,Integer> map = new HashMap<>();`|`let map = { a:1, b:2 }` or `let map = new Map();`|JS objects can be used like maps, but Map preserves insertion order|
|Add element|`map.put("a",1);`|`map["a"]=1` or `map.set("a",1)`|`Map` object uses `.set`|
|Get element|`map.get("a");`|`map["a"]` or `map.get("a")`||
|Delete element|`map.remove("a");`|`delete map["a"]` or `map.delete("a")`||
|Iterate keys/values|`for(Map.Entry<String,Integer> e: map.entrySet())`|`for(const [k,v] of Object.entries(map))`|Destructuring works in JS|
|Filter / Transform|`map.entrySet().stream().filter(...).collect(Collectors.toMap(...))`|`Object.fromEntries(Object.entries(map).filter(([k,v]) => v>0))`|Returns new object|
|Keys only|`map.keySet()`|`Object.keys(map)`|Array of keys in JS|
|Values only|`map.values()`|`Object.values(map)`|Array of values in JS|

---

## **3️⃣ Sets**

|Feature|Java|JavaScript|Notes|
|---|---|---|---|
|Declaration|`Set<String> set = new HashSet<>();`|`let set = new Set();`|JS Set stores unique values|
|Add|`set.add("A");`|`set.add("A");`||
|Delete|`set.remove("A");`|`set.delete("A");`||
|Contains|`set.contains("A");`|`set.has("A");`||
|Iterate|`for(String s : set)`|`for(const s of set)`||
|Size|`set.size();`|`set.size;`||

---

## **4️⃣ Stack / Queue**

|Feature|Java|JavaScript|Notes|
|---|---|---|---|
|Stack|`Stack<Integer> stack = new Stack<>();`|`let stack = [];`|Use array in JS|
|Push / Pop|`stack.push(5); stack.pop();`|`stack.push(5); stack.pop();`|LIFO|
|Peek|`stack.peek();`|`stack[stack.length-1]`||
|Queue|`Queue<Integer> q = new LinkedList<>();`|`let queue = [];`|Use array with push/shift|
|Enqueue / Dequeue|`q.add(5); q.poll();`|`queue.push(5); queue.shift();`|FIFO|

---

## **5️⃣ Linked List**

|Feature|Java|JavaScript|Notes|
|---|---|---|---|
|Singly / Doubly|`LinkedList<Integer> list = new LinkedList<>();`|`No built-in, implement manually`|JS arrays can sometimes replace linked lists|
|Add / Remove|`list.add(5); list.remove(0);`|`arr.push(5); arr.splice(0,1);`||

---

## **6️⃣ Arrays vs Typed Arrays**

|Feature|Java|JavaScript|Notes|
|---|---|---|---|
|Integer array|`int[] arr = new int[5];`|`let arr = [1,2,3];`|JS arrays are flexible|
|Typed array|`int[] arr`|`let arr = new Int32Array(5)`|JS TypedArrays exist for performance & numeric ops|

---

## **7️⃣ Functional / Streams / Array Methods**

|Feature|Java|JavaScript|Notes|
|---|---|---|---|
|Map / transform|`list.stream().map(x->x*2).collect(Collectors.toList())`|`arr.map(x=>x*2)`||
|Filter / select|`list.stream().filter(x->x>5).collect(...)`|`arr.filter(x=>x>5)`||
|Reduce / accumulate|`list.stream().reduce(0,Integer::sum)`|`arr.reduce((acc,x)=>acc+x,0)`||
|forEach / iteration|`list.forEach(x->System.out.println(x))`|`arr.forEach(x=>console.log(x))`|JS `forEach` does not return a new array|

---

## **8️⃣ Notes for Java Devs in JS**

1. **Arrays in JS are dynamic**, unlike Java arrays.
    
2. **Objects `{}`** are like `Map<String,Object>` but keys are always strings.
    
3. **Map and Set exist in JS**, but often you can use objects or arrays for simple data.
    
4. **Array methods** (`map`, `filter`, `reduce`) always return new arrays; `forEach` doesn’t.
    
5. **No native LinkedList or TreeSet** in JS; you implement manually or use libraries.
    
6. **Functional style** is much more common in JS; you can chain `map().filter().reduce()`.

