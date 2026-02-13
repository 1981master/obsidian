```javascript
fetch("http://localhost:8080/api/data", {
    method: "GET", // or POST, PUT, DELETE, PATCH
    headers: {
        // ✅ Authentication & Authorization
        "Authorization": "Bearer your-jwt-token", // JWT, OAuth token, etc.
        "Cookie": "JSESSIONID=your-session-id",  // Optional, usually handled by browser with credentials: 'include'

        // ✅ Content negotiation
        "Content-Type": "application/json",       // Type of data being sent
        "Accept": "application/json",             // Type of data expected in response

        // ✅ Caching
        "Cache-Control": "no-cache",              // "no-store", "max-age=3600", etc.
        "Pragma": "no-cache",                     // HTTP 1.0 cache control
        "If-None-Match": "etag-value",            // Conditional GET based on ETag
        "If-Modified-Since": "Mon, 01 Feb 2026 12:00:00 GMT",

        // ✅ Security & CORS
        "Origin": "http://localhost:3000",        // Required for CORS requests
        "Referer": "http://localhost:3000/page",  // Page URL sending the request
        "User-Agent": "Mozilla/5.0 ...",          // Optional; browser sets automatically
        "X-Requested-With": "XMLHttpRequest",     // Common for AJAX detection
        "Strict-Transport-Security": "max-age=31536000; includeSubDomains", // Rare, usually server sets it

        // ✅ Custom headers
        "X-Custom-Header": "custom-value",       // Example of any custom header
        "X-Api-Version": "1.0",

        // ✅ Encoding / compression
        "Accept-Encoding": "gzip, deflate, br",  // Usually handled by browser automatically
        "Accept-Language": "en-US,en;q=0.9",

        // ✅ Other
        "Connection": "keep-alive",               // Usually handled by browser
        "Host": "localhost:8080"                  // Usually handled by browser
    },
    credentials: "include" // send cookies for session
});

```

### ⚡ Key Notes:

1. **Browser restrictions:** Some headers (like `Host`, `User-Agent`, `Connection`) **cannot be set manually** in browsers; the browser will set them automatically.
    
2. **CORS:** If your frontend is on a different origin, headers like `Authorization` and `Content-Type: application/json` require **CORS preflight**.
    
3. **Custom headers:** Anything starting with `X-` is common for custom data.
    
4. **Session cookies:** `credentials: 'include'` ensures the browser sends `JSESSIONID` automatically—no need to manually add `Cookie` header.