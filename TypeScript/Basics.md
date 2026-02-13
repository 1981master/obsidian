```typescript
/******************************************************************
 JAVASCRIPT vs TYPESCRIPT — SIDE BY SIDE SYNTAX GUIDE
 Think of TypeScript = JavaScript + Static Types
******************************************************************/

/* ================================================================
1) BASIC VARIABLES
================================================================ */

// JavaScript
let name = "Mohammed";
let age = 25;
let isActive = true;

// TypeScript
let nameTS: string = "Mohammed";
let ageTS: number = 25;
let isActiveTS: boolean = true;

// Type Inference (TS auto-detects type)
let city = "New York"; // inferred as string


/* ================================================================
2) PRIMITIVE TYPES IN TYPESCRIPT
================================================================ */

let username: string;
let count: number;
let isLogged: boolean;
let data: any;        // avoid if possible
let safeData: unknown;
let nothing: void;
let neverValue: never;


/* ================================================================
3) FUNCTIONS
================================================================ */

// JavaScript
function add(a, b) {
    return a + b;
}

// TypeScript
function addTS(a: number, b: number): number {
    return a + b;
}

// Arrow Function

// JavaScript
const multiply = (a, b) => a * b;

// TypeScript
const multiplyTS = (a: number, b: number): number => a * b;


/* ================================================================
4) OPTIONAL & DEFAULT PARAMETERS
================================================================ */

function greet(name: string, age?: number): string {
    return age ? `${name} is ${age}` : name;
}

function greetDefault(name: string = "Guest"): string {
    return `Hello ${name}`;
}


/* ================================================================
5) ARRAYS
================================================================ */

// JavaScript
let numbers = [1, 2, 3];

// TypeScript (two ways)
let numbersTS: number[] = [1, 2, 3];
let numbersTS2: Array<number> = [1, 2, 3];


/* ================================================================
6) TUPLES (TypeScript Only)
================================================================ */

let userTuple: [string, number];
userTuple = ["Mohammed", 25];


/* ================================================================
7) OBJECTS
================================================================ */

// JavaScript
let user = {
    name: "Mohammed",
    age: 25
};

// TypeScript Inline Type
let userTS: { name: string; age: number } = {
    name: "Mohammed",
    age: 25
};


/* ================================================================
8) TYPE ALIAS
================================================================ */

type User = {
    name: string;
    age: number;
};

let user2: User = {
    name: "Mohammed",
    age: 25
};


/* ================================================================
9) INTERFACE
================================================================ */

interface Person {
    name: string;
    age: number;
}

let person: Person = {
    name: "Mohammed",
    age: 25
};


/* ================================================================
10) UNION TYPES
================================================================ */

let id: string | number;

id = 10;
id = "ABC123";


/* ================================================================
11) TYPE NARROWING
================================================================ */

function printId(id: string | number) {
    if (typeof id === "string") {
        console.log(id.toUpperCase());
    } else {
        console.log(id.toFixed(2));
    }
}


/* ================================================================
12) ENUMS (TypeScript Only)
================================================================ */

enum Role {
    ADMIN,
    USER,
    GUEST
}

let myRole: Role = Role.ADMIN;

// String Enum
enum RoleString {
    ADMIN = "ADMIN",
    USER = "USER"
}


/* ================================================================
13) CLASSES
================================================================ */

// JavaScript
class UserJS {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        return "Hello " + this.name;
    }
}

// TypeScript
class UserTS {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    greet(): string {
        return "Hello " + this.name;
    }
}


/* ================================================================
14) ACCESS MODIFIERS (TypeScript)
================================================================ */

class Account {
    public username: string;
    private password: string;
    protected id: number;

    constructor(username: string, password: string, id: number) {
        this.username = username;
        this.password = password;
        this.id = id;
    }
}


/* ================================================================
15) CONSTRUCTOR SHORTCUT (TypeScript Only)
================================================================ */

class Customer {
    constructor(
        public name: string,
        private age: number
    ) {}
}


/* ================================================================
16) GENERICS
================================================================ */

// Without Generics
function identityAny(value: any): any {
    return value;
}

// With Generics
function identity<T>(value: T): T {
    return value;
}

identity<string>("hello");
identity<number>(10);


/* ================================================================
17) GENERICS WITH ARRAYS
================================================================ */

function getFirst<T>(arr: T[]): T {
    return arr[0];
}


/* ================================================================
18) TYPE ASSERTION (Casting)
================================================================ */

let input = document.getElementById("name") as HTMLInputElement;
input.value = "Hello";

// Alternative syntax
let input2 = <HTMLInputElement>document.getElementById("name");


/* ================================================================
19) ANY vs UNKNOWN
================================================================ */

let valueAny: any = 10;
valueAny.toUpperCase(); // allowed (unsafe)

let valueUnknown: unknown = 10;
// valueUnknown.toUpperCase(); ❌ not allowed without checking


/* ================================================================
20) MODULES (Same as ES6)
================================================================ */

export class Product {}

import { Product } from "./Product";


/* ================================================================
21) JAVASCRIPT FEATURES THAT STAY THE SAME
================================================================ */

let arr = [1, 2, 3];

arr.map(x => x * 2);
arr.filter(x => x > 1);
arr.reduce((a, b) => a + b, 0);

let { name: userName } = user;
let copy = { ...user };

async function fetchData() {
    const res = await fetch("https://api.com");
    return res.json();
}


/******************************************************************
MENTAL MODEL

TypeScript =
JavaScript
+ Static Types
+ Interfaces
+ Enums
+ Generics
+ Access Modifiers
+ Compile-Time Checking

It compiles into pure JavaScript.
Browser only understands JavaScript.
******************************************************************/

```