<mark>JavaScript its passing by reference</mark>

# 🚨 The Real Problem (Without Cloning)
```javascript
const user = { name: "Alice", age: 25 };

const updatedUser = user; // NOT a copy

updatedUser.age = 30;

console.log(user.age); // 30 😱 (original changed!)

```
Both variables point to the **same object in memory**.
# ✅ Real Life Example 1: Editing a Form

Imagine:

- You load user data
    
- You let them edit it
    
- If they click "Cancel", you want original data unchanged
    

### ❌ Without cloning (buggy)
```javascript
const originalUser = { name: "Alice", age: 25 };
const formData = originalUser; // reference copy

formData.age = 30; // user edits form

console.log(originalUser.age); 
// 30 ❌ original already modified

```

You can't "cancel" anymore.

---

### ✅ With cloning (correct)
use: <mark>structuredClone(obj)</mark>
```javascript
const originalUser = { name: "Alice", age: 25 };
const formData = structuredClone(originalUser);

formData.age = 30;

console.log(originalUser.age); 
// 25 ✅ safe

```

Now:

- `formData` is editable
    
- `originalUser` stays untouched
    

---

# ✅ Real Life Example 2: React State (VERY common)

In React, you must NOT mutate state directly.

`const [user, setUser] = useState({ name: "Alice", age: 25 });`

### ❌ Wrong

`user.age = 30; setUser(user); // React may not re-render`

Because:

- You modified the same object
    
- React thinks nothing changed
    

---

### ✅ Correct (clone first)

`const updatedUser = structuredClone(user); updatedUser.age = 30;  setUser(updatedUser);`

Now:

- New object reference
    
- React re-renders properly
    

---

# ✅ Real Life Example 3: Undo / History Feature

Imagine a drawing app:

`const currentState = {   shapes: [{ x: 10, y: 20 }] };  history.push(structuredClone(currentState));`

If you don’t clone:

`history.push(currentState);`

Later changes will modify ALL history entries 😱

Cloning freezes the state at that moment.

---

# 🧠 The Core Concept

Objects are stored in memory like this:

```text
user  ─┐
       ├──> { name: "Alice", age: 25 }
admin ─┘

```

Two variables → same object.

Cloning creates:

`user   ──> { name: "Alice", age: 25 }` 
`admin  ──> { name: "Alice", age: 25 }`

Now they are independent.

---

# 🎯 When You REALLY Need Cloning

You need cloning when:

- Editing temporary data
    
- Working with state management (React, Redux, etc.)
    
- Creating undo/redo features
    
- Preventing side effects
    
- Protecting original API response data
    
- Functional programming patterns
    

---

# 🚀 Simple Rule

If you're going to modify something  
and you don’t want the original affected  
→ **Clone it first**
`JSON.parse(JSON.stringify(obj))` Vs `structuredClone(obj)`

they are both used to **deep copy** objects — but they behave very differently.

---

## 1️⃣ `JSON.parse(JSON.stringify(obj))`

### ✅ What it does well

- Creates a deep copy of **simple JSON-safe objects**
    
- Works in older environments
    
- Easy and widely known trick
    

### ❌ Major limitations

It **breaks or removes**:

- `undefined`
    
- `Date` (turns into string)
    
- `Map`
    
- `Set`
    
- `BigInt`
    
- `Infinity`
    
- `RegExp`
    
- Functions
    
- Circular references (throws error)
    
- Custom class instances (loses prototype)
    

### Example

```javascript
const obj = {
  date: new Date(),
  map: new Map(),
  value: undefined
};

const copy = JSON.parse(JSON.stringify(obj));

console.log(copy);
// {
//   date: "2026-02-18T12:34:56.000Z"
// }
// map and undefined are gone

```

It only preserves data that is valid JSON.

---

## 2️⃣ `structuredClone(obj)`

This is the **modern built-in deep cloning API**.

### ✅ What it supports

- Objects
    
- Arrays
    
- `Date`
    
- `Map`
    
- `Set`
    
- `RegExp`
    
- `ArrayBuffer`
    
- `Blob`
    
- `File`
    
- `BigInt`
    
- Typed arrays
    
- Circular references
    
- Much more
    

### Example

```javascript
const obj = {
  date: new Date(),
  map: new Map([["a", 1]]),
};

const copy = structuredClone(obj);

console.log(copy.date instanceof Date); // true
console.log(copy.map instanceof Map);   // true

```

### ❌ What it still does NOT clone

- Functions
    
- DOM nodes
    
- Class prototype methods (custom prototypes are not preserved exactly)
    

---

## 🔥 Key Differences

|Feature|JSON trick|structuredClone|
|---|---|---|
|Deep copy|✅|✅|
|Circular refs|❌ Error|✅|
|Date preserved|❌ (string)|✅|
|Map / Set|❌|✅|
|BigInt|❌|✅|
|Performance|Slower (string conversion)|Faster|
|Modern API|❌|✅|

---

## 🧠 Why `structuredClone` is Better

1. It does **not serialize to string**
    
2. It preserves **data types**
    
3. It handles **complex structures**
    
4. It supports **circular references**
    
5. It’s the official modern standard
    

---

## 🚀 When to Use What

### Use `structuredClone()` if:

- You're in modern browsers / Node 17+
    
- You need reliable deep cloning
    
- You care about performance
    
- You have complex objects
    

### Use JSON trick only if:

- You’re cloning very simple data
    
- You need compatibility with older environments
    
- You know the object is fully JSON-safe
    

---

## 💡 Bottom Line

`structuredClone()` is the correct modern solution.  
`JSON.parse(JSON.stringify())` is a workaround hack with many limitations.

---
<mark>Shallow Vs Deep copy</mark>
# 🧠 Visual Comparison

| Feature               | Shallow Clone | Deep Clone      |
| --------------------- | ------------- | --------------- |
| Top-level copy        | ✅             | ✅               |
| Nested objects copied | ❌             | ✅               |
| Safe for nested edits | ❌             | ✅               |
| Performance           | Faster        | Slightly slower |
| Memory usage          | Lower         | Higher          |

---
SHALLOW vs DEEP CLONE (Simple Explanation)

🥤 Simple Analogy

- Shallow clone = Copy the box, but inside items are shared.
- Deep clone = Copy the box AND everything inside it.


🔹 1️⃣ SHALLOW CLONE

A shallow clone copies only the first level.
If the object contains nested objects, those nested objects are still shared.

Example:

```javascript
const user = {
  name: "Alice",
  address: {
    city: "New York"
  }
};

const shallowCopy = { ...user };

shallowCopy.name = "Bob";              // ✅ safe
shallowCopy.address.city = "LA";       // ❌ modifies original

console.log(user.address.city); // "LA"
```

Why?

Because both objects share the same nested reference:

user.address ───┐
                ├──> { city: "New York" }
shallow.address ─┘

Only the top-level object was copied.


Common Ways to Shallow Clone:

{ ...obj }              
Object.assign({}, obj)
array.slice()
[...array]

All of these are shallow.


🔥 2️⃣ DEEP CLONE

A deep clone copies everything recursively.
Nested objects are fully duplicated.

Example:

const user = {
  name: "Alice",
  address: {
    city: "New York"
  }
};

const deepCopy = structuredClone(user);

deepCopy.address.city = "LA";

console.log(user.address.city); // "New York" ✅ safe

Now the memory looks like:

user      ──> { address ──> { city: "New York" } }
deepCopy  ──> { address ──> { city: "New York" } }

Two completely separate object trees.


🚨 Real Bug Scenario

const state = {
  user: {
    name: "Alice"
  }
};

const newState = { ...state };

newState.user.name = "Bob";

console.log(state.user.name);
// "Bob" 😱

Developers think they copied state — but they didn’t deeply copy it.


🎯 When to Use Each

Use Shallow Clone when:
- Object is flat (no nested objects)
- You only change top-level fields
- Performance is important
- Updating most React state cases

Use Deep Clone when:
- Object has nested objects
- You will modify nested data
- You need full isolation
- Implementing undo/history features


🚀 Quick Rule

If your object contains:
- objects
- arrays
- maps
- sets

And you plan to modify inside them → use deep clone.
JAVA: SHALLOW vs DEEP COPY (Clear Explanation)

🚨 First: What “Pass by Value” Really Means in Java

Java is always pass by value.

But when dealing with objects:
- The value being passed is the reference
- Not the object itself

So Java copies the reference value, not the object.

--------------------------------------------------

Example: <mark>JAVA</mark>

```java
class User {
    String name;
}

public class Main {
    public static void main(String[] args) {
        User user1 = new User();
        user1.name = "Alice";

        User user2 = user1;  // copy of reference

        user2.name = "Bob";

        System.out.println(user1.name); // Bob 😱
    }
}
```

Why?

Memory looks like this:

user1 ──┐
        ├──> User { name = "Alice" }
user2 ──┘

Even though Java is pass-by-value,
the value copied is the reference.

--------------------------------------------------

🔹 SHALLOW COPY IN JAVA

A shallow copy:
- Copies primitive fields
- Copies object references (not the nested objects)

Example classes:

```java
class Address {
    String city;
}

class User {
    String name;
    Address address;

    public User(String name, Address address) {
        this.name = name;
        this.address = address;
    }
}

Shallow Copy Constructor:

public User(User other) {
    this.name = other.name;
    this.address = other.address; // reference copied
}

Usage:

Address addr = new Address();
addr.city = "New York";

User user1 = new User("Alice", addr);
User user2 = new User(user1); // shallow copy

user2.address.city = "LA";

System.out.println(user1.address.city); // LA 😱
```



Because both users share the same Address.

Memory:

user1.address ───┐
                 ├──> Address { city = "New York" }
user2.address ───┘

--------------------------------------------------

🔥 DEEP COPY IN JAVA

Deep copy:
- Copies primitives
- Creates NEW objects for nested objects

Deep Copy Constructor:
```java
public User(User other) {
    this.name = other.name;
    this.address = new Address();
    this.address.city = other.address.city;
}

Now:

User user2 = new User(user1);

user2.address.city = "LA";

System.out.println(user1.address.city); // New York ✅
```


Memory now:

user1 ──> Address { city = "New York" }
user2 ──> Address { city = "New York" }

Two completely separate objects.

--------------------------------------------------

🧠 Java vs JavaScript Difference

JavaScript:
- Objects are assigned by reference
- Mutations easily affect originals

Java:
- Always pass-by-value
- But the value of an object variable is a reference
- So objects are still shared unless deep copied

--------------------------------------------------

🎯 When Deep Copy Is Needed in Java

- DTO duplication
- Preventing shared mutable state
- Multi-threaded applications
- Caching
- Defensive copying in constructors/getters

Example (Defensive Copying):

public class Person {
    private Date birthDate;

    public Person(Date birthDate) {
        this.birthDate = new Date(birthDate.getTime()); // deep copy
    }

    public Date getBirthDate() {
        return new Date(birthDate.getTime()); // prevent mutation
    }
}

Without this, external code could mutate internal state.

--------------------------------------------------

🚀 Simple Rule for Java

If your class contains:
- Other objects
- Lists
- Maps
- Mutable types

And you copy it without creating new nested objects
→ It’s a shallow copy.

If you manually create new nested objects
→ It’s a deep copy.

--------------------------------------------------

💡 Key Takeaway

Java being “pass by value” does NOT mean objects are copied.

It means:
- The reference value is copied
- The actual object is still shared
- You must explicitly create new nested objects to achieve deep copy

---
JAVA: OTHER WAYS TO DEEP COPY (Without Manually Copying Nested Objects)

Yes ✅ — you do NOT have to manually copy every nested object.
There are several other ways to deep copy in Java.

--------------------------------------------------
1️⃣ Serialization (Built-in Java Way)

Java can deep copy an object by serializing it to bytes
and then deserializing it back into a new object.

All classes must implement Serializable.

Example:

```java
import java.io.*;

public static <T extends Serializable> T deepCopy(T object) {
    try {
        ByteArrayOutputStream bos = new ByteArrayOutputStream();
        ObjectOutputStream out = new ObjectOutputStream(bos);
        out.writeObject(object);
        out.flush();

        ByteArrayInputStream bis = new ByteArrayInputStream(bos.toByteArray());
        ObjectInputStream in = new ObjectInputStream(bis);

        return (T) in.readObject();
    } catch (Exception e) {
        throw new RuntimeException(e);
    }
}
```

Pros:
✔ Automatically deep copies entire object graph
✔ No manual nested copying

Cons:
❌ Slower
❌ All classes must implement Serializable
❌ Not recommended for high-performance code



2️⃣ Apache Commons Lang (SerializationUtils)

Library: org.apache.commons.lang3.SerializationUtils

Example:

import org.apache.commons.lang3.SerializationUtils;

User copy = SerializationUtils.clone(original);

Pros:
✔ Very simple
✔ Deep copies entire object graph

Cons:
❌ Still uses serialization internally
❌ Requires Serializable
❌ Extra dependency

--------------------------------------------------
3️⃣ Using JSON (Jackson or Gson)

Convert object → JSON → back to object.

Example using Jackson:

ObjectMapper mapper = new ObjectMapper();

User copy = mapper.readValue(
    mapper.writeValueAsString(original),
    User.class
);

Pros:
✔ Easy
✔ Works well for DTOs

Cons:
❌ Slower
❌ Ignores transient fields
❌ Can break with complex types
❌ Requires default constructors

--------------------------------------------------
4️⃣ Copy Constructors (Best Practice for Domain Models)

Instead of manually copying nested fields every time,
each class handles copying itself.

Example:

```java
class Address {
    String city;

    Address(Address other) {
        this.city = other.city;
    }
}

class User {
    String name;
    Address address;

    User(User other) {
        this.name = other.name;
        this.address = new Address(other.address);
    }
}
```

Pros:
✔ Fast
✔ Explicit
✔ Safe
✔ No reflection
✔ No serialization overhead

Cons:
❌ Requires writing constructors

👉 This is usually the cleanest production approach.

--------------------------------------------------
5️⃣ Cloneable (NOT Recommended)

Java has clone() but it’s widely considered broken design.

Problems:
❌ Confusing behavior
❌ Shallow by default
❌ Hard to maintain
❌ Requires overriding carefully

Most modern Java developers avoid it.

--------------------------------------------------
🚀 What Professionals Usually Do

High-performance systems:
→ Copy constructors

DTO copying:
→ MapStruct or manual mapping

Quick deep copy for testing:
→ Serialization or Jackson

--------------------------------------------------
💡 Simple Rule

If performance matters:
    → Use copy constructors

If convenience matters:
    → Use serialization or JSON

If code quality matters:
    → Avoid clone()

---

🎯 Bottom Line

Yes — Java has multiple ways to deep copy without manually copying every nested field inline.

But the cleanest and safest production method is:
    Copy constructors per class.

<mark>Example of Deep Copy</mark>

REAL EXAMPLE: COPY CONSTRUCTOR (Deep Copy) – SIMPLE & CLEAN

Goal:
- Show normal constructor
- Show copy constructor
- Prove deep copy works
- Use nested object (Address)

---------------------------------------------
STEP 1: Address Class (with copy constructor)


```java
class Address {
    String city;
    String country;

    // Normal constructor
    public Address(String city, String country) {
        this.city = city;
        this.country = country;
    }

    // Copy constructor (deep copy)
    public Address(Address other) {
        this.city = other.city;
        this.country = other.country;
    }
}
```

---------------------------------------------
STEP 2: User Class (with copy constructor)


```java
class User {
    String name;
    int age;
    Address address;

    // Normal constructor
    public User(String name, int age, Address address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    // Copy constructor (deep copy)
    public User(User other) {
        this.name = other.name;
        this.age = other.age;
        this.address = new Address(other.address); // IMPORTANT
    }
}
```

---------------------------------------------
STEP 3: Test It


```java
public class Main {
    public static void main(String[] args) {

        // Original object
        Address address1 = new Address("New York", "USA");
        User user1 = new User("Alice", 25, address1);

        // Deep copy using copy constructor
        User user2 = new User(user1);

        // Modify copy
        user2.name = "Bob";
        user2.address.city = "Los Angeles";

        // Print results
        System.out.println("Original User:");
        System.out.println(user1.name);                 // Alice ✅
        System.out.println(user1.address.city);         // New York ✅

        System.out.println("\nCopied User:");
        System.out.println(user2.name);                 // Bob
        System.out.println(user2.address.city);         // Los Angeles
    }
}
```

---------------------------------------------
WHAT HAPPENS IN MEMORY

user1  ---> Address("New York")
user2  ---> Address("New York")

Two completely separate Address objects.

Changing user2.address does NOT affect user1.address.

---------------------------------------------
WHY THIS IS THE BEST PRACTICE

✔ Fast (no serialization)
✔ No reflection
✔ Clear and explicit
✔ Safe for production
✔ Works perfectly with nested objects
✔ Easy to maintain

---------------------------------------------
KEY RULE

If a class contains another object:
    In the copy constructor,
    call the copy constructor of that object.

Example:
    this.address = new Address(other.address);

That is what makes it DEEP copy.
