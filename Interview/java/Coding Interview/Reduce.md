```java
// INTERVIEW QUESTION (Single Task) - JAVA VERSION

/****************************
 * PROBLEM
 ****************************/

// You are given a list of transactions.
// Each transaction has:
// - id (int)
// - amount (double)
// - type: "credit" or "debit"

// Expected result for example data:
// 100 - 50 + 200 - 30 = 220

/****************************
 * REQUIREMENTS
 ****************************/

// 1. First solve using a loop
// 2. Then solve using streams (reduce)
// 3. Handle invalid input safely

import java.util.*;

class Transaction {
    int id;
    double amount;
    String type;

    Transaction(int id, double amount, String type) {
        this.id = id;
        this.amount = amount;
        this.type = type;
    }
}

public class Main {

    public static double getBalanceLoop(List<Transaction> transactions) {
        if (transactions == null) return 0;

        double balance = 0;
        for (Transaction t : transactions) {
            if (t == null || t.type == null) continue;

            if (t.type.equals("credit")) {
                balance += t.amount;
            } else if (t.type.equals("debit")) {
                balance -= t.amount;
            }
        }
        return balance;
    }

    public static double getBalanceReduce(List<Transaction> transactions) {
        if (transactions == null) return 0;

        return transactions.stream()
                .filter(Objects::nonNull)
                .reduce(0.0,
                        (acc, t) -> {
                            if (t.type == null) return acc;
                            if (t.type.equals("credit")) return acc + t.amount;
                            if (t.type.equals("debit")) return acc - t.amount;
                            return acc;
                        },
                        Double::sum);
    }

    public static void main(String[] args) {
        List<Transaction> transactions = Arrays.asList(
                new Transaction(1, 100, "credit"),
                new Transaction(2, 50, "debit"),
                new Transaction(3, 200, "credit"),
                new Transaction(4, 30, "debit")
        );

        System.out.println(getBalanceLoop(transactions));
        System.out.println(getBalanceReduce(transactions));
    }
}
```

## Reduce
```java
## 🔹 1. Two-argument version (simpler)

reduce(identity, accumulator)

- `identity` → starting value
- `accumulator` → how to combine values

Used when:  
👉 working with **same type** (e.g., `int → int`, `double → double`)

---

## 🔹 2. Three-argument version (what you saw)

reduce(identity, accumulator, combiner)

- `identity` → starting value
- `accumulator` → processes each element
- `combiner` → merges results (important for parallel streams)

---

## 🧠 Why 3 arguments exist

Because Java streams can run in **parallel**.

So:

- different threads compute partial results
- `combiner` merges them

---

## 🔴 Important for YOU right now

In your code:

.reduce(0.0, (acc, t) -> ..., Double::sum);

👉 That third argument (`Double::sum`) is **not really needed** for simple cases.

You could use the simpler version.

---

## 🧠 Mental model

- 2 args → “just accumulate”
- 3 args → “accumulate + combine parallel results”

---

## 🔥 Interview tip

If they ask about `reduce()`:

Say:

> “Java has 2 versions. The 3-arg version is mainly for parallel streams.”

That’s a strong answer.
//in two args use map() to return double what we need as acc 0.0(this is important)
    public static double getBalanceReduceTwoArgs(List<Transaction> transactions) {

        if (transactions == null) return 0;

        return transactions.stream()
                .filter(Objects::nonNull)
                .map(t -> {
                    if (t.type == null) return 0.0;
                    if (t.type.equals("credit")) return t.amount;
                    if (t.type.equals("debit")) return -t.amount;
                    return 0.0;
                })
                .reduce(0.0, (acc, val) -> acc + val);
    }  
    
    
```

---
- ❌ No external variable mutation inside streams
- ✅ Proper use of `acc` (accumulator)
- ❌ No `continue` inside lambdas
- ❌ No typos (`tansactions`, `equlas`, etc.)
- ✅ Correct 2-arg and 3-arg `reduce()` usage