```html
<!DOCTYPE html>
<html>
<head>
  <title>Page Title</title>
  <style>
    body {
      font-family: Arial, sans-serif;
    }

    .container {
      width: 420px;
      margin: 40px auto; /* 🔥 centers everything */
    }

    .centerText {
      text-align: center;
    }

    form {
      display: grid;
      grid-template-columns: 150px 250px;
      gap: 10px;
      align-items: start;
    }

    .option-group {
      display: flex;
      align-items: center;
      gap: 8px;
    }
  </style>
</head>
<body>

<div class="container">
  <h1 class= "centerText">Sign Up</h1>

  <form>
    <label for="name">Name:</label>
    <input id="name" type="text">

    <label for="username">User Name:</label>
    <input id="username" type="text">

    <label for="password">Password:</label>
    <input id="password" type="password">

    <label for="email">Email:</label>
    <input id="email" type="email">

    <label>Gender:</label>
    <div class="option-group">
      <label><input type="radio" name="gender"> Male</label>
      <label><input type="radio" name="gender"> Female</label>
    </div>

    <label>Certificate:</label>
    <div class="option-group">
      <input type="checkbox" id="certificate">
      <label for="certificate">I have a certificate</label>
    </div>
  </form>
</div>

</body>
</html>


```

```css
# 🎨 CSS — Complete Beginner → Intermediate Guide (Readable Markup)

---

## 🧱 1. BASIC STRUCTURE

`selector {   property: value; }`

- **selector** → what you style
    
- **property** → what you change
    
- **value** → how you change it
    

---

## 🔤 2. TEXT & FONT STYLES

`font-family: Arial, sans-serif;   /* font type */ font-size: 16px;                  /* text size */ font-weight: bold;                /* thickness */ font-style: italic;               /* italic text */ color: #333;                      /* text color */  text-align: center;               /* left | right | center */ text-transform: uppercase;        /* uppercase | lowercase */ text-decoration: underline;       /* underline | none */ line-height: 1.5;                 /* space between lines */ letter-spacing: 1px;              /* space between letters */`

🧠 **Used for:** headings, paragraphs, labels

---

## 📦 3. BOX MODEL (VERY IMPORTANT)

Every element is a box:

`[ margin ]   [ border ]     [ padding ]       [ content ]`

`width: 300px;        /* content width */ height: 50px;        /* content height */  padding: 10px;       /* space inside the box */ margin: 20px;        /* space outside the box */  border: 1px solid #000;  /* border around box */ border-radius: 8px;      /* rounded corners */`

🧠 **Used for:** spacing, cards, forms, layout

---

## 📍 4. DISPLAY TYPES (CORE CONCEPT)

`display: block;      /* takes full width (div, p) */ display: inline;     /* stays inline (span) */ display: inline-block; /* inline but width/height allowed */ display: none;       /* hidden */`

---

## 🔀 5. FLEXBOX (1-D Layout: Row OR Column)

> **Flex = align things in a line**

`display: flex;               /* enable flexbox */  flex-direction: row;         /* row | column */ justify-content: center;     /* horizontal alignment */ align-items: center;         /* vertical alignment */ gap: 10px;                   /* spacing between items */ flex-wrap: wrap;             /* allow wrapping */`

### Common patterns

`justify-content: space-between; justify-content: space-around; justify-content: space-evenly;`

🧠 **Use Flexbox for:**

- Buttons
    
- Menus
    
- Icons + text
    
- Radio / checkbox groups
    

---

## 🧮 6. GRID (2-D Layout: Rows + Columns)

> **Grid = table-like layout**

`display: grid;  grid-template-columns: 150px 250px;   /* define columns */ grid-template-rows: auto;              /* define rows */  gap: 10px;                             /* spacing */  align-items: start;                    /* vertical alignment */ justify-items: center;                 /* horizontal alignment */`

🧠 **Use Grid for:**

- Forms
    
- Dashboards
    
- Page layout
    
- Cards
    

---

## 📐 7. POSITIONING

`position: static;     /* default */ position: relative;   /* move relative to itself */ position: absolute;   /* move relative to parent */ position: fixed;      /* fixed to screen */ position: sticky;     /* sticks on scroll */`

`top: 10px; right: 20px; bottom: 0; left: 0;`

🧠 **Used for:** modals, dropdowns, tooltips

---

## 🎯 8. ALIGNMENT & CENTERING

### Center block horizontally

`margin: 0 auto;`

### Center text

`text-align: center;`

### Perfect center (flex)

`display: flex; justify-content: center; align-items: center;`

---

## 🎨 9. BACKGROUNDS

`background-color: #f5f5f5; background-image: url("img.jpg"); background-size: cover;        /* cover | contain */ background-position: center; background-repeat: no-repeat;`

---

## ✨ 10. SHADOWS & EFFECTS

`box-shadow: 0 4px 10px rgba(0,0,0,0.2); text-shadow: 1px 1px 2px black; opacity: 0.8;`

---

## 🔄 11. TRANSITIONS & ANIMATION

`transition: all 0.3s ease;`

`:hover {   background-color: blue; }`

### Animation

`@keyframes fade {   from { opacity: 0; }   to { opacity: 1; } }`

---

## 📱 12. RESPONSIVE DESIGN

`@media (max-width: 768px) {   .container {     width: 100%;   } }`

🧠 **Used for:** mobile, tablet layouts

---

## 🧪 13. FORM STYLES

`input {   padding: 8px;   border: 1px solid #ccc; }  input:focus {   outline: none;   border-color: blue; }`

---

## 🧠 14. COMMON SELECTORS

`div {}        /* element */ .class {}     /* class */ #id {}        /* id */  div p {}      /* child */ div > p {}    /* direct child */  input[type="text"] {}  /* attribute selector */`

---

## 🏆 FINAL RULES (REMEMBER THESE)

- **HTML = structure**
    
- **CSS = layout + style**
    
- **Flexbox = alignment**
    
- **Grid = layout**
    
- **Margin = outside**
    
- **Padding = inside**
    

---

If you want next:

- 🔥 Flexbox deep dive (with diagrams)
    
- 🔥 Grid deep dive
    
- 🔥 Build full signup UI (styled)
    
- 🔥 CSS interview questions
    

Just tell me 🚀
```