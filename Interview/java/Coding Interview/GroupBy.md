```java
// INTERVIEW QUESTION (GROUPING + FILTERING) - JAVA

/****************************
 * PROBLEM
 ****************************/

// You are given a list of transactions.
// Each transaction has:
// - id (int)
// - amount (double)
// - type: "credit" or "debit"

// Example:
// [
//  {1, 100, "credit"},
//  {2, 50, "debit"},
//  {3, 200, "credit"},
//  {4, 30, "debit"}
// ]

/****************************
 * TASK
 ****************************/

// 1. Group transactions by type (credit / debit)
// 2. For each group, calculate the TOTAL amount

// Expected output (conceptually):
// {
//   "credit": 300,
//   "debit": 80
// }

/****************************
 * REQUIREMENTS
 ****************************/

// 1. First solve using loop
// 2. Then solve using streams (groupingBy)
// 3. Ignore null transactions or null types

import java.util.*;
import java.util.stream.*;

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

    /****************************
     * YOUR CODE HERE
     ****************************/

    public static Map<String, Double> groupBalanceLoop(List<Transaction> transactions) {
        if (transactions == null) return new HashMap<>();

        Map<String, Double> result = new HashMap<>();

        for (Transaction tra : transactions) {
            if (tra == null || tra.type == null) continue; // skip invalid

            // accumulate instead of overwrite
            result.put(tra.type, result.getOrDefault(tra.type, 0.0) + tra.amount);
        }

        return result;
    }

    public static Map<String, Double> groupBalanceStream(List<Transaction> transactions) {
        if (transactions == null) return new HashMap<>();

        return transactions.stream()
                .filter(Objects::nonNull)
                .filter(t -> t.type != null)
                .collect(Collectors.groupingBy(
                        t -> t.type,
                        Collectors.summingDouble(t -> t.amount)
                ));
    }

    public static void main(String[] args) {
        List<Transaction> transactions = Arrays.asList(
                new Transaction(1, 100, "credit"),
                new Transaction(2, 50, "debit"),
                new Transaction(3, 200, "credit"),
                new Transaction(4, 30, "debit")
        );

        System.out.println(groupBalanceLoop(transactions));
        System.out.println(groupBalanceStream(transactions));
    }
}

```