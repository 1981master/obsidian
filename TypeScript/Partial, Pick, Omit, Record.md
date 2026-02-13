```typescript
/******************************************************************
ADVANCED TYPES — Partial, Pick, Omit, Record
These are built-in utility types used to transform existing types.
******************************************************************/

/* ================================================================
BASE TYPE
================================================================ */

type User = {
    id: number;
    name: string;
    email: string;
    isAdmin: boolean;
};


/* ================================================================
1) Partial<T>
Makes all properties optional
================================================================ */

type PartialUser = Partial<User>;

/*
Equivalent to:

type PartialUser = {
    id?: number;
    name?: string;
    email?: string;
    isAdmin?: boolean;
}
*/

const updateUser = (user: Partial<User>) => {
    console.log(user);
};

updateUser({ name: "Mohammed" }); // valid


/* ================================================================
2) Pick<T, Keys>
Select specific properties from a type
================================================================ */

type UserPreview = Pick<User, "id" | "name">;

/*
Equivalent to:

{
    id: number;
    name: string;
}
*/

const preview: UserPreview = {
    id: 1,
    name: "Mohammed"
};


/* ================================================================
3) Omit<T, Keys>
Remove properties from a type
================================================================ */

type UserWithoutEmail = Omit<User, "email">;

/*
Equivalent to:

{
    id: number;
    name: string;
    isAdmin: boolean;
}
*/


/* ================================================================
4) Record<KeyType, ValueType>
Create an object type with specific key/value types
================================================================ */

type Role = "admin" | "user" | "guest";

type RolePermissions = Record<Role, boolean>;

/*
Equivalent to:

{
    admin: boolean;
    user: boolean;
    guest: boolean;
}
*/

const permissions: RolePermissions = {
    admin: true,
    user: false,
    guest: false
};


/******************************************************************
MENTAL MODEL

Partial<T>  → Make everything optional
Pick<T>     → Select fields
Omit<T>     → Remove fields
Record<K,V> → Build object with keys K and values V

These are used everywhere in real apps.
******************************************************************/

```