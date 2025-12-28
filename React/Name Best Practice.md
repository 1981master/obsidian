## **1. Component Names**

- **PascalCase for components** (start each word with a capital letter)
    
    `function SignUpForm() { ... } const ProductDashboard = () => { ... }`
    
    **Why:** React treats lowercase names as **HTML tags** and capitalized names as **components**.  
    Example error:
    
    `// ❌ Incorrect <signupForm />  // React thinks this is <signupform> HTML element  // ✅ Correct <SignUpForm />`
    
- **File names** should **match component names** (optional but highly recommended)
    
    `src/components/SignUpForm.js   → component: SignUpForm src/components/ProductDashboard.js → component: ProductDashboard`
    

---

## **2. Hooks**

- **Start custom hooks with `use`**
    
    `function useFetchProducts() { ... } function useFormValidation() { ... }`
    
    **Why:** React identifies functions starting with `use` as hooks.  
    **Do not capitalize the `use` part**—it should be camelCase.
    

---

## **3. Event Handlers / Functions**

- Use **camelCase** for functions and handlers
    
    `const handleSubmit = () => { ... } const handleEmailVerification = () => { ... }`
    
- Prefix with `handle` for events, `get/set` for accessors
    
    `const handleClick = () => { ... } const getUserData = () => { ... } const setProductPrice = (id, price) => { ... }`
    

---

## **4. Props and State Variables**

- **camelCase** for prop names and state
    
    `<ProductCard product={product} onUpdatePrice={updatePrice} /> const [isModalVisible, setIsModalVisible] = useState(false)`
    
- Be descriptive:
    
    `// ❌ Not descriptive const [p, setP] = useState([]) // ✅ Descriptive const [products, setProducts] = useState([])`
    

---

## **5. Constants**

- **UPPER_CASE** for constants, especially fixed values
    
    `const API_URL = 'http://localhost:8080/api' const MAX_IMAGE_SIZE = 1024`
    
- **camelCase** for regular variables
    
    `const productList = [] const newUserEmail = ''`
    

---

## **6. File Organization**

- **Group related components** inside folders
    
    `src/   components/     SignUpForm/       SignUpForm.js       SignUpForm.css       index.js   // optional, re-export     ProductDashboard/       ProductDashboard.js       ProductCard.js`
    
- Use `index.js` to **re-export** for cleaner imports:
    
    `// components/index.js export { default as SignUpForm } from './SignUpForm/SignUpForm' export { default as ProductDashboard } from './ProductDashboard/ProductDashboard'`
    

---

## **7. Misc Best Practices**

- **Avoid abbreviations** unless very common (`id`, `url`, `img`)
    
- **Keep component and file names consistent** to avoid module resolution errors
    
- **React hooks names** must be **camelCase** and **start with `use`**
    
- **JSX elements** that are components must **start with a capital letter**
    

---

### ✅ Quick Summary Table:

|Type|Naming Style|Example|
|---|---|---|
|Component / File|PascalCase|`SignUpForm.js` → `SignUpForm`|
|Props / State / variables|camelCase|`isModalVisible`, `productList`|
|Event handlers|camelCase + handle|`handleClick`, `handleSubmit`|
|Custom Hooks|camelCase + use|`useFetchData`, `useFormValidation`|
|Constants|UPPER_CASE|`API_URL`, `MAX_IMAGE_SIZE`|

---

If you follow this consistently:

1. Components will render correctly (no React thinks it’s an HTML tag)
    
2. File imports won’t break (especially on case-sensitive systems like Linux)
    
3. Your code will be easier for teams and open-source contributions.