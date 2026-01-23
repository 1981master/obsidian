[Skip to content](https://chatgpt.com/c/6973e66a-4e58-8328-a355-0cd4af0c0102#main)

## Chat history

[](https://chatgpt.com/)

##### You said:

explain bean life cycle in springboot java

###### ChatGPT said:

Absolutely! Let’s go **step by step** and cover the **Spring Bean Life Cycle** in a **Spring Boot (or Spring) Java application**. I’ll make it clear and practical.

---

## **1️⃣ What is a Spring Bean?**

A **Bean** in Spring is an object that is **managed by the Spring IoC (Inversion of Control) container**.

- Beans are created, initialized, and destroyed by Spring according to the **bean life cycle**.
    
- Every Spring-managed bean goes through a well-defined life cycle.
    

---

## **2️⃣ Bean Life Cycle Phases**

The Spring Bean Life Cycle has **three main phases**:

### **A. Instantiation**

- Spring container **creates the bean instance** using the **constructor** or factory method.
    
- At this point, the bean is just an object; dependencies are not injected yet.
    

`@Component public class MyBean {     public MyBean() {         System.out.println("Bean instance created!");     } }`

---

### **B. Dependency Injection (Populate Properties)**

- Spring injects all **dependencies** (like `@Autowired` fields or `@Value` properties) into the bean.
    
- After this step, the bean is fully configured.
    

`@Component public class MyBean {     @Autowired     private SomeService service;      @Value("${app.name}")     private String appName; }`

---

### **C. Initialization**

- Spring provides **callbacks** before the bean is ready to use.
    
- You can hook into initialization in three main ways:
    

#### **1. Using `@PostConstruct`**

`@PostConstruct public void init() {     System.out.println("Bean is initialized using @PostConstruct"); }`

#### **2. Using `InitializingBean` Interface**

`@Component public class MyBean implements InitializingBean {     @Override     public void afterPropertiesSet() throws Exception {         System.out.println("Bean is initialized using afterPropertiesSet()");     } }`

#### **3. Using `init-method` in XML / `@Bean`**

`@Bean(initMethod = "customInit") public MyBean myBean() {     return new MyBean(); }  public void customInit() {     System.out.println("Custom init method called"); }`

> ✅ At this point, the bean is ready to use.

---

### **D. Bean in Use**

- The bean is now **active in the Spring container** and can be **injected anywhere**.
    

`@Autowired private MyBean myBean;`

---

### **E. Destruction**

- When the Spring container is **shutting down**, it **destroys singleton beans**.
    
- Destruction callbacks can be specified in three ways:
    

#### **1. Using `@PreDestroy`**

`@PreDestroy public void cleanup() {     System.out.println("Bean is being destroyed"); }`

#### **2. Using `DisposableBean` Interface**

`@Component public class MyBean implements DisposableBean {     @Override     public void destroy() throws Exception {         System.out.println("DisposableBean destroy method called");     } }`

#### **3. Using `destroy-method` in `@Bean`**

`@Bean(destroyMethod = "customDestroy") public MyBean myBean() {     return new MyBean(); }  public void customDestroy() {     System.out.println("Custom destroy method called"); }`

> ⚠️ Note: **Prototype scoped beans are not managed for destruction** by Spring.

---

## **3️⃣ Full Bean Life Cycle Flow**

Here’s a visual flow:

`Bean Instantiation → Dependency Injection → @PostConstruct / afterPropertiesSet / init-method → Bean Ready → Usage → @PreDestroy / DisposableBean / destroy-method → Bean Destroyed`

---

## **4️⃣ Bean Scopes & Life Cycle**

- **Singleton** (default) → Spring manages entire life cycle including destruction.
    
- **Prototype** → Spring creates new instance per request, initialization callbacks are called, but destruction is **not managed**.
    

---

## **5️⃣ Practical Example**

`@Component public class MyBean implements InitializingBean, DisposableBean {      public MyBean() {         System.out.println("Bean instance created");     }      @PostConstruct     public void postConstruct() {         System.out.println("@PostConstruct called");     }      @Override     public void afterPropertiesSet() throws Exception {         System.out.println("afterPropertiesSet called");     }      @PreDestroy     public void preDestroy() {         System.out.println("@PreDestroy called");     }      @Override     public void destroy() throws Exception {         System.out.println("DisposableBean destroy called");     } }`

**Output on application start:**

`Bean instance created @PostConstruct called afterPropertiesSet called`

**Output on application shutdown:**

`@PreDestroy called DisposableBean destroy called`

---

### ✅ **Key Takeaways**

1. Beans are **managed by Spring**, not manually created.
    
2. Initialization can be done using:
    
    - `@PostConstruct`
        
    - `InitializingBean`
        
    - `init-method`
        
3. Destruction can be done using:
    
    - `@PreDestroy`
        
    - `DisposableBean`
        
    - `destroy-method`
        
4. Singleton beans → full life cycle, Prototype beans → only initialization.
    

---

If you want, I can also make a **diagram showing the Spring Bean Life Cycle with all hooks**. It’s very helpful for interviews and understanding.

Do you want me to make that diagram?

ChatGPT can make mistakes. Check important info.