## For accessing pre props
```javascript
import React from 'react';
import { useState, useRef, useEffect } from 'react'//1 add useRef to import

function App() {
  const [count, setCount] = useState(0)
  
  const ref = useRef()//2 create refrence to useRef
  
  useEffect(()=>{
    ref.current = count;//3 use useEffect to get updadate count assign it to ref
  }, [count])
    const prev = ref.current;//4 get the prev value
  
  const styles = {
    main: {
      padding: '20px',
    },
    title: {
      color: '#5C6AC4'
    },
  };

  return (
    <div style={styles.main}>
      <p>Besm ALAH</p>
      <p>Count:  {count}</p>
      <p>Previous Value: {prev}</p>
      
      <button onClick={()=>{return setCount((prev) => prev +1)}}> Change Count</button>
    </div>
  )
}

export default App
 

```

## 🧠 What happens (very briefly)

1. First render
    
    - `prevValueRef.current` → `undefined`
        
2. `useEffect` runs **after render**
    
    - stores current `value`
        
3. Next render
    
    - `prevValueRef.current` = **previous value**
        

✔ `useRef` persists across renders  
✔ No re-render caused  
✔ Clean & predictable

---

## 🎯 Interview one-liner

> “I use `useRef` to store previous props because refs persist across renders without triggering re-renders.”

---
<mark> useRef for Prev Props/State </mark>

```javascript
import React, { useEffect, useRef } from "react";

function UserProfile({ name }) {
  // Create a ref to store previous prop value
  const prevNameRef = useRef();

  useEffect(() => {
    // After every render, update ref to current prop
    prevNameRef.current = name;
  }, [name]);

  const prevName = prevNameRef.current;

  return (
    <div>
      <h2>Current Name: {name}</h2>
      <h3>Previous Name: {prevName}</h3>
    </div>
  );
}

export default function App() {
  const [name, setName] = React.useState("Alice");

  return (
    <div>
      <UserProfile name={name} />
      <button onClick={() => setName("Bob")}>Change to Bob</button>
      <button onClick={() => setName("Charlie")}>Change to Charlie</button>
    </div>
  );
}

```

<mark> The main benefit of using useRef to store previous props is:</mark>

## 1️⃣ You can compare current vs previous value

React does **not** automatically give you the previous prop/state.  
`useRef` lets you manually store it without causing re-renders.

Example use cases:

- Detect if a value changed
    
- Trigger animations only when value updates
    
- Run logic only when a specific prop changes
    
- Debugging prop changes
    

---

## 2️⃣ It does NOT trigger re-render

Updating `ref.current`:

- ✅ Does NOT re-render component
    
- ✅ Keeps value between renders
    
- ✅ Is very lightweight
    

If you used `useState` instead:

- It would cause an extra render
    
- Less efficient for just storing previous value
    

---

## 3️⃣ Useful for conditional logic

Example:

```javascript
if (prevName && prevName !== name) {
   console.log("Name changed!");
}
```

---

## 🔥 Simple summary

`useRef` for previous props is useful when:

- You need the old value
    
- You don’t want extra renders
    
- You want to compare before/after values
    

It’s mainly for **tracking**, not for displaying UI state.