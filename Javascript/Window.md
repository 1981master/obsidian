## 1️⃣ Global Methods (functions)

- `alert(message)` → Shows a modal alert box with a message.
    
- `confirm(message)` → Shows an OK/Cancel dialog and returns `true` or `false`.
    
- `prompt(message, default)` → Shows an input dialog and returns the string entered, or `null` if canceled.
    
- `setTimeout(func, ms)` → Executes a function once after a delay of `ms` milliseconds.
    
- `setInterval(func, ms)` → Executes a function repeatedly every `ms` milliseconds.
    
- `clearTimeout(id)` → Cancels a timeout scheduled by `setTimeout`.
    
- `clearInterval(id)` → Cancels a repeating interval scheduled by `setInterval`.
    
- `console.log()` → Logs a message to the browser console.
    
- `decodeURI(uri)` → Decodes a complete URI string.
    
- `encodeURI(uri)` → Encodes a complete URI string.
    
- `decodeURIComponent(uri)` → Decodes a URI component.
    
- `encodeURIComponent(uri)` → Encodes a URI component.
    

---

## 2️⃣ Window Properties

- `window.innerWidth` → Width of the viewport (visible part of the page).
    
- `window.innerHeight` → Height of the viewport.
    
- `window.outerWidth` → Width including browser chrome (toolbars, scrollbars).
    
- `window.outerHeight` → Height including browser chrome.
    
- `window.location` → Object with information about the current URL.
    
- `window.document` → The DOM document object of the page.
    
- `window.navigator` → Browser information (user agent, platform, etc.).
    
- `window.screen` → Screen information (width, height, color depth).
    
- `window.history` → Browser history object.
    
- `window.localStorage` → Storage object for persisting data across sessions.
    
- `window.sessionStorage` → Storage object for the current tab/session.
    
- `window.name` → Name of the window (string).
    
- `window.opener` → Reference to the window that opened this window.
    
- `window.parent` → Parent frame (useful in iframes).
    
- `window.top` → The topmost window object in a window hierarchy.
    
- `window.self` → Reference to the current window itself.
    
- `window.frames` → Array-like list of frames inside the window.
    

---

## 3️⃣ Window Events

- `onload` → Fires when the page is fully loaded.
    
- `onresize` → Fires when the window is resized.
    
- `onscroll` → Fires when the window is scrolled.
    
- `onbeforeunload` → Fires before leaving the page.
    
- `onunload` → Fires when the page is unloaded.
    

---

## 4️⃣ Window Dialog / User Interaction Methods

- `alert()` → Show a simple alert box.
    
- `confirm()` → Show an OK/Cancel dialog.
    
- `prompt()` → Show an input dialog.
    

---

## 5️⃣ Window Timing Methods

- `setTimeout(func, ms)` → Execute a function after a delay.
    
- `setInterval(func, ms)` → Execute a function repeatedly at intervals.
    
- `clearTimeout(id)` → Cancel a timeout.
    
- `clearInterval(id)` → Cancel an interval.
    

---

## 6️⃣ Other Useful Window Objects

- `window.location` → Current URL info; methods include `.reload()`, `.assign()`.
    
- `window.history` → Methods like `.back()`, `.forward()`, `.go()`.
    
- `window.navigator` → Browser info (`userAgent`, `platform`, etc.).
    
- `window.screen` → Screen properties (`width`, `height`).
    
- `window.performance` → Performance and timing info.
    
- `window.XMLHttpRequest` → Old-school HTTP requests.
    
- `window.fetch` → Modern HTTP requests.
    
- `window.EventSource` → Server-sent events.
    
- `window.WebSocket` → WebSocket connections.
    
- `window.location.hash` → Hash fragment of the URL.
    

---

### 🔑 Key Points to Remember

1. Global variables (`var`) and functions become properties of `window`.
    
2. `let` and `const` do **not** attach to `window`.
    
3. `window` exposes **all browser APIs** like timers, alerts, storage, and DOM access.
    
4. You can call `window` methods explicitly or directly without `window.`


### 1️⃣ Categories that exist but were not fully listed

- **Web APIs / DOM-related**
    
    - `window.addEventListener()` / `window.removeEventListener()`
        
    - `window.getComputedStyle()`
        
    - `window.matchMedia()`
        
    - `window.requestAnimationFrame()`
        
    - `window.cancelAnimationFrame()`
        
- **Clipboard / Web Storage**
    
    - `window.navigator.clipboard` (read/write)
        
- **File / Blob APIs**
    
    - `window.FileReader`
        
    - `window.Blob`
        
    - `window.URL.createObjectURL()`
        
- **Geolocation / Sensors**
    
    - `window.navigator.geolocation`
        
    - `window.DeviceOrientationEvent`
        
- **Networking / WebSockets**
    
    - `window.WebSocket`
        
    - `window.EventSource`
        
- **Performance / Timing / Memory**
    
    - `window.performance.now()`
        
    - `window.performance.timing`
        
    - `window.performance.memory` (Chrome only)
        
- **Window Control / Popups**
    
    - `window.open()`
        
    - `window.close()`
        
    - `window.focus()` / `window.blur()`
        
- **Printing / Screen Capture**
    
    - `window.print()`
        
    - `window.scrollTo()` / `scrollBy()`
        
- **Other experimental APIs** (browser dependent)
    
    - `window.AudioContext`
        
    - `window.ClipboardEvent`
        
    - `window.Notification`
        
    - `window.SpeechSynthesis`
        

---

### 2️⃣ Why there is no “complete list”

- Browsers **extend `window` all the time** with new APIs.
    
- Some methods exist in **specific browsers only**.
    
- Some are **deprecated** or **experimental**.
    

---

### 3️⃣ Key takeaway

> **`window` is the browser global object — everything that is global lives here. There is a core set of methods/properties (like `alert`, `setTimeout`, `document`, `location`) that are always available, and many more advanced APIs depending on your browser.**