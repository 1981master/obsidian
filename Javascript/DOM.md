## 1️⃣ Selecting Elements (Finding nodes)

- `document.getElementById(id)` → Select a single element by its ID.
    
- `document.getElementsByClassName(className)` → Live HTMLCollection of elements with the class.
    
- `document.getElementsByTagName(tagName)` → Live HTMLCollection of elements with the tag.
    
- `document.querySelector(cssSelector)` → Select the first element matching CSS selector.
    
- `document.querySelectorAll(cssSelector)` → NodeList of all elements matching CSS selector.
    

> **Tip:** `querySelector` / `querySelectorAll` are the most flexible.

---

## 2️⃣ Creating / Adding / Removing Elements

- `document.createElement(tagName)` → Create a new element node.
    
- `document.createTextNode(text)` → Create a text node.
    
- `parent.appendChild(child)` → Add a child node to a parent.
    
- `parent.insertBefore(newNode, referenceNode)` → Insert before a specific child.
    
- `parent.removeChild(child)` → Remove a child node.
    
- `parent.replaceChild(newNode, oldNode)` → Replace a child node with a new one.
    
- `element.innerHTML` → Get/set HTML content of an element.
    
- `element.textContent` → Get/set plain text content.
    

---

## 3️⃣ Attributes / Classes / IDs

- `element.getAttribute(name)` → Get an attribute value.
    
- `element.setAttribute(name, value)` → Set an attribute value.
    
- `element.removeAttribute(name)` → Remove an attribute.
    
- `element.id` → Get/set element’s `id`.
    
- `element.className` → Get/set element’s `class`.
    
- `element.classList.add(name)` → Add a class.
    
- `element.classList.remove(name)` → Remove a class.
    
- `element.classList.toggle(name)` → Toggle a class.
    
- `element.classList.contains(name)` → Check if class exists.
    

---

## 4️⃣ Events

- `element.addEventListener(event, handler, options)` → Attach an event listener.
    
- `element.removeEventListener(event, handler)` → Remove an event listener.
    
- `element.onclick` → Older style, not recommended for multiple listeners.
    

**Common events:**

- `click`, `input`, `change`, `submit`, `keydown`, `keyup`, `load`, `DOMContentLoaded`.
    

---

## 5️⃣ Traversing the DOM

- `element.parentNode` → Parent element.
    
- `element.children` → HTMLCollection of child elements.
    
- `element.childNodes` → All child nodes (includes text nodes).
    
- `element.firstChild` → First child node.
    
- `element.lastChild` → Last child node.
    
- `element.nextSibling` → Next node at the same level.
    
- `element.previousSibling` → Previous node at the same level.
    

> **Tip:** Use `.children` for elements only (skip text nodes).

---

## 6️⃣ Styling / Layout

- `element.style.property = value` → Inline style (e.g., `element.style.color = "red"`).
    
- `window.getComputedStyle(element)` → Get the computed style of an element.
    
- `element.classList` → Best way to toggle CSS classes.
    

---

## 7️⃣ Forms / Inputs

- `document.forms` → Collection of all `<form>` elements.
    
- `form.elements` → Collection of all input elements in a form.
    
- `input.value` → Get/set input value.
    
- `input.checked` → Boolean for checkbox/radio.
    
- `input.disabled` → Boolean for disabled state.
    

---

## 8️⃣ Useful Properties

- `document.body` → `<body>` element.
    
- `document.head` → `<head>` element.
    
- `document.documentElement` → `<html>` element.
    
- `document.activeElement` → Currently focused element.
    
- `document.readyState` → `"loading"`, `"interactive"`, `"complete"`.
    

---

### 🔑 Summary — What you **really need**

1. **Selection:** `querySelector`, `getElementById`, `getElementsByClassName`.
    
2. **Manipulation:** `createElement`, `appendChild`, `removeChild`, `innerHTML`, `textContent`.
    
3. **Attributes / classes:** `getAttribute`, `setAttribute`, `classList`.
    
4. **Events:** `addEventListener`, `removeEventListener`.
    
5. **Traversal:** `parentNode`, `children`, `firstChild`, `lastChild`.
    
6. **Forms / inputs:** `forms`, `elements`, `value`, `checked`.
    
7. **Styling:** `style` + `getComputedStyle`.