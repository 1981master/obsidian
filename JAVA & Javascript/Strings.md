# **Java vs JavaScript: Strings**

---

## **1️⃣ Basic String creation**

|Java|JavaScript|Notes|
|---|---|---|
|`String s = "Hello";`|`let s = "Hello";`|Both are immutable|
|`new String("Hello")`|`new String("Hello")`|Avoid using `new String()` in JS, it creates an object|

---

## **2️⃣ Length / Access characters**

|Operation|Java|JavaScript|
|---|---|---|
|Length|`s.length()`|`s.length`|
|Char at index|`s.charAt(0)`|`s.charAt(0)` or `s[0]`|
|Substring|`s.substring(1,3)`|`s.substring(1,3)` or `s.slice(1,3)`|
|Concatenate|`s1 + s2` or `s1.concat(s2)`|`s1 + s2` or `` `${s1}${s2}` ``|

---

## **3️⃣ Searching / Finding**

|Operation|Java|JavaScript|
|---|---|---|
|Index of substring|`s.indexOf("e")`|`s.indexOf("e")`|
|Last index of|`s.lastIndexOf("e")`|`s.lastIndexOf("e")`|
|Contains substring|`s.contains("ell")`|`s.includes("ell")`|
|Starts with|`s.startsWith("H")`|`s.startsWith("H")`|
|Ends with|`s.endsWith("o")`|`s.endsWith("o")`|
|Match regex|`s.matches("\\d+")`|`s.match(/\d+/)`|

---

## **4️⃣ Case conversion**

|Operation|Java|JavaScript|
|---|---|---|
|Upper case|`s.toUpperCase()`|`s.toUpperCase()`|
|Lower case|`s.toLowerCase()`|`s.toLowerCase()`|
|Trim|`s.trim()`|`s.trim()`|
|Strip (new in Java 11)|`s.strip()`|`s.trim()`|

---

## **5️⃣ Splitting / Joining**

|Operation|Java|JavaScript|
|---|---|---|
|Split string|`s.split(",")`|`s.split(",")`|
|Join array|`String.join("-", arr)`|`arr.join("-")`|
|Replace|`s.replace("a","b")`|`s.replace("a","b")` (first match)|
|Replace all|`s.replaceAll("a","b")`|`s.replace(/a/g,"b")`|

---

## **6️⃣ Substrings / Extraction**

|Operation|Java|JavaScript|
|---|---|---|
|Substring|`s.substring(2,5)`|`s.substring(2,5)`|
|Slice|N/A|`s.slice(2,5)` or `s.slice(-3)`|
|Char array|`s.toCharArray()`|`Array.from(s)` or `[...s]`|

---

## **7️⃣ Searching / Pattern**

|Operation|Java|JavaScript|
|---|---|---|
|Matches regex|`s.matches("\\d+")`|`s.match(/\d+/)`|
|Replace regex|`s.replaceAll("\\d+","X")`|`s.replace(/\d+/g,"X")`|
|Search index|`s.search("\\d+")`|`s.search(/\d+/)`|

---

## **8️⃣ Comparison**

|Operation|Java|JavaScript|
|---|---|---|
|Equals|`s1.equals(s2)`|`s1 === s2`|
|Equals ignore case|`s1.equalsIgnoreCase(s2)`|`s1.toLowerCase() === s2.toLowerCase()`|
|Compare lexicographically|`s1.compareTo(s2)`|`s1.localeCompare(s2)`|

---

## **9️⃣ Conversion**

|Operation|Java|JavaScript|
|---|---|---|
|Number → String|`String.valueOf(123)`|`123 + ""` or `String(123)`|
|String → Number|`Integer.parseInt("123")`|`parseInt("123")` / `Number("123")`|
|Boolean → String|`String(true)`|`String(true)`|
|String → Char array|`s.toCharArray()`|`[...s]`|

---

## **10️⃣ Extras / Fun JS string methods**

| Method                         | Description               |
| ------------------------------ | ------------------------- |
| `padStart(n, "0")`             | Fill string on left       |
| `padEnd(n, " ")`               | Fill string on right      |
| `repeat(n)`                    | Repeat string n times     |
| `split("").reverse().join("")` | Reverse a string          |
| `includes("x")`                | Check substring           |
| `startsWith` / `endsWith`      | Same as Java              |
| Template strings               | `` `${name} is ${age}` `` |