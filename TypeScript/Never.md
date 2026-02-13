```typescript
/******************************************************************
NEVER TYPE — PRACTICAL EXAMPLES
******************************************************************/

/* ================================================================
1) Function That Always Throws
================================================================ */

function throwError(message: string): never {
    throw new Error(message);
}

// This function NEVER returns a value.
// Execution stops immediately.


/* ================================================================
2) Infinite Loop
================================================================ */

function infiniteLoop(): never {
    while (true) {
        console.log("Running...");
    }
}

// This function never finishes.
// It never reaches the end.


/* ================================================================
3) Type Narrowing With Exhaustive Check (VERY IMPORTANT)
================================================================ */

type Shape =
    | { kind: "circle"; radius: number }
    | { kind: "square"; size: number };

function getArea(shape: Shape): number {
    switch (shape.kind) {
        case "circle":
            return Math.PI * shape.radius * shape.radius;

        case "square":
            return shape.size * shape.size;

        default:
            const _exhaustiveCheck: never = shape;
            return _exhaustiveCheck;
    }
}

/*
Why this is powerful:

If you later add:

| { kind: "triangle"; base: number; height: number }

TypeScript will ERROR at:

const _exhaustiveCheck: never = shape;

Because shape is no longer "never".
This forces you to handle all cases.
*/


/* ================================================================
4) never in Union (Impossible Value)
================================================================ */

let value: string & number; 
// This becomes NEVER because a value can't be both string and number.


/* ================================================================
5) never in Conditional Types
================================================================ */

type OnlyString<T> = T extends string ? T : never;

type A = OnlyString<string>;  // string
type B = OnlyString<number>;  // never


/******************************************************************
MENTAL MODEL

never means:
- This code path is impossible
- This function never returns
- This type should not exist

If TypeScript infers "never", it usually means:
"You logically reached an impossible state."
******************************************************************/

```