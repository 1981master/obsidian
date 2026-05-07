```javascript
// PRACTICE: FREQUENCY COUNT (Simple)

/****************************
 * PROBLEM
 ****************************/

// Given an array of values, count how many times each value appears.

// Example:
// input: ["a", "b", "a", "c", "b", "a"]
// output:
// {
//   a: 3,
//   b: 2,
//   c: 1
// }

/****************************
 * REQUIREMENTS
 ****************************/

// 1) First solve using a loop
// 2) Then solve using reduce()
// 3) Return an object with counts

/****************************
 * YOUR CODE HERE
 ****************************/

function countFreqLoop(arr) {
  if(!Array.isArray(arr)) return {};

  let map = {};

  for(let i of arr){
    //in java I can use putOrDefault to count frequency
    //in JS we simulate it like this:
    map[i] = (map[i] || 0) + 1;
  }

  return map;
}

function countFreqReduce(arr) {
  if(!Array.isArray(arr)) return {};

  return arr.reduce((acc, curr) => {
    acc[curr] = (acc[curr] || 0) + 1;
    return acc;
  }, {});
}

/****************************
 * TEST
 ****************************/

const data = ["a", "b", "a", "c", "b", "a"];

console.log(countFreqLoop(data));
console.log(countFreqReduce(data));

```