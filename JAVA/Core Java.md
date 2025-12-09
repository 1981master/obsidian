# 🏛 Core Java

This note focuses on **Solidifying Core Java** concepts with common **interview questions and answers**.

---

## 1. OOP Concepts

### Q1: What is Object-Oriented Programming (OOP)?
**A:** OOP is a programming paradigm that organizes code around **objects** instead of functions or logic. Objects encapsulate **data (fields)** and **behavior (methods)**.

### Q2: What are the four main principles of OOP?
**A:**  
1. **Encapsulation** – Hiding internal state and requiring all interaction via methods.  
2. **Abstraction** – Exposing only relevant details and hiding complexity.  
3. **Inheritance** – Reusing code by creating child classes from parent classes.  
4. **Polymorphism** – Ability for objects to take multiple forms, e.g., method overriding.

### Q3: Difference between abstraction and encapsulation?
- **Encapsulation:** Hides internal data using `private` fields and provides access via getters/setters.  
- **Abstraction:** Hides implementation details using abstract classes or interfaces.

---

## 2. Java Memory Model

### Q1: What are the main memory areas in Java?
**A:**  
- **Heap:** Stores objects and class instances.  
- **Stack:** Stores local variables and method call frames.  
- **Method Area:** Stores class structures and static variables.  
- **PC Register:** Holds the current instruction address.  

### Q2: What is Garbage Collection in Java?
**A:** Automatic process of reclaiming memory by removing objects that are **no longer reachable**.

### Q3: Difference between Stack and Heap?
- **Stack:** Fast, stores primitives & references, memory automatically managed, method-scoped.  
- **Heap:** Slower, stores objects, managed by Garbage Collector, accessible globally.

---

## 3. Collections Framework

### Q1: What are the main interfaces in Java Collections?
**A:** `List`, `Set`, `Map`, `Queue`, `Deque`.

### Q2: Difference between `ArrayList` and `LinkedList`?
- **ArrayList:** Resizable array, fast random access, slow insert/delete in middle.  
- **LinkedList:** Doubly-linked nodes, fast insert/delete, slower random access.

### Q3: Difference between `HashMap` and `TreeMap`?
- **HashMap:** Unordered, fast lookup, allows one null key.  
- **TreeMap:** Ordered (sorted by keys), slower, no null key allowed.

---

## 4. Generics & Type Safety

### Q1: What are Generics in Java?
**A:** Mechanism to ensure **type safety at compile time** by allowing classes, interfaces, and methods to operate on specified types.

### Q2: Why use Generics?
- Prevent **ClassCastException** at runtime.  
- Eliminate explicit casting.  
- Increase code **reusability**.

### Q3: Difference between `<?>`, `<T>`, and `<T extends Class>`?
- `<?>` – Unbounded wildcard, any type.  
- `<T>` – Generic type parameter.  
- `<T extends Class>` – Bounded type parameter, restricts T to be a subclass of Class.

---

## 5. Concurrency Basics

### Q1: What is a thread in Java?
**A:** A thread is the **smallest unit of execution** in Java. Each Java application has at least one main thread.

### Q2: Difference between `Runnable` and `Thread`?
- `Runnable` – Defines **task to run**. Can be executed by multiple threads.  
- `Thread` – Represents a **thread of execution**, can implement Runnable or extend Thread class.

### Q3: What is `synchronized` in Java?
**A:** A keyword that ensures **only one thread can execute a method or block at a time** to prevent race conditions.

### Q4: What is `volatile`?
**A:** Ensures that **updates to a variable are visible across threads** immediately. Prevents threads from caching the variable locally.

---

> ✅ **Tip:** Review each concept by writing small code examples in Java. Practice implementing Collections, OOP patterns, and multithreaded programs.
