# 🔥 1️⃣ Spring Boot Transaction EDGE CASES (Senior Level)

---

### Q: Why does `@Transactional` NOT work on private methods?

**A:**

- Spring uses **proxies**
    
- Private methods are **not proxied**
    
- Transaction never starts
    

---

### Q: Why does `@Transactional` fail on self-invocation?

**A:**

- Method call stays inside same class
    
- Proxy is bypassed
    
- No transaction applied
    

**Bank fix:** Move method to another service

---

### Q: Why rollback didn’t happen even though exception was thrown?

**A:**

- Checked exception by default does NOT trigger rollback
    
- Exception was caught and swallowed
    

**Fix:**

`@Transactional(rollbackFor = Exception.class)`

---

### Q: What happens if exception is thrown AFTER DB commit?

**A:**

- Transaction already committed
    
- Cannot rollback
    
- Leads to inconsistent state
    

**Bank solution:**

- Two-phase validation
    
- Compensating transaction
    

---

### Q: Difference between REQUIRED vs REQUIRES_NEW?

**A:**

- REQUIRED → joins existing transaction
    
- REQUIRES_NEW → suspends existing, starts new
    

**Bank use-case:**  
Audit logs → `REQUIRES_NEW`

---

### Q: What is transaction propagation NEVER?

**A:**

- Fails if transaction exists
    
- Used for non-transactional logic
    

---

### Q: Can multiple threads share same transaction?

**A:**

- ❌ No
    
- Transaction is thread-bound
    

---

### Q: How does Spring bind transaction to thread?

**A:**

- `ThreadLocal` via `TransactionSynchronizationManager`
    

---

### Q: Isolation level used by banks?

**A:**

- Usually `READ_COMMITTED`
    
- `SERIALIZABLE` only for critical operations
    

---

# 🔥 2️⃣ Spring Security – DEEP DIVE (Bank Grade)

---

### Q: How does Spring Security work internally?

**A:**

- Servlet filter chain
    
- Requests pass through multiple filters
    
- SecurityContext stored per request
    

---

### Q: What is `SecurityContext`?

**A:**

- Holds authentication details
    
- Stored in ThreadLocal
    

---

### Q: Authentication vs Authorization?

**A:**

- Authentication → who are you
    
- Authorization → what can you access
    

---

### Q: JWT flow in Spring Security?

**A:**

1. Login → credentials validated
    
2. JWT generated
    
3. JWT sent in Authorization header
    
4. Filter validates token
    
5. SecurityContext populated
    

---

### Q: Why banks prefer JWT?

**A:**

- Stateless
    
- Scales horizontally
    
- No session replication
    

---

### Q: How do you invalidate JWT?

**A:**

- Short expiration
    
- Token blacklist (Redis)
    
- Rotate signing keys
    

---

### Q: What is `OncePerRequestFilter`?

**A:**

- Executes once per request
    
- Used for JWT validation
    

---

### Q: Difference between `UserDetailsService` and `AuthenticationProvider`?

**A:**

- UserDetailsService → loads user
    
- AuthenticationProvider → validates credentials
    

---

### Q: CSRF — when enabled?

**A:**

- Enabled for session-based auth
    
- Disabled for stateless JWT APIs
    

---

### Q: How to secure endpoints?

**A:**

- Method-level security
    
- `@PreAuthorize`
    
- Role-based rules
    

---

### Q: Common security mistakes in banks?

**A:**

- Logging sensitive data
    
- Long JWT expiration
    
- Missing rate limiting
    
- No audit trail
    

---

# 🔥 3️⃣ JPA PERFORMANCE TUNING (VERY IMPORTANT)

---

### Q: What is N+1 problem?

**A:**

- One query for parent
    
- N queries for child entities
    
- Massive DB load
    

---

### Q: How to fix N+1?

**A:**

- Fetch join
    
- `@EntityGraph`
    
- Batch fetching
    

---

### Q: LazyInitializationException — why?

**A:**

- Lazy entity accessed outside transaction
    
- Session already closed
    

**Fix:**

- DTO mapping
    
- Fetch join
    
- Open session in view (NOT recommended in banks)
    

---

### Q: EAGER fetching — why dangerous?

**A:**

- Loads unnecessary data
    
- Causes memory & performance issues
    

---

### Q: `save()` vs `saveAndFlush()`?

**A:**

- save → delayed DB write
    
- saveAndFlush → immediate SQL execution
    

---

### Q: First-level vs Second-level cache?

**A:**

- First-level → session scoped
    
- Second-level → shared cache
    

---

### Q: Why banks avoid 2nd-level cache for money?

**A:**

- Risk of stale data
    
- Consistency issues
    

---

### Q: Indexing — when critical?

**A:**

- JOIN columns
    
- WHERE clauses
    
- Foreign keys
    

---

### Q: Pagination best practice?

**A:**

- Use DB pagination
    
- Avoid loading full result sets
    

---

### Q: Why DTO projection preferred?

**A:**

- Avoid entity graph explosion
    
- Better performance
    
- Safer for APIs
    

---

# 🔥 4️⃣ BANK-STYLE MOCK INTERVIEW (Senior)

---

### Q1: How do you design a money transfer service?

**A:**

- Transaction boundary
    
- Lock accounts
    
- Debit then credit
    
- Idempotency key
    
- Audit log
    

---

### Q2: What if two transfers hit same account?

**A:**

- Pessimistic locking
    
- Or optimistic locking with retries
    

---

### Q3: How do you prevent double processing?

**A:**

- Idempotent requests
    
- Unique transaction ID
    
- Deduplication table
    

---

### Q4: What happens if service crashes mid-transfer?

**A:**

- DB rollback
    
- Message replay
    
- Compensating transaction
    

---

### Q5: How do you handle distributed transactions?

**A:**

- Saga pattern
    
- Event-driven consistency
    

---

### Q6: How do you audit all operations?

**A:**

- Separate audit service
    
- `REQUIRES_NEW` transaction
    
- Immutable audit records
    

---

### Q7: How do you secure internal microservice calls?

**A:**

- mTLS
    
- Service-to-service JWT
    
- Network policies
    

---

### Q8: How do you handle high throughput?

**A:**

- Async processing
    
- Kafka
    
- Back-pressure
    
- Rate limiting
    

---

### Q9: What is your biggest production failure lesson?

**A:**

- Always mention:
    
    - Race condition
        
    - Missing rollback
        
    - Poor isolation
        

---

### Q10: Why should we trust you with financial systems?

**A:**

- Emphasize correctness
    
- Defensive coding
    
- Monitoring & alerts
    
- Testing edge cases
    

---

# 🏦 FINAL BANK INTERVIEW ADVICE

They evaluate:  
✔ Depth  
✔ Risk awareness  
✔ Failure handling  
✔ Transaction safety