# 🔹 1️⃣ Core Java (Senior Level)

### Q: Why is `String` immutable?

**A:**

- Thread-safe without synchronization
    
- Security (used in class loading, DB URLs)
    
- Enables string pool caching
    
- Hashcode caching for `HashMap` keys
    

---

### Q: Difference between `==` and `.equals()`?

**A:**

- `==` → compares references
    
- `.equals()` → compares logical content
    
- `String` overrides `.equals()`; `Object` does not
    

---

### Q: What happens if `hashCode()` is wrong in `HashMap`?

**A:**

- Objects may go into wrong bucket
    
- Retrieval fails even if `.equals()` is true
    
- Breaks HashMap contract → data loss risk
    

---

### Q: `final`, `finally`, `finalize`?

**A:**

- `final` → prevents modification
    
- `finally` → always executes after try
    
- `finalize` → GC hook (deprecated, unsafe)
    

---

### Q: Can static methods be overridden?

**A:**

- No
    
- They are **hidden**, not overridden
    
- Resolved at compile time
    

---

### Q: Abstract class vs Interface (Java 8+)?

**A:**

- Abstract: state + constructors allowed
    
- Interface: multiple inheritance, default methods
    
- Use interface for contracts
    

---

# 🔹 2️⃣ Collections (VERY IMPORTANT)

### Q: How does `HashMap` work internally?

**A:**

- Uses array of buckets
    
- Hash → index
    
- Collisions → linked list / red-black tree
    
- Treeification after threshold (≥8)
    

---

### Q: How are collisions handled?

**A:**

- Same hash → same bucket
    
- Stored as linked list
    
- Converted to tree for performance
    

---

### Q: `ConcurrentHashMap` vs `HashMap`?

**A:**

- Thread-safe
    
- No global locking
    
- Uses CAS + fine-grained locking
    

---

### Q: `Collections.synchronizedMap()` vs `ConcurrentHashMap`?

**A:**

- synchronizedMap → single lock (slow)
    
- ConcurrentHashMap → concurrent reads/writes
    

---

### Q: Fail-fast vs Fail-safe?

**A:**

- Fail-fast → throws `ConcurrentModificationException`
    
- Fail-safe → works on copy (weak consistency)
    

---

# 🔹 3️⃣ Multithreading & Concurrency (CRITICAL)

### Q: `Thread` vs `Runnable` vs `Callable`?

**A:**

- Thread → heavy, not reusable
    
- Runnable → no return value
    
- Callable → returns result + throws exception
    

---

### Q: What is `synchronized`?

**A:**

- Ensures mutual exclusion
    
- Uses intrinsic lock
    
- Blocks other threads
    

---

### Q: `volatile` keyword?

**A:**

- Guarantees visibility
    
- Prevents instruction reordering
    
- Not atomic
    

---

### Q: What is a race condition?

**A:**

- Multiple threads modify shared data
    
- Result depends on execution order
    

---

### Q: How do you prevent deadlocks?

**A:**

- Lock ordering
    
- Timeout locks
    
- Avoid nested locks
    

---

### Q: Why use `ExecutorService`?

**A:**

- Thread reuse
    
- Resource control
    
- Better performance
    

---

### Q: `CompletableFuture` advantage?

**A:**

- Non-blocking async
    
- Chaining tasks
    
- Better error handling
    

---

# 🔹 4️⃣ JVM & Memory

### Q: Stack vs Heap?

**A:**

- Stack → method calls, local vars
    
- Heap → objects, shared
    

---

### Q: Causes of `OutOfMemoryError`?

**A:**

- Memory leak
    
- Large object allocation
    
- Improper GC tuning
    

---

### Q: StackOverflowError vs OOM?

**A:**

- StackOverflow → deep recursion
    
- OOM → heap/metaspace exhausted
    

---

### Q: What is Metaspace?

**A:**

- Stores class metadata
    
- Replaced PermGen
    
- Native memory
    

---

### Q: G1 GC?

**A:**

- Region-based
    
- Predictable pause times
    
- Default for modern JVMs
    

---

# 🔹 5️⃣ Streams & Functional Java

### Q: `map()` vs `flatMap()`?

**A:**

- map → one-to-one
    
- flatMap → one-to-many, flattens
    

---

### Q: Are streams lazy?

**A:**

- Yes
    
- Executed only on terminal operation
    

---

### Q: Parallel streams pros & cons?

**A:**

- Pros: CPU-intensive tasks
    
- Cons: thread contention, blocking I/O issues
    

---

### Q: Streams vs loops?

**A:**

- Streams → declarative, readable
    
- Loops → better for complex logic
    

---

# 🔹 6️⃣ Exception Handling

### Q: Checked vs Unchecked?

**A:**

- Checked → compile-time enforced
    
- Unchecked → runtime (RuntimeException)
    

---

### Q: Can `finally` not execute?

**A:**

- Yes
    
- JVM crash or `System.exit()`
    

---

### Q: `throw` vs `throws`?

**A:**

- `throw` → actually throws
    
- `throws` → declares possibility
    

---

# 🔹 7️⃣ Spring & Transactions (VERY IMPORTANT)

### Q: How does `@Transactional` work?

**A:**

- AOP proxy
    
- Opens transaction before method
    
- Commit/rollback after
    

---

### Q: Propagation types?

**A:**

- REQUIRED
    
- REQUIRES_NEW
    
- SUPPORTS
    
- NESTED
    

---

### Q: Why rollback sometimes doesn’t happen?

**A:**

- Checked exceptions by default
    
- Self-invocation bypasses proxy
    

---

### Q: `@Component` vs `@Service` vs `@Repository`?

**A:**

- Semantic difference
    
- `@Repository` adds exception translation
    

---

# 🔹 8️⃣ Database & ACID

### Q: What is ACID?

**A:**

- Atomicity
    
- Consistency
    
- Isolation
    
- Durability
    

---

### Q: Isolation levels?

**A:**

- READ_UNCOMMITTED
    
- READ_COMMITTED
    
- REPEATABLE_READ
    
- SERIALIZABLE
    

---

### Q: Dirty read / Phantom read?

**A:**

- Dirty → read uncommitted
    
- Phantom → new rows appear
    

---

### Q: What is N+1 problem?

**A:**

- One query for parent
    
- N queries for children
    

---

# 🔹 9️⃣ Messaging (Kafka / RabbitMQ)

### Q: Kafka vs RabbitMQ?

**A:**

- Kafka → event streaming
    
- RabbitMQ → message queue
    

---

### Q: At-least-once vs Exactly-once?

**A:**

- At-least-once → duplicates possible
    
- Exactly-once → idempotent + transactions
    

---

### Q: How handle duplicate messages?

**A:**

- Idempotent consumers
    
- Deduplication via keys
    

---

### Q: What if consumer crashes?

**A:**

- Offset not committed
    
- Message reprocessed
    

---

# 🔹 🔟 System Design (Bank-Style)

### Q: How to design money transfer?

**A:**

- DB transaction
    
- Lock accounts
    
- Debit then credit
    
- Idempotency
    
- Audit logs
    

---

### Q: How ensure consistency in distributed systems?

**A:**

- Saga pattern
    
- Two-phase commit (rare)
    
- Eventual consistency
    

---

## 🏦 FINAL BANK TIP

They expect:

- Clear reasoning
    
- Real production experience
    
- Trade-offs