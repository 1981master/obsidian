```javascript
// INTERVIEW QUESTION (Single Task)

/****************************
 * PROBLEM
 ****************************/

// You are given an array of transactions.
// Each transaction has:
// - id (number)
// - amount (number)
// - type: "credit" or "debit"

// Example:
const transactions = [
  { id: 1, amount: 100, type: "credit" },
  { id: 2, amount: 50, type: "debit" },
  { id: 3, amount: 200, type: "credit" },
  { id: 4, amount: 30, type: "debit" }
];

/****************************
 * TASK
 ****************************/

// Write a function that returns the FINAL BALANCE.

// Rules:
// - "credit" adds money
// - "debit" subtracts money

// Expected result for above data:
// 100 - 50 + 200 - 30 = 220

/****************************
 * REQUIREMENTS
 ****************************/

// 1. First solve using for...of
// 2. Then solve using reduce()
// 3. Handle invalid input safely

/****************************
 * YOUR CODE HERE
 ****************************/

function getBalanceLoop(transactions) {
  if (!Array.isArray(transactions)) return 0;

  let balance = 0;
  for (let tran of transactions) {
    if (tran.type === 'credit') {
      balance += tran.amount;
    } else if (tran.type === 'debit') {
      balance -= tran.amount;
    }
  }

  return balance;
}

function getBalanceReduce(transactions) {
  if (!Array.isArray(transactions)) return 0;

  return transactions.reduce((acc, curr) => {
    if (curr.type === 'credit') {
      return acc + curr.amount;
    } else if (curr.type === 'debit') {
      return acc - curr.amount;
    }
    return acc;
  }, 0);
}

// Test your result
console.log(getBalanceLoop(transactions));
console.log(getBalanceReduce(transactions));

```