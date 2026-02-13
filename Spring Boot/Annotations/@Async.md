### 🔹 What is `@Async` (Spring)?

`@Async` is used to **run a method asynchronously** in a **separate thread**, so the caller **does not block** waiting for the method to finish.

👉 Fire-and-forget / background execution.

---

## ✅ When to Use `@Async`

- Sending emails
    
- Logging
    
- Calling external APIs
    
- Long-running tasks
    
- Background processing
    

---

## 🔹 Enable Async Support (REQUIRED)

`@Configuration @EnableAsync public class AsyncConfig { }`

---

## 🔹 Simple Example (Void – Fire & Forget)

## 🔹 Thread Pool (Optional but Recommended)


```java
@Configuration
@EnableAsync
public class AsyncConfig {

    @Bean
    public Executor taskExecutor() {
        ThreadPoolTaskExecutor exec = new ThreadPoolTaskExecutor();
        exec.setCorePoolSize(5);
        exec.setMaxPoolSize(10);
        exec.setQueueCapacity(100);
        exec.initialize();
        return exec;
    }
}

```
`emailService.sendEmail(); // returns immediately`

---

## 🔹 Async with Return Value (`Future` / `CompletableFuture`)

```java
@Service
public class EmailService {

    @Async
    public void sendEmail() {
        System.out.println("Running in thread: " +Thread.currentThread().getName());
    }
}

```

---

## 🔹 Important Rules (Interview Gold)

❌ **Will NOT work** if:

- Method is `private`
    
- Method is called inside the same class (self-invocation)
    
- `@EnableAsync` is missing
    

✔ Works via **Spring proxy**



---

## 🔹 `@Async` vs `@Scheduled`

|Feature|@Async|@Scheduled|
|---|---|---|
|Triggered by|Method call|Time|
|Background|✔|✔|
|Use case|Async tasks|Cron / interval|

---

## 🔥 One-Line Summary

> `@Async` = **run method in another thread without blocking caller**