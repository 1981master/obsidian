# 🔥 1️⃣ Kafka + EXACTLY-ONCE Deep Dive (Bank Level)

Banks care about **no double debit / no lost transaction**.

---

## 1️⃣ Kafka delivery semantics

### At-most-once

- Message may be lost
    
- Never duplicated
    
- ❌ Not acceptable for banks
    

---

### At-least-once (MOST COMMON)

- Message processed **one or more times**
    
- Duplicates possible
    
- ✅ Acceptable **only with idempotency**
    

---

### Exactly-once (EOS)

- Message processed **once and only once**
    
- No duplicates
    
- No loss
    
- ⚠️ Hard & expensive
    

---

## 2️⃣ What “Exactly-Once” REALLY means in Kafka

> Kafka **does NOT magically prevent duplicates**

**Exactly-once =**

- Idempotent producer
    
- Transactional producer
    
- Atomic read → process → write
    

---

## 3️⃣ Idempotent Producer (REQUIRED)

### What problem does it solve?

- Prevents duplicate messages when producer retries
    

### How?

- Kafka assigns **Producer ID (PID)**
    
- Tracks sequence numbers
    
- Broker discards duplicates
    

### Config (INTERVIEW GOLD)

```text
enable.idempotence=true 
acks=all 
retries=Integer.MAX_VALUE max.in.flight.requests.per.connection=5
```


---

## 4️⃣ Transactional Producer (CORE OF EOS)

### What it guarantees?

- Either **all messages are written**
    
- Or **none are**
    

### Bank use-case

> Debit + Credit + Audit event  
> All must succeed or rollback

---

### Producer transaction flow

1. `initTransactions()`
    
2. `beginTransaction()`
    
3. Produce messages
    
4. `commitTransaction()` OR `abortTransaction()`
    

---

## 5️⃣ Exactly-once with Kafka Streams / Consumer

### The BIG rule

> **Offsets must be committed inside the transaction**

---

### Consumer + Producer EXACTLY-ONCE FLOW

1. Consumer reads message
    
2. Business logic executes
    
3. Producer writes output
    
4. Offset committed **atomically**
    
5. Transaction committed
    

If crash happens → rollback → reprocess safely

---

## 6️⃣ Why banks STILL use At-least-once + Idempotency

### Exactly-once drawbacks

- Higher latency
    
- Complex debugging
    
- Broker overhead
    

### Bank reality

✔ At-least-once  
✔ Idempotent consumers  
✔ Deduplication tables

---

## 7️⃣ Idempotent Consumer (MOST IMPORTANT)

### Pattern used in banks

- Unique transaction ID
    
- Store processed IDs
    
- Reject duplicates
    

---

### Example logic (conceptual)

`IF transaction_id exists → skip ELSE process + store transaction_id`

---

## 8️⃣ Kafka vs DB Transaction (INTERVIEW QUESTION)

### Q: Can Kafka and DB share same transaction?

**A:** ❌ No (no distributed XA in practice)

### Solution

- Transactional Outbox Pattern
    
- Saga pattern
    

---

## 9️⃣ Transactional Outbox (BANK FAVORITE)

### Flow

1. Write business data + outbox event in DB transaction
    
2. Commit DB
    
3. CDC / Debezium publishes event to Kafka
    

✔ Strong consistency  
✔ Recoverable  
✔ Auditable

---

## 1️⃣0️⃣ Exactly-once summary (SAY THIS IN INTERVIEW)

> “Kafka exactly-once requires transactional producers and atomic offset commits, but in banking systems we usually rely on at-least-once delivery with idempotent consumers and transactional outbox to guarantee correctness.”

---

# 🔥 2️⃣ Spring Security — CODING EXAMPLES (Senior Level)

---

## 1️⃣ Basic Security Configuration (JWT, Stateless)

```java
@Configuration
@EnableWebSecurity
@EnableMethodSecurity
public class SecurityConfig {

    @Bean
    SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.disable())
            .sessionManagement(sm ->
                sm.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            )
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/auth/**").permitAll()
                .anyRequest().authenticated()
            )
            .addFilterBefore(jwtFilter(), UsernamePasswordAuthenticationFilter.class);

        return http.build();
    }

    @Bean
    public JwtFilter jwtFilter() {
        return new JwtFilter();
    }
}

```

---

## 2️⃣ JWT Filter (CORE BANK QUESTION)

```java
public class JwtFilter extends OncePerRequestFilter {

    @Override
    protected void doFilterInternal(
        HttpServletRequest request,
        HttpServletResponse response,
        FilterChain chain
    ) throws ServletException, IOException {

        String authHeader = request.getHeader("Authorization");

        if (authHeader != null && authHeader.startsWith("Bearer ")) {
            String token = authHeader.substring(7);

            if (JwtUtil.validate(token)) {
                Authentication auth =
                    JwtUtil.getAuthentication(token);

                SecurityContextHolder
                    .getContext()
                    .setAuthentication(auth);
            }
        }

        chain.doFilter(request, response);
    }
}

```

---

## 3️⃣ JWT Utility (Simplified)

```java
public class JwtUtil {

    public static boolean validate(String token) {
        // verify signature, expiration
        return true;
    }

    public static Authentication getAuthentication(String token) {
        return new UsernamePasswordAuthenticationToken(
            "user", null, List.of(new SimpleGrantedAuthority("ROLE_USER"))
        );
    }
}

```

---

## 4️⃣ Login Endpoint (AuthenticationManager)

```java
@RestController
@RequestMapping("/auth")
public class AuthController {

    private final AuthenticationManager authManager;

    public AuthController(AuthenticationManager authManager) {
        this.authManager = authManager;
    }

    @PostMapping("/login")
    public String login(@RequestBody LoginRequest req) {
        Authentication auth = authManager.authenticate(
            new UsernamePasswordAuthenticationToken(
                req.username(), req.password()
            )
        );

        return JwtUtil.generateToken(auth);
    }
}

```

---

## 5️⃣ Role-Based Authorization (VERY COMMON)

```java
@PreAuthorize("hasRole('ADMIN')")
@GetMapping("/admin/report")
public String adminOnly() {
    return "Sensitive financial report";
}

```

---

## 6️⃣ Common Spring Security EDGE CASES

### ❌ JWT filter not triggered

- Filter order wrong
    
- Not added before `UsernamePasswordAuthenticationFilter`
    

---

### ❌ `@PreAuthorize` not working

- Missing `@EnableMethodSecurity`
    

---

### ❌ SecurityContext lost in async

- ThreadLocal lost
    
- Use `DelegatingSecurityContextExecutor`
    

---

## 7️⃣ Bank Security Best Practices (SAY THIS)

✔ Short JWT expiration  
✔ Refresh tokens  
✔ Audit logs  
✔ Rate limiting  
✔ No sensitive logs  
✔ mTLS for internal calls

---

# 🏦 FINAL INTERVIEW STATEMENT (VERY STRONG)

> “For Kafka, we rely on at-least-once delivery with idempotent consumers and transactional outbox. For security, we use stateless JWT, method-level authorization, and audit logging to ensure compliance and traceability.”