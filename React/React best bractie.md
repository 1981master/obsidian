❌ Mutation (causes React warning / bugs):

```javascript
import React, { useState } from "react";

export default function App() {
  // ----- ARRAY EXAMPLE ----- //
  const [numbers, setNumbers] = useState([1, 2, 3]);

  ❌ Mutation (causes React warning / bugs)
  const addNumberMutate = () => {
    numbers.push(4);      // directly mutating state
    setNumbers(numbers);  // reference unchanged
  };

  // ✅ Immutable update (safe)
  const addNumberImmutable = () => {
    setNumbers([...numbers, 4]); // new array reference
  };

  // ----- OBJECT EXAMPLE -----
  const [user, setUser] = useState({ name: "Alice", age: 25 });

  // ❌ Mutation (causes React warning / bugs)
  const updateUserMutate = () => {
    user.age = 26;      // directly mutating state
    setUser(user);      // reference unchanged
  };

  // ✅ Immutable update (safe)
  const updateUserImmutable = () => {
    setUser({ ...user, age: 26 }); // new object reference
  };

  return (
    <div>
      <h3>Numbers: {numbers.join(", ")}</h3>
      <button onClick={addNumberMutate}>Add Number (Mutate)</button>
      <button onClick={addNumberImmutable}>Add Number (Immutable)</button>

      <h3>User: {user.name}, Age: {user.age}</h3>
      <button onClick={updateUserMutate}>Update User (Mutate)</button>
      <button onClick={updateUserImmutable}>Update User (Immutable)</button>
    </div>
  );
}

```