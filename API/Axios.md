#### Usually axios like:
#### Axios structure (this is the key idea)



```javascript
Axios structure: axios.post(url, body, config)
//url: string
//body: {}
//config: {one or more object/s}

// ❌ Not valid JavaScript
axios.post(
  url = "/users/42",
  body = {...},
  config = {...}
);

```
simple Reusable method. better at the end of this doc
```javascript
function createUser({ url, body, params, headers }) {
  // For return only params and headers below code, but if we need
  return axios.post(url, body, { params, headers });
}
createUser({
  url: "/users/42",
  body: { name: "Alice" },
  params: { filter: "active" },
  headers: {
	Authorization: "Bearer abc123",
	//can have many key values see code below.
  }
});

//header object:
instance.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem('token')
    if (token) {
      config.headers.Authorization = `Bearer ${token}`
    }
    return config
  },
  (error) => {
    return Promise.reject(error)
  },
)
//to pass more config we can do:
  function createUser({ url, body, ...config }) {
    return axios.post(url, body, config);
  }
//Now we can pass as many as we wont.
createUser({
  url: "/users/42",
  body: { name: "Alice" },
  params: { filter: "active" },
  headers: { Authorization: "Bearer abc123",//can add more key value see below },
  timeout: 5000,
  withCredentials: true
});

------------------------------------------------------------------
## ⚠️ Important notes

- Header names are **case-insensitive**, but standard casing is preferred
- Don’t send unnecessary headers — keep it minimal
- Some headers (like `Host`, `Content-Length`) are automatically managed by the browser/Axios.
  
## 🧠 Simple rule of thumb

You usually only need:

- `Authorization` → for auth
- `Content-Type` → for request body
- `Accept` → for response format

Everything else is **use-case specific**

For used for **ETag caching**:

- Client sends: `"If-None-Match": "etag-value"`
- Server responds:
    - `304 Not Modified` (if unchanged)
    - or new data (if changed)

👉 You usually don’t set this manually unless implementing caching logic.
  
createUser({
  url: "/users/42",
  body: { name: "Alice" },
  params: { filter: "active" },
  headers: {
    Authorization: "Bearer abc123",
    // Key must be a string because of the hyphen (-)
    "Content-Type": "application/json",
    Accept: "application/json",
    // ⚠️ Usually NOT set manually in browsers (handled automatically)
    Cookie: "sessionId=xyz",
    // ⚠️ Also controlled by browser in most cases (CORS-related)
    Origin: "https://yourfrontend.com",
    // Caching
    "Cache-Control": "no-cache",
    // ✅ Used for conditional requests (ETag-based caching)
    "If-None-Match": "etag-value",
    // Custom Headers (very common)
    "X-Request-ID": "12345",
    "X-API-Key": "my-api-key",
    // Debugging / Metadata
    // ⚠️ Browser usually sets this automatically (cannot override in frontend JS)
    "User-Agent": "my-app/1.0",
    "Accept-Language": "en-US",
  }
});

Authorization: Bearer <token>

```
- `url` → **path + query params**
    
- `body` → **request body** (`@RequestBody`)
    
- `config.params` → **query params** (`@RequestParam`)
    
- `config.headers` → **headers** (`@RequestHeader`)
## ⚙️ What can go inside `config`?

Here are the most important options:
### 🔹 1. `params` (query string)

params: { filter: "active" }

➡️ `/users/42?filter=active`

---

### 🔹 2. `headers`

headers: {  
  Authorization: "Bearer abc123"  
}

---

### 🔹 3. `timeout`

timeout: 5000 // 5 seconds

---

### 🔹 4. `withCredentials` (cookies)

withCredentials: true

➡️ Needed for sending cookies in cross-origin requests

---

### 🔹 5. `responseType`

responseType: "json" // default  
// or "blob", "text", "arraybuffer"

---

### 🔹 6. `baseURL`

baseURL: "https://api.example.com"

---

### 🔹 7. `auth` (basic auth)

auth: {  
  username: "admin",  
  password: "1234"  
}

---

### 🔹 8. `validateStatus`

validateStatus: (status) => status < 500

➡️ Control which responses count as "error"

---

### 🔹 9. `onUploadProgress` / `onDownloadProgress`

onUploadProgress: (progressEvent) => {  
  console.log(progressEvent.loaded);  
}

---

### 🔹 10. `signal` (cancel request)

signal: controller.signal

---
frontend

```javascript
axios.post(
  `http://localhost:8080/users/42`,   // @PathVariable
  {
    name: "Alice",
    id: 1,
    email: "alice@example.com"
  },                                  // @RequestBody
  {
    params: { filter: "active" },     // @RequestParam
    headers: { token: "abc123" }      // @RequestHeader
  }
);

```
---

backend


```java
@PostMapping("/users/{id}")
public void method(
    @PathVariable Long id,
    @RequestParam String filter,
    @RequestHeader String token,
    @RequestBody UserDto body
) {}

```
---
#### Headers


### 2️⃣ What if you want **many headers**?

There are two options:

#### Option A — Map of headers

```java
@PostMapping("/users/{id}") public void method(     
@PathVariable Long id,     
@RequestParam String filter,     
@RequestHeader Map<String, String> headers, // ← all headers     
@RequestBody UserDto body ) {}
```


- Spring will now **collect all request headers** into the map.
    
- Axios example:
    
```javascript
axios.post(
`/users/42?filter=active`, 
body, 
{   headers: 
		{     
			token: "abc123",     
			"X-Custom-Header": "hello",     
			"Authorization": "Bearer xyz" 
		} 
});
```

- Spring sees:

```java
headers.get("token")           // "abc123" 
headers.get("X-Custom-Header") // "hello" 
headers.get("Authorization")   // "Bearer xyz"
```


✅ This is the **dynamic, reusable approach**.

---

#### Option B — Multiple specific headers

```java
@PostMapping("/users/{id}") 
public void method(     
@RequestHeader("token") String token,     
@RequestHeader("X-Custom-Header") String customHeader,  
@RequestHeader("Authorization") String authorization,   
@RequestBody UserDto body ) {}
```


- Spring expects each header individually.
    
- Axios example:
    

``axios.post(`/users/42`, body, {   headers: {     token: "abc123",     "X-Custom-Header": "hello"   } });``

- Only works for **known headers**; not flexible if you add more later.
    

---

### ✅ Recommendation

For a **reusable API**:

`@RequestHeader Map<String, String> headers`

- Works with **any number of headers**.
    
- Lets you merge dynamic headers in Axios (`...headers`).
    

---

### Recap

|Case|Spring annotation|Notes|
|---|---|---|
|Single known header|`@RequestHeader String token`|Only one header, must match key|
|Multiple dynamic headers|`@RequestHeader Map<String, String> headers`|Can handle any headers from client|
|Multiple specific headers|`@RequestHeader("X") String x, @RequestHeader("Y") String y`|Only works for predefined headers|

---

### use <mark> create </mark> for all requests(Best)
```javascript
import axios from "axios";

// 1️⃣ Create an Axios instance
const axiosInstance = axios.create({
  baseURL: "http://localhost:8080", // optional base URL
  timeout: 10000,
  withCredentials: false,
  headers: {
    "Content-Type": "application/json"
  }
});

// 2️⃣ Add a request interceptor (dynamic headers, auth, logging, etc.)
axiosInstance.interceptors.request.use(
  (config) => {
    // Example: add dynamic Authorization header
    const token = localStorage.getItem("token");
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }

    // You can also log requests
    console.log(`[Request] ${config.method.toUpperCase()} ${config.url}`);
    return config;
  },
  (error) => Promise.reject(error)
);

// 3️⃣ Add a response interceptor (optional)
axiosInstance.interceptors.response.use(
  (response) => response,
  (error) => {
    // Handle global errors
    if (error.response?.status === 401) {
      console.warn("Unauthorized - redirect to login?");
    }
    return Promise.reject(error);
  }
);

// 4️⃣ Fully dynamic reusable request function
export function apiRequest({
  method = "get",             // HTTP method: get, post, put, patch, delete
  url,
  data = null,                // @RequestBody
  params = {},                // @RequestParam
  headers = {},               // @RequestHeader
  timeout,                    // override default timeout
  withCredentials,            // override default
  responseType,               // e.g., "json", "blob", "text"
  validateStatus,             // optional
  onUploadProgress,           // optional
  onDownloadProgress,         // optional
  ...rest                     // capture anything else
}) {
  return axiosInstance({
    method,
    url,
    data,
    params,
    headers: { ...axiosInstance.defaults.headers, ...headers },
    timeout: timeout ?? axiosInstance.defaults.timeout,
    withCredentials: withCredentials ?? axiosInstance.defaults.withCredentials,
    responseType,
    validateStatus,
    onUploadProgress,
    onDownloadProgress,
    ...rest // any other axios config
  });
}

```