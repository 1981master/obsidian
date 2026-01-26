#Simple Context
<mark>Simmple Context</mark>
```javascript
import React, { useContext, createContext, useState } from 'react';

// Create context
const ThemeContext = createContext();

function App() {
  const [color, setColor] = useState('dark');
  const [data, setData] = useState([])

  return (
    <ThemeContext.Provider value={{ color, setColor, data, setData }}>
      <Toolbar />
        <input type='texxt' value={data} onChange={(e) => setData(e.target.value)}>
            </input>
    </ThemeContext.Provider>
  );
}

export default App;

function Toolbar() {
  return <ThemedButton />;
}

function ThemedButton() {
  // use context
  const { color, setColor, data, setData } = useContext(ThemeContext);

  return (
    <div>
      <button className={color}>I'm {color} themed!</button>
      <button onClick={() => setColor(color === 'dark' ? 'light' : 'dark')}>
        Toggle Theme
      </button>
      <h5>{data}</h5>
    </div>
  );
}

```