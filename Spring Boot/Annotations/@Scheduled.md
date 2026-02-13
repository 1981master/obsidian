### 🔹 What is `@Scheduled` (Spring)?

`@Scheduled` is used to **run tasks automatically on a schedule**—like a cron job—without manually triggering the method.

It’s great for:

- Periodic reports
    
- Cleaning temp files
    
- Sending reminder emails
    
- Polling APIs
    

---

## ✅ Enable Scheduling

`@Configuration @EnableScheduling public class SchedulerConfig { }`

---

## 🔹 Simple Examples

### 1️⃣ Fixed Rate (runs every 5 seconds, **regardless of task duration**)

```java
@Component
public class MyTask {

    @Scheduled(fixedRate = 5000)
    public void runEvery5Seconds() {
        System.out.println("Fixed Rate Task - " + System.currentTimeMillis());
    }
}

```

---

### 2️⃣ Fixed Delay (waits **after previous execution completes**)

```java
@Scheduled(fixedDelay = 5000)
public void runAfterPrevious() {
    System.out.println("Fixed Delay Task - " + System.currentTimeMillis());
}

```

---

### 3️⃣ Initial Delay + Fixed Rate

```java
@Scheduled(initialDelay = 2000, fixedRate = 5000)
public void delayedStart() {
    System.out.println("Starts after 2s, then every 5s");
}

```

---

### 4️⃣ Cron Expression (powerful schedule)

```java
@Scheduled(cron = "0 0 9 * * ?")
public void runDailyAt9AM() {
    System.out.println("Daily task at 9 AM");
}

```

**Cron format:**

`second minute hour day-of-month month day-of-week`

That’s the **Spring (and general Cron) time format** used in `@Scheduled(cron = "...")`. Here’s the breakdown:

|Field|Allowed Values|Description|
|---|---|---|
|**second**|0–59|The second at which the task runs|
|**minute**|0–59|The minute at which the task runs|
|**hour**|0–23|The hour of the day|
|**day-of-month**|1–31|The day of the month|
|**month**|1–12 or JAN–DEC|Month|
|**day-of-week**|0–7 or SUN–SAT (0 and 7 both = SUN)|Day of the week|

---

### 🔹 Special Characters

|Character|Meaning|
|---|---|
|`*`|Any value (every)|
|`?`|No specific value (used in day-of-month or day-of-week)|
|`,`|Value list (e.g., `MON,WED,FRI`)|
|`-`|Range (e.g., `1-5`)|
|`/`|Increment (e.g., `0/5` = every 5 units)|

---

### 🔹 Example Cron Expressions

|Expression|Meaning|
|---|---|
|`0 0 9 * * ?`|Every day at 9:00:00 AM|
|`0 0/15 8-17 * * MON-FRI`|Every 15 minutes between 8 AM – 5 PM, Mon–Fri|
|`0 0 0 1 1 ?`|Every Jan 1st at 12:00 AM|
|`0 0 12 ? * WED`|Every Wednesday at 12:00 PM|

---

## 🔹 Notes / Best Practices

- Can be combined with `@Async` for **non-blocking scheduled tasks**.
    
- Method must be `public` or `protected`.
    
- Scheduling runs **in a separate thread managed by Spring**.