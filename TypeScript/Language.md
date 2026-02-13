```javascript
/******************************************************************
DECLARATIVE vs IMPERATIVE vs VERBOSE
Simple Meaning + Examples
******************************************************************/

/* ================================================================
1️⃣ IMPERATIVE
================================================================ */

/*
You tell the computer STEP BY STEP how to do something.
You control the flow manually.

Think:
"HOW to do it"
*/

const numbers = [1, 2, 3, 4, 5];

let doubledImperative: number[] = [];

for (let i = 0; i < numbers.length; i++) {
    doubledImperative.push(numbers[i] * 2);
}

console.log(doubledImperative);

/*
We manually:
- create array
- loop
- push
- control index

Very explicit.
*/


/* ================================================================
2️⃣ DECLARATIVE
================================================================ */

/*
You describe WHAT you want.
The system handles HOW.

Think:
"WHAT result I want"
*/

const doubledDeclarative = numbers.map(n => n * 2);

console.log(doubledDeclarative);

/*
We don’t manage:
- loop
- index
- push

We just say:
"Give me numbers doubled"

React is DECLARATIVE:
*/

type Props = { count: number };

const Counter = ({ count }: Props) => {
    return <h1>{count}</h1>;
};

/*
We describe:
"When count changes, show it."

We do NOT manually:
- find DOM
- update text
- re-render
React handles that.
*/


/* ================================================================
3️⃣ VERBOSE
================================================================ */

/*
Verbose = More words / more code than necessary.

Not about logic style.
It means "too detailed" or "long".
*/

function addVerbose(a: number, b: number): number {
    let result = a + b;
    return result;
}

const addShort = (a: number, b: number) => a + b;

/*
Both work the same.
First is more VERBOSE.
Second is concise.
*/


/* ================================================================
QUICK SUMMARY
================================================================ */

/*
IMPERATIVE:
→ How to do it step-by-step
→ Manual control
→ for loops, mutation, DOM manipulation

DECLARATIVE:
→ What you want
→ System handles details
→ map(), filter(), React UI

VERBOSE:
→ Too much unnecessary code
→ Long / overly detailed


MENTAL MODEL:

Imperative = Instructions
Declarative = Description
Verbose = Wordy
******************************************************************/
/******************************************************************
PROGRAMMING LANGUAGE TYPES — INTERVIEW MASTER CHEAT SHEET
What they mean + Examples
******************************************************************/

/* ================================================================
1️⃣ IMPERATIVE PROGRAMMING
================================================================ */

/*
Definition:
You tell the computer HOW to do something step-by-step.

You control:
- Loops
- Conditions
- State changes
- Execution order

Focus: HOW

Examples:
C
C++
Java
JavaScript (can be imperative)
Python (can be imperative)
*/


/* ================================================================
2️⃣ DECLARATIVE PROGRAMMING
================================================================ */

/*
Definition:
You describe WHAT you want.
The system handles HOW internally.

Focus: WHAT

Examples:
SQL
HTML
CSS
React (UI description)
GraphQL
*/


/* ================================================================
3️⃣ PROCEDURAL PROGRAMMING
================================================================ */

/*
Definition:
A type of imperative programming organized around procedures/functions.

Focus:
Step-by-step instructions grouped into functions.

Examples:
C
Pascal
Early BASIC
*/


/* ================================================================
4️⃣ OBJECT-ORIENTED PROGRAMMING (OOP)
================================================================ */

/*
Definition:
Programming based on objects and classes.

Core concepts:
- Encapsulation
- Inheritance
- Polymorphism
- Abstraction

Examples:
Java
C++
C#
Python
TypeScript
*/


/* ================================================================
5️⃣ FUNCTIONAL PROGRAMMING
================================================================ */

/*
Definition:
Programming using pure functions and immutability.

Concepts:
- Pure functions
- No side effects
- Immutability
- Higher-order functions

Examples:
Haskell
Scala
Elixir
JavaScript (supports functional)
React (functional components)
*/


/* ================================================================
6️⃣ LOGIC PROGRAMMING
================================================================ */

/*
Definition:
Programming based on rules and logical relationships.

You define facts and rules, system solves queries.

Examples:
Prolog
Datalog
*/


/* ================================================================
7️⃣ SCRIPTING LANGUAGES
================================================================ */

/*
Definition:
Usually interpreted, used for automation or web scripting.

Examples:
JavaScript
Python
PHP
Bash
Ruby
*/


/* ================================================================
8️⃣ COMPILED vs INTERPRETED
================================================================ */

/*
Compiled:
Code converted to machine code before running.
Faster execution.

Examples:
C
C++
Rust
Go

Interpreted:
Executed line-by-line by interpreter.

Examples:
JavaScript
Python
PHP

Hybrid:
Java (compiled to bytecode, runs on JVM)
C# (.NET runtime)
TypeScript (compiled to JS)
*/


/* ================================================================
9️⃣ STATIC vs DYNAMIC TYPING
================================================================ */

/*
Static Typing:
Types checked at compile time.

Examples:
Java
C++
C#
TypeScript
Go

Dynamic Typing:
Types checked at runtime.

Examples:
JavaScript
Python
PHP
Ruby
*/


/* ================================================================
🔟 STRONG vs WEAK TYPING
================================================================ */

/*
Strongly Typed:
Strict type rules.
Less implicit conversion.

Examples:
Java
TypeScript
Python

Weakly Typed:
Allows implicit conversions easily.

Example:
JavaScript (5 + "5" → "55")
*/


/* ================================================================
1️⃣1️⃣ MULTI-PARADIGM LANGUAGES
================================================================ */

/*
Most modern languages support multiple paradigms.

JavaScript:
- Imperative
- Functional
- Object-Oriented

Python:
- Procedural
- OOP
- Functional

TypeScript:
- OOP
- Functional
- Static typing

Java:
- OOP
- Imperative
*/


/* ================================================================
INTERVIEW QUICK SUMMARY
================================================================ */

/*
Imperative → HOW to do it
Declarative → WHAT you want
Procedural → Imperative organized in functions
OOP → Objects & classes
Functional → Pure functions & immutability
Logic → Rules & facts
Compiled → Machine code first
Interpreted → Run line-by-line
Static typing → Types checked before run
Dynamic typing → Types checked at runtime
Strong typing → Strict rules
Weak typing → Implicit conversions

Most modern languages are multi-paradigm.
******************************************************************/

```