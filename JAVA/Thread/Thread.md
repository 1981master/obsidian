### How to make two threads working sequentially
```java
class Printer {
    private boolean letterTurn = true; // true = letter's turn, false = number's turn

    public synchronized void printLetter(char c) throws InterruptedException {
        while (!letterTurn) {
            wait(); // wait if it's not letter's turn
        }
        System.out.print(c);
        letterTurn = false; // next is number
        notify(); // wake up number thread
    }

    public synchronized void printNumber(int n) throws InterruptedException {
        while (letterTurn) {
            wait(); // wait if it's not number's turn
        }
        System.out.print(n);
        letterTurn = true; // next is letter
        notify(); // wake up letter thread
    }
}

public class Main {
    public static void main(String[] args) {
        Printer printer = new Printer();

        Thread t1 = new Thread(() -> {
            char[] letters = {'a', 'b', 'c', 'd'};
            try {
                for (char c : letters) {
                    printer.printLetter(c);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        Thread t2 = new Thread(() -> {
            int[] numbers = {1, 2, 3, 4};
            try {
                for (int n : numbers) {
                    printer.printNumber(n);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        t1.start();
        t2.start();
    }
}

```