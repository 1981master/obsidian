```typescript
/******************************************************************
REACT + TYPESCRIPT COMMON PATTERNS
******************************************************************/

import React, { useState } from "react";


/* ================================================================
1) Functional Component with Props
================================================================ */

type ButtonProps = {
    label: string;
    onClick: () => void;
};

const Button: React.FC<ButtonProps> = ({ label, onClick }) => {
    return <button onClick={onClick}>{label}</button>;
};


/* ================================================================
2) useState Typing
================================================================ */

// Inferred type
const [count, setCount] = useState(0);

// Explicit type
const [name, setName] = useState<string>("");

// Nullable state
const [user, setUser] = useState<User | null>(null);

type User = {
    id: number;
    name: string;
};


/* ================================================================
3) Event Typing
================================================================ */

const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    console.log(e.target.value);
};

const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
};


/* ================================================================
4) useRef Typing
================================================================ */

import { useRef } from "react";

const inputRef = useRef<HTMLInputElement>(null);

const focusInput = () => {
    inputRef.current?.focus();
};


/* ================================================================
5) Children Typing
================================================================ */

type CardProps = {
    children: React.ReactNode;
};

const Card = ({ children }: CardProps) => {
    return <div>{children}</div>;
};


/* ================================================================
6) Generic Component
================================================================ */

type ListProps<T> = {
    items: T[];
    render: (item: T) => React.ReactNode;
};

function List<T>({ items, render }: ListProps<T>) {
    return (
        <ul>
            {items.map((item, index) => (
                <li key={index}>{render(item)}</li>
            ))}
        </ul>
    );
}


/* ================================================================
7) API Fetch Pattern
================================================================ */

type ApiResponse<T> = {
    data: T;
    status: number;
};

async function fetchUser(): Promise<ApiResponse<User>> {
    const res = await fetch("/api/user");
    const data = await res.json();
    return { data, status: res.status };
}


/******************************************************************
MENTAL MODEL FOR REACT + TS

Props → always define a type
State → use generics in useState<T>()
Events → use React.Event types
API → use generics for reusable responses

React + TS = predictable UI + safer refactoring
******************************************************************/

```