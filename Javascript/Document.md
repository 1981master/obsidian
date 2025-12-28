## 1️⃣ What is `document`?

- `document` is a property of `window` (`window.document`).
    
- It represents the **HTML page loaded in the browser**.
    
- You use it to **read, modify, create, and delete HTML elements**.
    

`console.log(document.title);       // shows page title console.log(document.body);        // accesses <body> console.log(document.head);        // accesses <head>`

---

## 2️⃣ Document Properties

- `document.title` → The title of the document (`<title>` tag).
    
- `document.URL` → The full URL of the page.
    
- `document.domain` → The domain of the page.
    
- `document.body` → The `<body>` element.
    
- `document.head` → The `<head>` element.
    
- `document.forms` → Collection of all `<form>` elements.
    
- `document.images` → Collection of all `<img>` elements.
    
- `document.links` → Collection of all `<a>` elements with `href`.
    
- `document.scripts` → Collection of all `<script>` elements.
    
- `document.styleSheets` → List of stylesheets linked in the page.
    
- `document.activeElement` → The currently focused element.
    
- `document.readyState` → Loading state: `"loading"`, `"interactive"`, `"complete"`.
    

---

## 3️⃣ Document Methods

### 🔹 Element Selection

- `document.getElementById(id)` → Returns element with the given `id`.
    
- `document.getElementsByClassName(className)` → Returns live HTMLCollection of elements.
    
- `document.getElementsByTagName(tagName)` → Returns live HTMLCollection of elements.
    
- `document.querySelector(cssSelector)` → Returns the first element matching CSS selector.
    
- `document.querySelectorAll(cssSelector)` → Returns NodeList of all elements matching CSS selector.
    

### 🔹 Creating / Modifying Elements

- `document.createElement(tagName)` → Creates a new element.
    
- `document.createTextNode(text)` → Creates a text node.
    
- `document.createDocumentFragment()` → Creates a lightweight container for multiple nodes.
    
- `document.appendChild(node)` → Appends a child node to a parent.
    
- `document.removeChild(node)` → Removes a child node.
    
- `document.replaceChild(newNode, oldNode)` → Replaces a child node.
    

### 🔹 Attribute / Class / ID Manipulation

- `element.setAttribute(name, value)` → Sets an attribute.
    
- `element.getAttribute(name)` → Gets an attribute.
    
- `element.removeAttribute(name)` → Removes an attribute.
    
- `element.classList.add(name)` → Adds a class.
    
- `element.classList.remove(name)` → Removes a class.
    
- `element.classList.toggle(name)` → Toggles a class.
    
- `element.classList.contains(name)` → Checks for a class.
    

### 🔹 Event Handling

- `element.addEventListener(event, handler, options)` → Registers an event listener.
    
- `element.removeEventListener(event, handler)` → Removes an event listener.
    
- `document.onclick` → Assign click handler directly (not recommended in modern JS).
    

---

## 4️⃣ Document Traversal / Node Relationships

- `document.parentNode` → Parent of the document (usually `null`).
    
- `element.parentNode` → Parent element.
    
- `element.children` → HTMLCollection of child elements.
    
- `element.childNodes` → NodeList of all child nodes (includes text nodes).
    
- `element.firstChild` → First child node.
    
- `element.lastChild` → Last child node.
    
- `element.nextSibling` → Next node in the DOM.
    
- `element.previousSibling` → Previous node in the DOM.
    

---

## 5️⃣ Document Content / Text Methods

- `element.innerHTML` → Gets/sets HTML content.
    
- `element.outerHTML` → Gets/sets the entire element including tags.
    
- `element.textContent` → Gets/sets plain text content.
    
- `element.innerText` → Gets/sets text content respecting CSS visibility.
    

---

## 6️⃣ Document Styling

- `element.style` → Access inline styles (`element.style.color = "red"`).
    
- `window.getComputedStyle(element)` → Get all computed styles for an element.
    

---

## 7️⃣ Document Forms & Input

- `document.forms` → Collection of `<form>` elements.
    
- `form.elements` → Collection of inputs inside a form.
    
- `input.value` → Gets/sets input value.
    
- `input.checked` → Boolean for checkbox/radio.
    
- `input.disabled` → Boolean for disabled state.
    

---

## 8️⃣ Document Events (short list)

- `DOMContentLoaded` → Fires when HTML is parsed and DOM is ready.
    
- `load` → Fires when all resources (images, scripts) are loaded.
    
- `input` → Fires when input value changes.
    
- `change` → Fires when input loses focus after a change.
    

Example:

`document.addEventListener("DOMContentLoaded", () => {   console.log("DOM ready!"); });`

---

## 9️⃣ Useful Document Objects

- `document.body` → `<body>` element.
    
- `document.head` → `<head>` element.
    
- `document.documentElement` → `<html>` element.
    
- `document.links` → All `<a>` elements with `href`.
    
- `document.images` → All `<img>` elements.
    
- `document.forms` → All `<form>` elements.
    
- `document.scripts` → All `<script>` elements.
    

---

### 🔑 Key Points to Remember

1. `document` is your **gateway to the page** — you can read, create, update, delete any element.
    
2. **Selection**: `getElementById`, `querySelector`, `getElementsByClassName`.
    
3. **Manipulation**: `innerHTML`, `textContent`, `setAttribute`, `appendChild`, `removeChild`.
    
4. **Events**: Use `addEventListener` for modern JS.
    
5. All global `window` objects like `document` are always accessible.