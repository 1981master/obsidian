- ✅ Props → define a type
    
- ✅ State → use generics in `useState<T>()`
    
- ✅ Events → use `React.Event` types
    
- ✅ API → use generics for reusable responses
---
```typescript
/******************************************************************
REAL-WORLD REACT + TYPESCRIPT EXAMPLE
Simple User List with Add Form + API Fetch
******************************************************************/

import React, { useEffect, useState } from "react";

/* ================================================================
1️⃣ API GENERIC RESPONSE TYPE
Reusable API wrapper type
================================================================ */

type ApiResponse<T> = {
    data: T;
    message: string;
    status: number;
};

/* ================================================================
2️⃣ DOMAIN MODEL TYPE
================================================================ */

type User = {
    id: number;
    name: string;
    email: string;
};

/* ================================================================
3️⃣ COMPONENT PROPS (Always define a type)
================================================================ */

type UserCardProps = {
    user: User;
    onDelete: (id: number) => void;
};

/* ================================================================
4️⃣ CHILD COMPONENT
================================================================ */

const UserCard: React.FC<UserCardProps> = ({ user, onDelete }) => {
    return (
        <div style={{ border: "1px solid gray", padding: 10, margin: 5 }}>
            <h4>{user.name}</h4>
            <p>{user.email}</p>
            <button onClick={() => onDelete(user.id)}>Delete</button>
        </div>
    );
};

/* ================================================================
5️⃣ MAIN COMPONENT
================================================================ */

const UserDashboard: React.FC = () => {

    /* ------------------------------------------------------------
    STATE (Use Generics in useState<T>())
    ------------------------------------------------------------ */

    const [users, setUsers] = useState<User[]>([]);
    const [name, setName] = useState<string>("");
    const [email, setEmail] = useState<string>("");
    const [loading, setLoading] = useState<boolean>(false);


    /* ------------------------------------------------------------
    API CALL (Using Generic ApiResponse<T>)
    ------------------------------------------------------------ */

    const fetchUsers = async (): Promise<void> => {
        setLoading(true);

        const res = await fetch("/api/users");
        const result: ApiResponse<User[]> = await res.json();

        setUsers(result.data);
        setLoading(false);
    };

    useEffect(() => {
        fetchUsers();
    }, []);


    /* ------------------------------------------------------------
    EVENTS (Use React Event Types)
    ------------------------------------------------------------ */

    const handleNameChange = (
        e: React.ChangeEvent<HTMLInputElement>
    ): void => {
        setName(e.target.value);
    };

    const handleEmailChange = (
        e: React.ChangeEvent<HTMLInputElement>
    ): void => {
        setEmail(e.target.value);
    };

    const handleSubmit = async (
        e: React.FormEvent<HTMLFormElement>
    ): Promise<void> => {
        e.preventDefault();

        const newUser: User = {
            id: Date.now(),
            name,
            email
        };

        // Fake POST
        setUsers(prev => [...prev, newUser]);

        setName("");
        setEmail("");
    };


    /* ------------------------------------------------------------
    DELETE HANDLER (Typed Function)
    ------------------------------------------------------------ */

    const handleDelete = (id: number): void => {
        setUsers(prev => prev.filter(user => user.id !== id));
    };


    /* ------------------------------------------------------------
    UI
    ------------------------------------------------------------ */

    return (
        <div style={{ maxWidth: 500, margin: "auto" }}>
            <h2>User Dashboard</h2>

            {/* Form */}
            <form onSubmit={handleSubmit}>
                <input
                    type="text"
                    placeholder="Name"
                    value={name}
                    onChange={handleNameChange}
                />
                <input
                    type="email"
                    placeholder="Email"
                    value={email}
                    onChange={handleEmailChange}
                />
                <button type="submit">Add User</button>
            </form>

            <hr />

            {loading && <p>Loading...</p>}

            {users.map(user => (
                <UserCard
                    key={user.id}
                    user={user}
                    onDelete={handleDelete}
                />
            ))}
        </div>
    );
};

export default UserDashboard;


/******************************************************************
MENTAL STRUCTURE SUMMARY

✔ Props → define a type (UserCardProps)
✔ State → useState<User[]> / useState<string>()
✔ Events → React.ChangeEvent / React.FormEvent
✔ API → Generic ApiResponse<T>
✔ Functions → Always type parameters & return type

This is real-world scalable structure.
******************************************************************/

```

<mark> Axios </mark>
```typescript
/******************************************************************
PRODUCTION-STYLE REACT + TYPESCRIPT
Axios + Interceptors + Proper Loading/Error Pattern
******************************************************************/

import React, { useEffect, useState } from "react";
import axios, {
    AxiosError,
    AxiosInstance,
    AxiosResponse
} from "axios";

/* ================================================================
1️⃣ GENERIC API RESPONSE TYPE
================================================================ */

type ApiResponse<T> = {
    data: T;
    message: string;
    status: number;
};

/* ================================================================
2️⃣ DOMAIN MODEL
================================================================ */

type User = {
    id: number;
    name: string;
    email: string;
};

/* ================================================================
3️⃣ AXIOS INSTANCE (Centralized Config)
================================================================ */

const api: AxiosInstance = axios.create({
    baseURL: "http://localhost:8080/api",
    timeout: 5000,
    headers: {
        "Content-Type": "application/json"
    }
});

/* ================================================================
4️⃣ REQUEST INTERCEPTOR
Example: attach token automatically
================================================================ */

api.interceptors.request.use(
    (config) => {
        const token = localStorage.getItem("token");

        if (token) {
            config.headers.Authorization = `Bearer ${token}`;
        }

        return config;
    },
    (error: AxiosError) => {
        return Promise.reject(error);
    }
);

/* ================================================================
5️⃣ RESPONSE INTERCEPTOR
Global error handling
================================================================ */

api.interceptors.response.use(
    (response: AxiosResponse) => {
        return response;
    },
    (error: AxiosError<{ message?: string }>) => {
        if (error.response?.status === 401) {
            console.error("Unauthorized — redirect to login");
        }

        return Promise.reject(error);
    }
);

/* ================================================================
6️⃣ API SERVICE LAYER (Typed)
================================================================ */

const userService = {
    getAll: async (): Promise<ApiResponse<User[]>> => {
        const response = await api.get<ApiResponse<User[]>>("/users");
        return response.data;
    },

    create: async (user: Omit<User, "id">): Promise<ApiResponse<User>> => {
        const response = await api.post<ApiResponse<User>>(
            "/users",
            user
        );
        return response.data;
    }
};

/* ================================================================
7️⃣ REACT COMPONENT
================================================================ */

const UserDashboard: React.FC = () => {

    /* ------------------------------------------------------------
    STATE (Proper Pattern)
    ------------------------------------------------------------ */

    const [users, setUsers] = useState<User[]>([]);
    const [loading, setLoading] = useState<boolean>(false);
    const [error, setError] = useState<string | null>(null);

    const [name, setName] = useState<string>("");
    const [email, setEmail] = useState<string>("");


    /* ------------------------------------------------------------
    FETCH USERS
    ------------------------------------------------------------ */

    const fetchUsers = async (): Promise<void> => {
        try {
            setLoading(true);
            setError(null);

            const result = await userService.getAll();
            setUsers(result.data);

        } catch (err) {
            const axiosError = err as AxiosError<{ message?: string }>;
            setError(
                axiosError.response?.data?.message ||
                axiosError.message ||
                "Something went wrong"
            );
        } finally {
            setLoading(false);
        }
    };

    useEffect(() => {
        fetchUsers();
    }, []);


    /* ------------------------------------------------------------
    CREATE USER
    ------------------------------------------------------------ */

    const handleSubmit = async (
        e: React.FormEvent<HTMLFormElement>
    ): Promise<void> => {
        e.preventDefault();

        try {
            setLoading(true);
            setError(null);

            const result = await userService.create({
                name,
                email
            });

            setUsers(prev => [...prev, result.data]);
            setName("");
            setEmail("");

        } catch (err) {
            const axiosError = err as AxiosError<{ message?: string }>;
            setError(
                axiosError.response?.data?.message ||
                axiosError.message ||
                "Failed to create user"
            );
        } finally {
            setLoading(false);
        }
    };


    /* ------------------------------------------------------------
    UI
    ------------------------------------------------------------ */

    return (
        <div style={{ maxWidth: 500, margin: "auto" }}>
            <h2>User Dashboard</h2>

            {error && (
                <div style={{ color: "red", marginBottom: 10 }}>
                    {error}
                </div>
            )}

            <form onSubmit={handleSubmit}>
                <input
                    type="text"
                    placeholder="Name"
                    value={name}
                    onChange={(e: React.ChangeEvent<HTMLInputElement>) =>
                        setName(e.target.value)
                    }
                />

                <input
                    type="email"
                    placeholder="Email"
                    value={email}
                    onChange={(e: React.ChangeEvent<HTMLInputElement>) =>
                        setEmail(e.target.value)
                    }
                />

                <button type="submit" disabled={loading}>
                    {loading ? "Processing..." : "Add User"}
                </button>
            </form>

            <hr />

            {loading && <p>Loading users...</p>}

            {!loading && users.map(user => (
                <div key={user.id}>
                    {user.name} - {user.email}
                </div>
            ))}
        </div>
    );
};

export default UserDashboard;


/******************************************************************
PRODUCTION PATTERN SUMMARY

✔ Axios instance centralized
✔ Request interceptor (attach token)
✔ Response interceptor (global error handling)
✔ Service layer separated from UI
✔ Generic API response typing
✔ Proper loading + error state pattern
✔ try / catch / finally structure
✔ Fully typed events & state

This is scalable architecture.
******************************************************************/

```