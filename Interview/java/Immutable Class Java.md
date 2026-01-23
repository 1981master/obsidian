[Skip to content](https://chatgpt.com/c/6973e355-610c-8333-b873-719f88153ab8#main)

## Chat history

[](https://chatgpt.com/)

##### You said:

how do you make class immutable java

###### ChatGPT said:

Making a class **immutable** in Java means creating a class whose instances **cannot be modified after they are created**. This is very useful for thread safety, caching, and predictable behavior. Let me break it down clearly with steps and examples.

---

## **Rules to Make a Class Immutable**

1. **Declare the class as `final` (optional but recommended)**
    
    - Prevents other classes from extending it and modifying behavior.
        
    
    `public final class Person { ... }`
    
2. **Make all fields `private` and `final`**
    
    - `private` prevents external access
        
    - `final` ensures fields are assigned once and never change
        
    
    `private final String name; private final int age;`
    
3. **Initialize all fields via a constructor**
    
    - Provide all values when creating an instance
        
    
    `public Person(String name, int age) {     this.name = name;     this.age = age; }`
    
4. **Do not provide setter methods**
    
    - Only provide **getter** methods for accessing values.
        
5. **Make deep copies of mutable objects**
    
    - If your class has fields that are mutable (like `Date`, arrays, collections), return **copies** instead of references.
        
    
    `private final Date birthDate;  public Person(String name, int age, Date birthDate) {     this.name = name;     this.age = age;     this.birthDate = new Date(birthDate.getTime()); // defensive copy }  public Date getBirthDate() {     return new Date(birthDate.getTime()); // return copy }`
    
6. **Avoid methods that modify the object**
    
    - Methods should only return new objects or computed values, never change internal state.
        

---

## **Example of a Fully Immutable Class**

`import java.util.Date;  public final class Person {     private final String name;     private final int age;     private final Date birthDate;      public Person(String name, int age, Date birthDate) {         this.name = name;         this.age = age;         this.birthDate = new Date(birthDate.getTime()); // defensive copy     }      public String getName() {         return name;     }      public int getAge() {         return age;     }      public Date getBirthDate() {         return new Date(birthDate.getTime()); // defensive copy     }      @Override     public String toString() {         return "Person{name='" + name + "', age=" + age + ", birthDate=" + birthDate + '}';     } }`

---

✅ **Key Points:**

- Immutable objects are **thread-safe** by default.
    
- Avoid exposing **mutable internal fields** directly.
    
- If the object has only **primitive types or Strings**, step 5 is not needed because Strings are already immutable.
    

---

If you want, I can also show a **shortcut for immutable classes using `record` in Java 16+**, which automatically handles all these rules.

Do you want me to show that version too?

ChatGPT can make mistakes. Check important info.