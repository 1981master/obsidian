## For accessing pre props
```javascript
import React, { useEffect, useRef } from "react";

function Counter({ value }) {
  const prevValueRef = useRef();

  useEffect(() => {
    prevValueRef.current = value;
  }, [value]);

  const prevValue = prevValueRef.current;

  return (
    <div>
      <p>Current: {value}</p>
      <p>Previous: {prevValue}</p>
    </div>
  );
}

export default Counter;

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