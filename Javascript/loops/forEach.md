### 1. Logging / debugging

```
arr.forEach(item => {  console.log(item);});
```

You’re not transforming data — just doing something with it.

---

### 2. Updating external state / variables

```
let total = 0;arr.forEach(item => {  total += item;});
```

(Though in modern JS, `reduce` is usually better for this.)

---

### 3. Calling APIs / triggering actions

```
users.forEach(user => {  sendEmail(user);});
```

You’re performing an action per item, not creating a new array.

---

### 4. Mutating objects (sometimes needed)

```
users.forEach(user => {  user.isActive = true;});
```

Here you're intentionally modifying existing objects.

---

### 5. DOM manipulation (very common in frontend)

```
elements.forEach(el => {  el.classList.add('active');});
```

---

### When NOT to use `forEach`

If you're transforming data:

```
// ❌ avoid thisarr.forEach((item, i) => {  arr[i] = item * 2;});
```

Use `map` instead:

```
const newArr = arr.map(item => item * 2);
```

---

### Real-world rule (this is what seniors follow):

- If you see `return` → probably `map`
- If you see side effects (log, API call, mutation) → `forEach`