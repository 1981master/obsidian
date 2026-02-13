```javascript
import axios from 'axios'

// ========================
// 1️⃣ Create an Axios instance
// ========================
// - Centralized configuration for base URL, headers, timeout, etc.
// - Automatically prepends `baseURL` to all requests
// - Makes switching dev/prod environments easy via .env
// - Allows multiple instances for different backends

const API = axios.create({
  baseURL: process.env.REACT_APP_API_URL, // e.g., http://localhost:8081/api
  timeout: 5000,                           // optional: 5 seconds timeout
  headers: {
    'Content-Type': 'application/json',    // default headers
    // Authorization can also be set here if token is fixed
    // Authorization: `Bearer ${token}`
  },
})

export default API

// ========================
// 2️⃣ How it works
// ========================

// GET request
API.get('/todo/1') 
// Actual URL: process.env.REACT_APP_API_URL + '/todo/1'

// POST request
API.post('/todo/saveToDo', { title: 'Learn Redux' }) 
// Actual URL: process.env.REACT_APP_API_URL + '/todo/saveToDo'

// Headers can also be set per request if token changes dynamically
const token = localStorage.getItem('token')
API.get('/todo/1', {
  headers: { Authorization: `Bearer ${token}` },
})

// ========================
// 3️⃣ Advantages of axios.create()
// ========================
// 1. Centralized config: baseURL, headers, timeout, etc.
// 2. Cleaner code: no repeating base URL or headers
// 3. Easy environment switching using .env files
// 4. Multiple instances possible for different APIs

// Example of multiple instances
const AdminAPI = axios.create({ baseURL: 'http://localhost:8082/api' })
const TodoAPI  = axios.create({ baseURL: process.env.REACT_APP_API_URL })

```