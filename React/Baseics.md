# 1) ✅ **100 React interview questions & answers** (concise, focused, interview-style)

Below are 100 Q&A pairs grouped by topic (Fundamentals → Advanced → Ecosystem → Architecture & Patterns → Practical). Answers are short and interview-ready.

**Fundamentals (1–20)**

1. Q: What is React?  
    A: A JavaScript library for building component-driven UIs using a declarative model and (virtual) DOM diffing. [React](https://react.dev/reference/react/hooks?utm_source=chatgpt.com)
    
2. Q: What is JSX?  
    A: A JavaScript syntax extension that looks like XML/HTML and is transpiled to `React.createElement` calls.
    
3. Q: What are components?  
    A: Reusable UI pieces (function components preferred today) that accept props and manage state.
    
4. Q: Function vs Class components — which to use?  
    A: Use function components + Hooks for new code; class components are legacy but still supported.
    
5. Q: What is a prop?  
    A: Read-only inputs a parent passes to a child component.
    
6. Q: What is state?  
    A: Local data managed by a component (e.g., `useState`) that drives rendering.
    
7. Q: What is the Virtual DOM?  
    A: An in-memory representation React uses to compute minimal DOM updates for efficiency. [React](https://react.dev/reference/react/hooks?utm_source=chatgpt.com)
    
8. Q: What is `useState`?  
    A: Hook that adds state to functional components.
    
9. Q: What is `useEffect`?  
    A: Hook for side effects; runs after render and can return cleanup logic.
    
10. Q: How do you run an effect only once on mount?  
    A: `useEffect(() => { /* */ }, [])`.
    
11. Q: What is `key` in lists?  
    A: Unique identifier to help React reconcile list items efficiently.
    
12. Q: Controlled vs uncontrolled components?  
    A: Controlled: React state drives form inputs. Uncontrolled: use DOM refs for value access.
    
13. Q: What is lifting state up?  
    A: Move shared state to the closest common ancestor to share it among children.
    
14. Q: How does React handle events?  
    A: Uses synthetic events which normalize across browsers.
    
15. Q: What is `useRef` used for?  
    A: Hold mutable values across renders or reference DOM nodes.
    
16. Q: How to memoize a component?  
    A: `React.memo(Component)` to skip re-renders when props are unchanged.
    
17. Q: What is `useMemo`?  
    A: Memoize a computed value between renders.
    
18. Q: What is `useCallback`?  
    A: Memoize a function reference to prevent unnecessary re-creations.
    
19. Q: What are fragments?  
    A: `<>...</>` or `<React.Fragment>` to group children without DOM nodes.
    
20. Q: When to use `useReducer`?  
    A: For complex state updates or when state logic belongs in a reducer-like pattern.
    

**Intermediate (21–50)**  
21. Q: How to manage global state in React?  
A: Context API for small-to-medium; state libraries (Redux Toolkit, Zustand, Recoil) for larger apps.

22. Q: What is React Context?  
    A: A way to pass data deeply without prop drilling via Provider/Consumer or `useContext`.
    
23. Q: What is suspense?  
    A: React feature for data fetching and code-splitting to suspend rendering until ready.
    
24. Q: What is code splitting?  
    A: Load JS bundles lazily (e.g., `React.lazy` + `Suspense`).
    
25. Q: How to optimize performance?  
    A: Memoization (`useMemo`, `useCallback`), `React.memo`, virtualization (e.g., react-window), avoid unnecessary state updates.
    
26. Q: How to do routing?  
    A: `react-router-dom` for client-side routing and nested routes.
    
27. Q: What is server-side rendering (SSR)?  
    A: Rendering React components on the server to produce HTML (Next.js is a common framework).
    
28. Q: What is hydration?  
    A: Bootstrapping client-side React on SSR HTML.
    
29. Q: What is Concurrent Mode (or transition variants)?  
    A: React features for interruptible rendering (newer Reacts changed the naming but ideas persist).
    
30. Q: How to handle forms?  
    A: Manual controlled forms, or use libraries: React Hook Form or Formik.
    
31. Q: What is prop drilling? How to avoid it?  
    A: Passing props through many layers — avoid by using Context or lifting state less.
    
32. Q: What are Synthetic Events?  
    A: Cross-browser wrapper around native browser events used by React.
    
33. Q: How to test React components?  
    A: Use Jest + React Testing Library for unit/component tests; Cypress for E2E.
    
34. Q: How to debug hooks?  
    A: React DevTools shows hooks state; console/logging and custom hooks with dev-only checks help.
    
35. Q: What is the effect cleanup function?  
    A: Return a function from `useEffect` to clean up subscriptions/timers.
    
36. Q: How to implement authentication in React?  
    A: Often via JWTs or cookies; store tokens securely (HTTP-only cookies recommended) and protect routes with HOCs or route guards.
    
37. Q: How to do file uploads?  
    A: Use `FormData` and fetch/axios with proper content-type; use presigned uploads for cloud storage.
    
38. Q: How to implement lazy-loaded routes?  
    A: `const Page = React.lazy(() => import('./Page'));` + `<Suspense>`.
    
39. Q: What is an HOC?  
    A: Higher-order component — function that returns a new component by wrapping one.
    
40. Q: What is render props?  
    A: Passing a function as a child to share behavior; often replaced by hooks now.
    

**Advanced (51–75)**  
41. Q: Explain reconciliation.  
A: React’s algorithm to diff previous and next virtual DOM trees and apply minimal DOM operations.

42. Q: What are microfrontends and how does React fit?  
    A: Break app into independently deployable front-end pieces; React is commonly used for each slice with runtime composition.
    
43. Q: How to manage side effects and data fetching?  
    A: Use `useEffect` or data libraries like React Query (TanStack Query) for caching, background updates, and retry logic.
    
44. Q: What is the right place to put business logic?  
    A: Prefer separation: presentational components for UI, container/services/hooks for logic.
    
45. Q: What are custom hooks?  
    A: Reusable functions that encapsulate stateful logic using hooks.
    
46. Q: How to prevent prop-drilling at scale?  
    A: Combine Context with modular providers or use a state manager.
    
47. Q: How to measure performance?  
    A: React Profiler, Lighthouse, and browser devtools.
    
48. Q: How to handle accessibility (a11y)?  
    A: Use semantic HTML, ARIA attributes, keyboard navigation, and tools like axe.
    
49. Q: What are pure components?  
    A: Components that render the same output for the same props; `React.memo` for functions.
    
50. Q: How to structure a large React codebase?  
    A: Feature-based folders, clear separation of components/hooks/services, shared UI lib, strong typing with TypeScript.
    
51. Q: What are render-phase side effects and why avoid them?  
    A: Side effects must be in `useEffect`; doing them in render can cause bugs and repeated effects.
    
52. Q: How to do dependency injection in React?  
    A: Not native—use Context or external service containers.
    
53. Q: How to secure React SPA?  
    A: Use HTTPS, secure token storage (HTTP-only cookies), CSP headers, sanitize inputs, guard routes server-side too.
    
54. Q: How to handle internationalization?  
    A: Libraries: react-intl, i18next — keep translations externalized and use lazy loading.
    
55. Q: What is tree-shaking?  
    A: Removing unused code in bundling; keep modules small and import only needed pieces.
    
56. Q: How to migrate from class to hooks?  
    A: Convert lifecycle to `useEffect`, state to `useState`/`useReducer`, instance variables to `useRef`.
    
57. Q: When to use TypeScript?  
    A: For large codebases to catch errors early and improve editor tooling.
    
58. Q: How to design tests for components with hooks?  
    A: Test effects by mocking dependencies and asserting side-effects or state changes with RTL.
    
59. Q: What is the Repository pattern for front-end?  
    A: Abstract API access behind services to decouple components from network details.
    
60. Q: Explain optimistic updates.  
    A: Update UI immediately assuming server success, then reconcile if server returns error.
    

**Ecosystem & Tools (76–90)**  
61. Q: What bundlers are used with React?  
A: Vite (recommended now), webpack, Parcel.

62. Q: What is Create React App (CRA)?  
    A: An older toolchain to bootstrap apps; many now prefer Vite or Next.js.
    
63. Q: What is Next.js?  
    A: React framework for SSR, SSG, and fullstack features (APIs, routing).
    
64. Q: What is Remix?  
    A: Framework focused on web fundamentals and server-driven UI.
    
65. Q: What's React Native?  
    A: Platform to build native mobile apps using React.
    
66. Q: What is Redux Toolkit?  
    A: Opinionated set of tools to simplify Redux usage.
    
67. Q: Why use React Query / TanStack Query?  
    A: Declarative, cache-first data fetching with retries, invalidation, and background refresh.
    
68. Q: What is Storybook?  
    A: Component playground and documentation tool.
    
69. Q: How to style React components?  
    A: CSS Modules, Tailwind, styled-components, Emotion, plain CSS — choose based on team.
    
70. Q: How to set up CI/CD for React apps?  
    A: Use GitHub Actions/GitLab CI to run tests/build and deploy to Vercel, Netlify, S3+CloudFront, or container registries.
    
71. Q: What is atomic design?  
    A: A component design methodology (atoms → molecules → organisms).
    
72. Q: How to do analytics safely?  
    A: Anonymize PII, load analytics after consent, use server-side events for privacy.
    
73. Q: What is a monorepo and benefits for React?  
    A: Single repo for multiple packages (using pnpm/workspaces or Yarn) improves code sharing and release coordination.
    
74. Q: How to adopt accessibility into dev flow?  
    A: Integrate axe tests, keyboard tests, and accessibility linters in pipeline.
    
75. Q: How to avoid memory leaks?  
    A: Cleanup subscriptions/timers in `useEffect` cleanup, abort fetches on unmount.
    

**Architecture & Practical (91–100)**  
76. Q: How to integrate React with Spring Boot backend?  
A: Use REST/GraphQL, CORS config, and secure endpoints; serve static build or deploy separately with proxy. (Detailed example later.)

77. Q: How to handle large lists?  
    A: Virtualize (react-window/react-virtualized).
    
78. Q: How to do real-time in React?  
    A: Use WebSocket, Socket.io, or server-sent events and manage subscriptions via hooks.
    
79. Q: How to do feature flags in React?  
    A: Use a remote config service or local feature-flag library and guard UI/behavior appropriately.
    
80. Q: What is progressive enhancement vs SPA tradeoffs?  
    A: PWAs and SSR combine SPA UX with progressive enhancement benefits.
    
81. Q: How to debug production issues in React?  
    A: Source maps, logging with Sentry/LogRocket, user session replay.
    
82. Q: How to migrate large apps to TypeScript?  
    A: Incremental migration (allowJs/skipLibCheck), start with critical modules.
    
83. Q: What are the cost considerations of client-side rendering?  
    A: Larger JS bundle, initial load time — mitigate via code-splitting and SSR.
    
84. Q: How to organize React component library?  
    A: Publish UI primitives with tokens, use Storybook and semantic versioning.
    
85. Q: How to do design tokens?  
    A: Centralize colors/spacing/typography and expose via CSS variables or theme provider.
    
86. Q: How to measure user-perceived performance?  
    A: First Contentful Paint (FCP), Time to Interactive (TTI), Largest Contentful Paint (LCP).
    
87. Q: How to handle license compliance for dependencies?  
    A: Use license scanning tools and maintain a dependency policy.
    
88. Q: What is hydration mismatch and how to avoid it?  
    A: Differences between server HTML and client render; ensure deterministic rendering and avoid `Math.random()` during render.
    
89. Q: How do you structure error boundaries?  
    A: Use React Error Boundaries around subtrees to catch rendering errors (class components required for boundary).
    
90. Q: When to use portals?  
    A: Render elements outside the parent DOM hierarchy (modals, tooltips).
    
91. Q: How to handle multi-tenant UI differences?  
    A: Theme tokens, runtime config, and conditional rendering.
    
92. Q: How to do A/B testing?  
    A: Controlled rollouts, experiment SDKs, and analytics instrumentation.
    
93. Q: What is progressive hydration?  
    A: Prioritize interactive parts and hydrate them first for perceived speed.
    
94. Q: How to protect against XSS in React?  
    A: Avoid `dangerouslySetInnerHTML` or sanitize inputs before use.
    
95. Q: How to handle large images?  
    A: Use responsive images, lazy-loading, formats like WebP/AVIF, and image CDN.
    
96. Q: How to handle offline-first?  
    A: Service workers and indexedDB caching strategies (Workbox).
    
97. Q: How to do multi-language builds?  
    A: Lazy-load translations and pre-render fallback locales.
    
98. Q: How to do schema-based forms?  
    A: Use libraries that accept JSON schema (e.g., react-jsonschema-form).
    
99. Q: How to onboard new engineers in React codebase?  
    A: Good README, Storybook, component guidelines, linting, and starter tasks.
    
100. Q: How to keep UI consistent across apps?  
    A: Shared component library, design tokens, and rigorous code review.
    

---

# 2) ✅ **React vs Vue — comparison (concise, practical)**

Short comparative summary with practical takeaways:

- **Philosophy & API**
    
    - React: Library, JS-first, JSX, minimal core, ecosystem choices for routing/state. [React](https://react.dev/reference/react/hooks?utm_source=chatgpt.com)
        
    - Vue: Framework-like, template-based (SFCs), more batteries-included (built-in reactivity model & conventions). [Vue.js](https://vuejs.org/v2/guide/comparison.html?utm_source=chatgpt.com)
        
- **Learning curve**
    
    - Vue: gentler for designers/HTML-first developers due to templates and SFC structure.
        
    - React: steeper if unfamiliar with JSX & functional patterns, but consistent with JS ecosystem.
        
- **State & Reactivity**
    
    - React: `useState`/`useReducer` + Context; predictable immutable data flow.
        
    - Vue: reactive refs + `reactive` — automatic tracking and reactivity in templates.
        
- **TypeScript support**
    
    - React: very strong TypeScript ergonomics.
        
    - Vue: Vue 3 improved TypeScript support (Composition API), still slightly more configuration.
        
- **Ecosystem & Tooling**
    
    - React: huge ecosystem (Next.js, Vite, React Query, Redux, etc.).
        
    - Vue: strong official CLI and ecosystem (Vue Router, Pinia).
        
- **When to choose which**
    
    - Choose **React**: if you need maximum ecosystem options, strong TypeScript, or large enterprise adoption.
        
    - Choose **Vue**: if you want faster onboarding for HTML-style devs, quicker scaffolding, and more built-in conventions. [Prismic+1](https://prismic.io/blog/vue-vs-react?utm_source=chatgpt.com)
        

---

# 3) ✅ **Beginner → Advanced React roadmap (step-by-step)**

Compact, ordered roadmap you can follow:

**Level 0 — Prerequisites**

- JavaScript fundamentals (ES6+, promises, async/await, modules)
    
- HTML & CSS basics
    
- Basic Node/npm usage
    

**Beginner**

1. Setup projects with Vite or Create React App.
    
2. Learn JSX, components, props, state (`useState`).
    
3. Learn events, forms, controlled components.
    
4. Basic routing (`react-router-dom`).
    
5. Component composition & props patterns.
    

**Intermediate**  
6. Hooks: `useEffect`, `useRef`, `useMemo`, `useCallback`, `useReducer`.  
7. Context API, simple global state.  
8. Data fetching with `fetch`/`axios`.  
9. Styling patterns: CSS Modules, styled-components, Tailwind.  
10. Testing: React Testing Library + Jest.

**Advanced**  
11. State management libraries: Redux Toolkit, Zustand.  
12. Performance: memoization, virtualization, profiling.  
13. SSR/SSG with Next.js or Remix.  
14. TypeScript adoption for typesafety.  
15. Advanced patterns: HOCs, render props (historical), custom hooks.  
16. Microfrontends, monorepo workspaces, design systems.  
17. Security: XSS, CSP, secure auth patterns (HTTP-only cookies).  
18. Observability: Sentry, performance monitoring.

**Extras**

- GraphQL (Apollo/urql), React Query for data layer.
    
- Mobile with React Native.
    
- CI/CD + testing pipeline.
    

(For an interactive visual roadmap see roadmap.sh — great, maintained roadmap.) [roadmap.sh](https://roadmap.sh/react?utm_source=chatgpt.com)

---

# 4) ✅ **React small project (Code Warrior style)**

I'll give a compact project spec + file structure + main code snippets. This is "Code Warrior" style: many questions/tasks, short exercises, and a UI listing 100 questions per topic.

**Project:** `react-code-warrior` — a single-page app that contains topics, each topic has 100 questions and answers (viewable, searchable, mark-as-reviewed).

**Features**

- Topics list (e.g., Basics, Hooks, Routing)
    
- Each topic shows 100 Q&A (paginate 25 per page)
    
- Search within topic, filter unreviewed, mark reviewed
    
- Local persistence (IndexedDB/localStorage)
    

**Minimal file structure**

`src/   App.jsx   index.jsx   components/     TopicList.jsx     QuestionList.jsx     QuestionCard.jsx     SearchBar.jsx   data/     topics.json   // contains 8–10 topics each with 100 Q&A   hooks/     useLocalStorage.js`

**Key snippets (examples)**

`useLocalStorage.js`

```javascript
import { useState, useEffect } from 'react';
export function useLocalStorage(key, initial) {
  const [state, setState] = useState(() => {
    try { return JSON.parse(localStorage.getItem(key)) ?? initial } 
    catch { return initial }
  });
  useEffect(() => { localStorage.setItem(key, JSON.stringify(state)) }, [key, state]);
  return [state, setState];
}

```

`QuestionCard.jsx`

```javascript
export default function QuestionCard({ q, onToggle }) {
  return (
    <div className="card p-3 my-2">
      <div className="d-flex justify-content-between">
        <h5>{q.title}</h5>
        <button onClick={()=>onToggle(q.id)}>{q.reviewed ? '✓' : 'Mark'}</button>
      </div>
      <p>{q.answer}</p>
    </div>
  );
}

```

**Data**

- Provide `topics.json` with 100 concise Q&A per topic (we can generate that content into the repo).
    

If you'd like, I can generate the full `topics.json` (all 100 Q&A for chosen topics) and a full Vite React app scaffold (including components), but I kept the example compact so you can review structure quickly.

---

# 5) ✅ **Real-world authentication (JWT, Spring Boot backend + React frontend)**

High-level approach + secure pattern + example flow (sources: practical tutorials). [BezKoder+1](https://www.bezkoder.com/spring-boot-react-jwt-auth/?utm_source=chatgpt.com)

**Recommended secure pattern**

- Use **HTTP-only, Secure cookies** to store refresh tokens (prevents XSS access).
    
- Use **short-lived access tokens** (in-memory or as cookie) to access APIs.
    
- Backend: Spring Boot + Spring Security issue JWT access token and set refresh token as HTTP-only cookie.
    
- Frontend: React stores minimal info in memory and requests token refresh via a refresh endpoint when necessary; persist only non-sensitive UI state in localStorage.
    

**Minimal flow**

1. User logs in (`POST /api/auth/login`) with credentials.
    
2. Server validates credentials and returns:
    
    - Access token in response body (short-lived) OR as cookie
        
    - Refresh token set as HTTP-only cookie (longer-lived)
        
3. Client attaches access token in `Authorization: Bearer <token>` header for API calls.
    
4. If access token expires, client calls `/api/auth/refresh` (with HTTP-only cookie automatically sent), backend returns new access token.
    
5. Logout: backend clears refresh cookie.
    

**Spring Boot tips**

- Use Spring Security 6 and JWT libs. Protect endpoints except auth ones. Add CORS and cookie config for frontend origin. [Medium+1](https://medium.com/%40tericcabrel/implement-jwt-authentication-in-a-spring-boot-3-application-5839e4fd8fac?utm_source=chatgpt.com)
    

**React tips**

- Use Axios with interceptors to automatically attach token and refresh when 401 occurs.
    
- Keep tokens in memory to reduce XSS risk; rely on HTTP-only cookie for refresh flow.
    

If you want, I will produce a full end-to-end code example (Spring Boot 3 + Spring Security 6 snippet + React Axios interceptors, CORS config, and secure cookie handling). I already consulted recent guides while drafting this. [Djamware+1](https://www.djamware.com/post/682b19cba28dce49720a319c/integrating-jwt-authentication-with-spring-boot-and-react?utm_source=chatgpt.com)

---

# 6) ✅ **Full CRUD example with API**

**API design (REST)** for `products`:

- `GET /api/products` → list
    
- `GET /api/products/{id}` → one
    
- `POST /api/products` → create
    
- `PUT /api/products/{id}` → update
    
- `DELETE /api/products/{id}` → delete
    

**Spring Boot (backend) quick outline**

- `Product` entity (id, name, price, category, stock)
    
- `ProductRepository extends JpaRepository<Product,Long>`
    
- `ProductController` with `@RestController` and mapped endpoints
    
- Use DTOs for API input/output, validation (`@Valid`), and global exception handling.
    

**React (frontend) quick outline**

- `productService.js` using Axios for API calls
    
- `ProductList.jsx` (GET), `ProductForm.jsx` (POST/PUT), `ProductDetail.jsx`, `ConfirmDelete` modal
    
- Use optimistic UI updates or refetch strategies with React Query.
    

**Example Axios call**
```javascript
// productService.js
import axios from 'axios';
export const api = axios.create({ baseURL: '/api' });
export const getProducts = () => api.get('/products');
export const createProduct = (data) => api.post('/products', data);

```

**Notes**

- Use pagination and server-side filtering for large datasets.
    
- Validate both client and server sides.
    

If you want, I can write the full Spring Boot controller + repository + JPA entity + DTOs and a complete React CRUD UI (components + routes).

---

# 7) ✅ **Full React + Spring Boot project structure (recommended)**

Opinionated structure that scales.

**Monorepo (recommended for dev speed)**

`/project-root   /backend (Spring Boot)     src/main/java/...     src/main/resources/application.yml     pom.xml   /frontend (React + Vite)     src/       pages/       components/       services/   // axios, api wrappers       hooks/       styles/     package.json   docker-compose.yml   // optional: run backend + frontend (dev proxy)   README.md`

**Backend (Spring Boot) package layout**

`com.example.app   config        // security, CORS, JWT config   controller   dto   entity   repository   service   util`

**Frontend (React) layout**

`src/   main.jsx   App.jsx   pages/     Dashboard/     Login/     Products/   components/     ui/    // buttons, inputs     layout/   hooks/   services/ // api wrappers   store/    // context or redux   utils/   assets/`

**Dev workflow**

- Backend runs on `localhost:8080`, frontend dev server on `localhost:5173` with proxy setup for `/api`.
    
- For production: build frontend and serve static from backend or host separately with appropriate CORS.
    

---

# 8) ✅ **React dashboard UI template (starter)**

A compact, modern dashboard layout using Ant Design or Tailwind components — here's a skeleton you can implement.

**Features**

- Top nav + collapsible sidebar
    
- Cards for KPIs (revenue, users)
    
- Product table with pagination/sorting
    
- Chart area (use Recharts or chart.js)
    
- Modal to add/edit items
    

**Example component layout**

```javascript
<Layout>
  <Sider>SidebarMenu</Sider>
  <Layout>
    <Header>Topbar (user menu)</Header>
    <Content>
      <Grid>
        <KpiCard />
        <KpiCard />
        <ChartCard />
        <TableCard />
      </Grid>
    </Content>
  </Layout>
</Layout>

```

**Styling**

- Use Ant Design components (fast to implement) or Tailwind for custom look.
    

If you want, I can generate a full React + AntD dashboard page (code for `App.jsx`, `Dashboard.jsx`, sample KPI cards, table with mock data and sorting) ready to paste into a Vite project.

---

# Final notes & next steps (pick what you want next)

I covered all 8 deliverables in order with practical detail, concise Q&A, roadmap, project outlines, and secure auth guidance. I can now:

- Expand any section into full code (e.g., generate the full `topics.json` with 100 Q&A per topic, or produce the full Spring Boot + React JWT code).
    
- Scaffold the React app files for you (complete code for all components + `package.json`) OR build the full backend controllers/entities for the CRUD API.
    
- Produce a downloadable repo structure (I can generate files and provide them).