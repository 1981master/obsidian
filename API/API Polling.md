API polling is a common technique in software development where a client repeatedly asks a server for updated information at regular intervals. It’s like “checking in” periodically to see if something has changed.

Here’s a clear breakdown:

---

# 1️⃣ Definition

**API polling:**

> The process of a client sending repeated requests to an API endpoint to check for new or updated data.

Instead of the server pushing updates automatically, the client initiates the request on a schedule.

---

# 2️⃣ How it works

1. Client sends a request to an API endpoint (e.g., `/notifications`, `/messages`, `/status`).
    
2. Server responds with the current data.
    
3. Client waits for a fixed interval (e.g., 5 seconds, 30 seconds).
    
4. Client sends the next request.
    
5. Repeat indefinitely or until a condition is met.
    

---

# 3️⃣ Example (Conceptual)

- You have a dashboard showing live orders.
    
- The frontend polls the backend every 10 seconds to get the latest order list.
    
- Each poll is a standard GET request to `/api/orders`.
    

---

# 4️⃣ Advantages

- Simple to implement.
    
- Works with almost any API (no special server configuration needed).
    
- Predictable network usage.
    

---

# 5️⃣ Disadvantages

- Can be inefficient: requests may return the same data repeatedly.
    
- Can overload server if many clients poll frequently.
    
- Not real-time — updates are only as fast as the polling interval.
    

---

# 6️⃣ Alternatives

- **WebSockets:** Server pushes updates instantly.
    
- **Server-Sent Events (SSE):** Server sends a stream of updates to the client.
    
- **Long Polling:** Client sends a request that the server holds open until there’s new data.
    

---

💡 **Summary:**  
Polling is a “client asks repeatedly” approach to get updates. It’s simple but can be inefficient compared to push-based alternatives.