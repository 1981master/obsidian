```typescript
/******************************************************************
COMMON UTILITY TYPES USED IN REAL PROJECTS
******************************************************************/

type User = {
    id: number;
    name: string;
    email?: string;
};


/* ================================================================
1) Required<T>
Make all properties required
================================================================ */

type RequiredUser = Required<User>;

/*
email becomes required
*/


/* ================================================================
2) Readonly<T>
Prevent property modification
================================================================ */

type ReadonlyUser = Readonly<User>;

const user: ReadonlyUser = {
    id: 1,
    name: "Mohammed"
};

// user.name = "Ali"; ❌ Error


/* ================================================================
3) Exclude<T, U>
Remove types from a union
================================================================ */

type Role = "admin" | "user" | "guest";

type WithoutGuest = Exclude<Role, "guest">;
// "admin" | "user"


/* ================================================================
4) Extract<T, U>
Keep only matching types
================================================================ */

type OnlyAdmin = Extract<Role, "admin" | "moderator">;
// "admin"


/* ================================================================
5) NonNullable<T>
Remove null and undefined
================================================================ */

type MaybeString = string | null | undefined;

type SafeString = NonNullable<MaybeString>;
// string


/* ================================================================
6) ReturnType<T>
Get function return type
================================================================ */

function getUser() {
    return { id: 1, name: "Mohammed" };
}

type GetUserReturn = ReturnType<typeof getUser>;

/*
{ id: number; name: string }
*/


/* ================================================================
7) Parameters<T>
Get function parameter types as tuple
================================================================ */

function login(username: string, password: string) {}

type LoginParams = Parameters<typeof login>;
// [string, string]


/******************************************************************
REAL WORLD USE

✔ API response typing
✔ Redux actions
✔ React props transformations
✔ DTO transformations
✔ Backend service typing

These utilities prevent rewriting types manually.
******************************************************************/

```