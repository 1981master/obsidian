```java
interface Payment {
    void pay(long amount);
}


public enum Level implements Payment {

    LOW(3L, "low", "show") {
        @Override
        public void pay(long amount) {
            process(amount);
        }
    },

    MEDIUM(2L, "medium", "show") {
        @Override
        public void pay(long amount) {
            process(amount * 2);
        }
    },

    HIGH(1L, "high", "hide") {
        @Override
        public void pay(long amount) {
            process(amount * 3);
        }
    };

    // private fields
    private final Long priority;
    private final String label;
    private final String visibility;

    // private constructor
    private Level(Long priority, String label, String visibility) {
        this.priority = priority;
        this.label = label;
        this.visibility = visibility;
    }

    // private method
    private void process(long amount) {
        System.out.println(
            name() + " | priority=" + priority +
            " | label=" + label +
            " | visibility=" + visibility +
            " | amount=" + amount
        );
    }

    // public methods
    public Long getPriority() {
        return priority;
    }

    public String getLabel() {
        return label;
    }
}


**Usage:**
public class EnumClient {

    public static void main(String[] args) {

        Level level = Level.LOW;

        level.pay(100);

        Level.valueOf("HIGH").pay(200);

        for (Level l : Level.values()) {
            l.pay(50);
        } 
        //for just low and high:
        for (Level l : new Level[]{Level.LOW, Level.HIGH}) {
		    l.pay(50);
		}
		//OR:
		EnumSet.of(Level.LOW, Level.HIGH)
       .forEach(l -> l.pay(50));
		//OR
		for (Level l : Level.values()) {
		    if (l != Level.MEDIUM) {
		        l.pay(50);
		    }
		}


    }
}

```

```text
### Key rule to remember

- `values()` **always returns all enum constants**
    
- Order = **exactly how they are declared**
```

---
---

## 🔹 Methods available on **every enum** (from `java.lang.Enum`)

`String name() int ordinal()  String toString()  boolean equals(Object o) int hashCode()  int compareTo(E other)  Class<E> getDeclaringClass()`

---

## 🔹 Static methods generated **per enum type**

`static E[] values() static E valueOf(String name)`

---

## 🔹 Methods inherited from `java.lang.Object`

```java
final Class<?> getClass() 
final void notify() 
final void notifyAll()
final void wait()
final void wait(long timeout)
final void wait(long timeout, int nanos)
final String toString()
```


---

## 🔹 Methods you can **override in enum**

`String toString()`

---

## 🔹 Methods you can **define yourself inside enum**

```java
// instance methods public void anyMethod() private void helper() 
// abstract methods (implemented per constant) abstract void execute();
// static methods public static Level fromCode(int code)
// getters public int getCode()
```


---

## 🔹 Special enum features (syntax-level)

`Enum.valueOf(Class<E> enumType, String name) EnumSet.allOf(Level.class) EnumMap<Level, String>`

---

## 🔹 Methods you CANNOT override

`name() ordinal() compareTo() equals() hashCode()`

---

## 🔹 Example usage summary

```java
Level.values() 
Level.valueOf("LOW")
level.name()
level.ordinal()
level.compareTo(Level.HIGH)
```


---
