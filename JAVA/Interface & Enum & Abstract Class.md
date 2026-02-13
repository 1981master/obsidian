
`when tow or more interfaces has same default method name and signture:`
```java
interface InterfaceA {
    default void display() {
        System.out.println("InterfaceA display");
    }
}

interface InterfaceB {
    default void display() {
        System.out.println("InterfaceB display");
    }
}

public class MyClass implements InterfaceA, InterfaceB {
    @Override
    public void display() {
        // Explicitly choosing which default method to use, or providing a custom implementation
        InterfaceA.super.display();
        // or InterfaceB.super.display();
    }
}


```