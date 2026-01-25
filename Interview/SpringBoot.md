## 1️⃣ Spring Boot Basics

### Q: What problem does Spring Boot solve?

**A:**

- Eliminates boilerplate Spring configuration
    
- Auto-configuration based on classpath
    
- Embedded servers (Tomcat/Jetty)
    
- Production-ready features (Actuator)
    

---

### Q: Difference between Spring and Spring Boot?

**A:**

- Spring → framework, manual configuration
    
- Spring Boot → opinionated setup, auto-config
    
- Boot runs standalone
    

---

### Q: What is auto-configuration?

**A:**

- Automatically configures beans
    
- Based on:
    
    - Classpath
        
    - Properties
        
    - Existing beans
        
- Implemented via `@EnableAutoConfiguration`
    

---

### Q: How to disable auto-configuration?

**A:**

- `exclude` in `@SpringBootApplication`
    
- `spring.autoconfigure.exclude` property
    

---

## 2️⃣ Spring Boot Startup & Internals

### Q: What happens when Spring Boot starts?

**A:**

1. ApplicationContext created
    
2. Auto-configuration runs
    
3. Beans instantiated
    
4. Embedded server starts
    
5. Application ready
    

---

### Q: What is `@SpringBootApplication`?

**A:**  
Combination of:

- `@Configuration`
    
- `@EnableAutoConfiguration`
    
- `@ComponentScan`
    

---

### Q: How does Spring Boot know which beans to create?

**A:**

- Classpath scanning
    
- Conditional annotations
    
- Properties evaluation
    

---

## 3️⃣ Dependency Injection & Beans

### Q: `@Component` vs `@Service` vs `@Repository`?

**A:**

- Same behavior
    
- Semantic meaning
    
- `@Repository` enables exception translation
    

---

### Q: Constructor vs Field injection?

**A:**

- Constructor injection preferred
    
- Immutable dependencies
    
- Easier testing
    

---

### Q: Bean scopes in Spring Boot?

**A:**

- singleton (default)
    
- prototype
    
- request
    
- session
    

---

### Q: What is `@Primary`?

**A:**

- Resolves multiple bean conflicts
    
- Preferred bean injection
    

---

### Q: Difference between `@Autowired` and `@Qualifier`?

**A:**

- `@Autowired` → type-based
    
- `@Qualifier` → name-based
    

---

## 4️⃣ Configuration & Properties

### Q: `application.properties` vs `application.yml`?

**A:**

- Same functionality
    
- YAML is hierarchical & readable
    

---

### Q: How to map properties to a class?

**A:**

- `@ConfigurationProperties`
    
- Type-safe binding
    

---

### Q: Profiles in Spring Boot?

**A:**

- Environment-based config
    
- `dev`, `test`, `prod`
    
- Activated via `spring.profiles.active`
    

---

---

## 5️⃣ REST APIs

### Q: `@Controller` vs `@RestController`?

**A:**

- `@Controller` → returns view
    
- `@RestController` → returns JSON
    

---

### Q: `@RequestParam` vs `@PathVariable`?

**A:**

- RequestParam → query params
    
- PathVariable → URI variables
    

---

### Q: How to handle exceptions globally?

**A:**

- `@ControllerAdvice`
    
- `@ExceptionHandler`
    

---

### Q: HTTP PUT vs PATCH?

**A:**

- PUT → full update
    
- PATCH → partial update
    

---

## 6️⃣ Transactions (VERY IMPORTANT FOR BANKS)

### Q: How does `@Transactional` work internally?

**A:**

- AOP proxy
    
- Starts transaction before method
    
- Commit or rollback after
    

---

### Q: Default rollback behavior?

**A:**

- Rollback on unchecked exceptions
    
- Not on checked exceptions
    

---

### Q: Transaction propagation types?

**A:**

- REQUIRED
    
- REQUIRES_NEW
    
- SUPPORTS
    
- MANDATORY
    
- NESTED
    
- NOT_SUPPORTED
    
- NEVER
    

---

### Q: Isolation levels?

**A:**

- READ_UNCOMMITTED
    
- READ_COMMITTED
    
- REPEATABLE_READ
    
- SERIALIZABLE
    

---

### Q: Why `@Transactional` sometimes doesn’t work?

**A:**

- Self-invocation
    
- Private methods
    
- Exception swallowed
    

---

## 7️⃣ JPA / Hibernate (Spring Boot)

### Q: What is the N+1 problem?

**A:**

- One query for parent
    
- N queries for children
    

---

### Q: Lazy vs Eager fetching?

**A:**

- Lazy → loaded on access
    
- Eager → loaded immediately
    

---

### Q: How to solve N+1?

**A:**

- Fetch join
    
- EntityGraph
    
- Batch fetching
    

---

### Q: `save()` vs `saveAndFlush()`?

**A:**

- save → deferred flush
    
- saveAndFlush → immediate DB write
    

---

## 8️⃣ Spring Boot Security

### Q: How does Spring Security work?

**A:**

- Filter chain
    
- Authentication
    
- Authorization
    

---

### Q: JWT vs Session authentication?

**A:**

- JWT → stateless
    
- Session → server state
    

---

### Q: Where is authentication logic placed?

**A:**

- `AuthenticationManager`
    
- `UserDetailsService`
    

---

### Q: How to secure REST APIs?

**A:**

- JWT
    
- OAuth2
    
- Role-based access
    

---

## 9️⃣ Actuator & Monitoring

### Q: What is Spring Boot Actuator?

**A:**

- Production monitoring
    
- Health, metrics, info
    

---

### Q: Common actuator endpoints?

**A:**

- `/health`
    
- `/metrics`
    
- `/info`
    
- `/env`
    

---

## 🔟 Performance & Best Practices

### Q: How to improve Spring Boot performance?

**A:**

- Connection pooling
    
- Caching
    
- Async processing
    
- Proper GC
    

---

### Q: How do you handle async tasks?

**A:**

- `@Async`
    
- `CompletableFuture`
    

---

### Q: Why avoid field injection?

**A:**

- Hidden dependencies
    
- Testing difficulty
    

---

## 🏦 BANK INTERVIEW GOLD QUESTIONS

### Q: How do you ensure transaction safety in money transfer?

**A:**

- DB transaction
    
- Proper isolation
    
- Idempotency
    
- Audit logging
    

---

### Q: How do you handle rollback in distributed systems?

**A:**

- Saga pattern
    
- Compensating transactions
    

---

## ✅ FINAL ADVICE

Banks expect:

- Transaction mastery
    
- Thread safety
    
- Clear explanations
    
- Real production examples