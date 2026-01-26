## **1️⃣ Normal Bean (Plain Java Bean / POJO)**

A “normal bean” usually refers to a **simple Java object**, often following the JavaBean conventions:

`public class Person {     private String name;     private int age;      public Person() {} // no-arg constructor      public String getName() { return name; }     public void setName(String name) { this.name = name; }      public int getAge() { return age; }     public void setAge(int age) { this.age = age; } }`

**Characteristics:**

|Feature|Normal Bean|
|---|---|
|Lifecycle|Managed by the developer (you create with `new Person()`)|
|Dependencies|You manually inject dependencies (e.g., `person.setAddress(addr)`)|
|Scope|No concept of singleton/prototype automatically|
|Configuration|Hardcoded or passed via constructor/setters|
|Features|None from Spring (no AOP, no DI, no lifecycle hooks)|

**Usage:**  
You just instantiate it when needed:

`Person p = new Person(); p.setName("John");`

---

## **2️⃣ Spring Bean**

A **Spring bean** is any object that **Spring IoC container manages**. You don’t create it manually; Spring instantiates, wires dependencies, and manages its lifecycle.

`@Component // tells Spring to manage this class public class Person {     private String name;      @Autowired // dependency injected automatically     private Address address;      public Person() {}      @PostConstruct // runs after bean creation     public void init() {         System.out.println("Bean initialized");     } }`

**Characteristics:**

|Feature|Spring Bean|
|---|---|
|Lifecycle|Managed by Spring container|
|Dependencies|Automatically injected using DI (`@Autowired`, constructor injection, etc.)|
|Scope|Can be `singleton`, `prototype`, `request`, `session` etc.|
|Configuration|Can be XML, Java `@Configuration`, or annotations (`@Component`, `@Bean`)|
|Features|Lifecycle callbacks (`@PostConstruct`, `@PreDestroy`), AOP, proxying, event handling|
|Access|Can be retrieved from Spring context: `context.getBean(Person.class)`|

**Example using Java Config:**

`@Configuration public class AppConfig {     @Bean     public Person person() {         return new Person();     } }`

Now Spring creates the bean for you and manages it.

---

## **3️⃣ Key Differences**

|Aspect|Normal Bean|Spring Bean|
|---|---|---|
|Creation|Using `new` keyword|Created by Spring container|
|Dependencies|Manually set|Injected automatically (DI)|
|Lifecycle|You control|Spring controls (init, destroy)|
|Scope|Only what you create|Singleton by default, can be prototype, etc.|
|Features|None|AOP, events, lifecycle methods, proxies|
|Configuration|Hardcoded or via setters|XML, Java Config, or annotations|
|Management|Developer responsibility|Spring container responsibility|

---

✅ **In short:**

- **Normal bean:** just a plain Java object you manage yourself.
    
- **Spring bean:** an object managed by Spring, with dependency injection, lifecycle, and extra Spring features.