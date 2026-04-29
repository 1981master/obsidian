## 🔥 Key lesson (important)

You mixed up:

- `for...in` → indexes
- `for...of` → values

```javascript
//return double array of given array of numbers.
function doubleArray(arr) {
  if (!arr) return;

  let result = [];

  for (let item of arr) {
    result.push(item * 2);
  }

  return result;
}
```

## ✅ Your map version (almost correct)


```javascript
function doubleArrayMap(arr) {  
  if (!arr) return;  
  
  return arr.map(item => item * 2);  
}
```