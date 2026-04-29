# The Main CSS Layout Systems

### 1. Normal Document Flow (Default)

This is the **base layout of the entire page**.

Elements stack automatically:

<h1>Title</h1>  
<p>Text</p>  
<button>Click</button>

Result:

Title  
Text  
Button

This is called **Normal Flow** (the real base of CSS).

---

### 2. Flexbox (1-Dimensional Layout)

Used for:

- Navbar
- Buttons
- Cards
- Aligning items

Example:

.container {  
  display: flex;  
}

Flexbox = **Row OR Column**

---

### 3. Grid (2-Dimensional Layout)

Used for:

- Full page layout
- Dashboards
- Product grids

Example:

.container {  
  display: grid;  
  grid-template-columns: 200px 1fr;  
}

Grid = **Rows AND Columns**

---

# Real World Example

Most modern websites use **combination**:

Page (Grid)  
 ├── Navbar (Flexbox)  
 ├── Sidebar (Flexbox)  
 └── Content (Grid)  
        └── Cards (Flexbox)

Example:

- Amazon → Grid + Flexbox
- YouTube → Grid + Flexbox
- Facebook → Grid + Flexbox

---

# Modern Best Practice

Most developers do:

- Grid → page layout
- Flexbox → components

Example:

.page {  
  display: grid;  
  grid-template-columns: 250px 1fr;  
}  
  
.navbar {  
  display: flex;  
}  
  
.cards {  
  display: grid;  
}

---

# Simple Rule to Remember

- Default → base layout
- Flexbox → align things
- Grid → structure page

---

Since you're building **Osly shopping dashboard**, you'll likely use:

- Grid → dashboard layout
- Flexbox → product cards
- Flexbox → navbar