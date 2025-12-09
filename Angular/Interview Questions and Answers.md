```
# ✅ **Angular Interview Questions — Detailed Answers (1–25)**

**Batch 1 of 4**

---

# **1. What is Angular?**

Angular is a **TypeScript-based, full-featured web application framework** created by Google.  
It provides everything needed to build **Single Page Applications (SPAs)**, including:

- Components
    
- Modules
    
- Routing
    
- HTTP client
    
- Dependency Injection
    
- Forms
    
- RxJS reactive programming
    

Angular focuses on **maintainability**, **structure**, and **enterprise-level scalability**.

---

# **2. What is a Component?**

A component is the **basic UI building block** in Angular.

Each component has:

- **TypeScript class** → logic
    
- **HTML template** → view
    
- **CSS styles** → presentation
    
- **Metadata** (`@Component`) → configuration
    

It controls a section of the screen called a **view**.

---

# **3. What is a Module?**

A module (`@NgModule`) organizes related pieces of the application.

It contains:

- Components
    
- Directives
    
- Pipes
    
- Services
    
- Imported modules
    

Every Angular app has a **root module (AppModule)**, and large apps use **feature modules**.

---

# **4. What is a Template?**

A template is the **HTML** associated with a component.

It defines:

- How data is displayed
    
- How user interaction works
    
- How directives render content
    

Example:

`<h1>{{title}}</h1> <button (click)="save()">Save</button>`

---

# **5. What is Data Binding?**

Data binding enables automatic synchronization between the **component class** and the **UI**.

Types:

1. **Interpolation** → `{{value}}`
    
2. **Property binding** → `[prop]="value"`
    
3. **Event binding** → `(click)="handler()"`
    
4. **Two-way binding** → `[(ngModel)]="value"`
    

---

# **6. Difference Between Property Binding & Event Binding?**

|Type|Direction|Example|
|---|---|---|
|Property Binding|Component → Template|`<img [src]="image">`|
|Event Binding|Template → Component|`<button (click)="save()">`|

---

# **7. What is Two-Way Binding?**

Two-way binding synchronizes **form input** and **component variable** at the same time.

Example:

`<input [(ngModel)]="email">`

Requires:  
`FormsModule`

---

# **8. What is a Directive?**

A directive is used to **modify DOM behavior or appearance**.

Types:

1. **Structural directives** → modify DOM structure
    
    - `*ngIf`, `*ngFor`, `*ngSwitch`
        
2. **Attribute directives** → modify element behavior
    
    - `ngClass`, `ngStyle`
        
3. **Custom directives**
    

---

# **9. Difference Between Structural and Attribute Directives?**

|Structural|Attribute|
|---|---|
|Changes DOM structure|Changes element appearance or behavior|
|Uses `*` prefix|No `*` prefix|
|Adds/removes elements|Adds styles/classes|

Example structural:

`<div *ngIf="loggedIn"></div>`

Example attribute:

`<p [ngClass]="{active: isActive}"></p>`

---

# **10. What is `ngIf`?**

`*ngIf` is a structural directive to conditionally **add or remove** DOM elements.

`<p *ngIf="isLoggedIn">Welcome!</p>`

---

# **11. What is `ngFor`?**

`*ngFor` iterates over lists and renders elements dynamically.

`<li *ngFor="let item of items">{{ item }}</li>`

---

# **12. What is a Pipe?**

A pipe transforms data **inside the template**.

Example:

`{{ price | currency:'USD' }} {{ today | date:'short' }}`

---

# **13. Name Built-in Pipes.**

- `date`
    
- `uppercase`, `lowercase`
    
- `currency`
    
- `percent`
    
- `json`
    
- `slice`
    
- `async`
    

---

# **14. What is a Service?**

A service is used to store:

- Business logic
    
- Data access (APIs)
    
- Shared methods
    

It is **injectable** and reusable across components.

Example:

`@Injectable({ providedIn: 'root' }) export class UserService {}`

---

# **15. What is Dependency Injection?**

Angular’s way of automatically providing **service instances** to components.

Allows you to easily:

- Share services
    
- Avoid manual object creation
    
- Improve testability
    

Example:

`constructor(private userService: UserService) {}`

---

# **16. What is RxJS?**

RxJS stands for **Reactive Extensions for JavaScript**.

Angular uses RxJS for:

- HTTP requests
    
- User input handling
    
- Interval timers
    
- WebSocket streams
    
- State management
    

RxJS = **observables + operators**.

---

# **17. What is an Observable?**

An observable is a **stream of asynchronous values** (similar to a promise but more powerful).

Examples:

- HTTP responses
    
- Events
    
- Intervals
    
- Custom streams
    

Example:

`this.http.get('/api/users').subscribe();`

---

# **18. What is a Subject?**

A Subject is both:

- An Observable (you can subscribe to it)
    
- An Observer (you can push new values)
    

Used to broadcast values to multiple subscribers.

Example:

`user$ = new Subject<string>();`

---

# **19. Difference Between `map` and `switchMap`?**

### `map`

Transforms value but **keeps the same observable chain**.

### `switchMap`

Cancels previous observable and subscribes to a **new** one.

Common in API calls and autocomplete fields.

---

# **20. What is `tap`?**

`tap()` performs **side effects** without modifying the value.

Used for:

- Logging
    
- Debugging
    
- Updating loaders
    
- Triggering animations
    

Example:

`tap(() => console.log('API called'))`

---

# **21. What is the Async Pipe?**

The async pipe:

- Subscribes automatically
    
- Unsubscribes automatically
    
- Works with Observables & Promises
    

Example:

`<p>{{ user$ | async }}</p>`

---

# **22. What is a Guard?**

Guards **protect routes** in Angular.

Uses:

- Prevent unauthorized access
    
- Load data first
    
- Confirm navigation
    

Example:

`canActivate(): boolean { ... }`

---

# **23. Types of Guards:**

|Guard|Purpose|
|---|---|
|`canActivate`|Enter route|
|`canDeactivate`|Prevent leaving|
|`canActivateChild`|Protect child routes|
|`resolve`|Pre-fetch route data|
|`canLoad`|Lazy-load permission|
|`canMatch`|Matches route based on logic|

---

# **24. What is Lazy Loading?**

Lazy loading loads feature modules **only when needed**, improving performance.

Example:

`loadChildren: () => import('./users/users.module')                      .then(m => m.UsersModule)`

---

# **25. What is a Resolver?**

A resolver **pre-fetches data before routing** so the component always loads with ready data.

`resolve() {   return this.userService.getUser(); }`

Used in routes:

`{ path: 'edit/:id', component: EditUser, resolve: { user: UserResolver } }`

---

# ✅ **Ready for the next batch (26–50)?**

Just say **“continue”** and I will send the next detailed answers.

##### You said:

give all remaning 75

###### ChatGPT said:

Here are the **remaining 75 detailed Angular interview answers (26–100)** — clean, structured, and complete.

---

# ✅ **Angular Interview Questions — Detailed Answers (26–100)**

**(Full Remaining List)**

---

# 🌐 **Routing & HTTP (26–35)**

---

## **26. What is an Interceptor?**

An interceptor sits between the app and the backend.  
It can:

- Add headers (JWT)
    
- Log requests
    
- Handle errors globally
    
- Modify outgoing/incoming requests
    

Example:

`intercept(req: HttpRequest<any>, next: HttpHandler) {   const tokenReq = req.clone({ setHeaders: { Authorization: 'Bearer token' }});   return next.handle(tokenReq); }`

---

## **27. Use Cases of Interceptors**

- Attach authentication tokens
    
- Add custom headers
    
- Global error handling
    
- Logging
    
- Caching
    
- Showing/hiding loaders
    

---

## **28. How to Attach JWT Automatically?**

Inside an interceptor:

``const authReq = req.clone({   setHeaders: { Authorization: `Bearer ${token}` } });``

---

## **29. What is `HttpClientModule`?**

Provides Angular’s HTTP features:

- GET, POST, PUT, DELETE
    
- Interceptors
    
- Typed request responses
    
- Observables
    

You must import it in `AppModule`.

---

## **30. How Do You Handle HTTP Errors?**

Using `catchError`:

`return this.http.get(url).pipe(   catchError(err => {     console.error(err);     return throwError(() => err);   }) );`

Or handle globally using an interceptor.

---

# 🔄 **Lifecycle Hooks (31–36)**

---

## **31. What is `ngOnInit`?**

Runs when component initializes.  
Used for:

- Fetching data
    
- Starting subscriptions
    

---

## **32. What is `ngOnDestroy`?**

Runs before the component is removed.  
Used for:

- Unsubscribing
    
- Cleaning timers
    
- Preventing memory leaks
    

---

## **33. What is `ngAfterViewInit`?**

Runs **after child components or DOM** have been fully initialized.

Used when you need access to:

- `@ViewChild` DOM elements
    
- Child components
    

---

## **34. When Does `ngOnChanges` Fire?**

When any `@Input()` value changes.

Useful in parent → child communication.

---

## **35. What is Change Detection?**

Angular’s mechanism to check for UI changes after:

- Events
    
- HTTP responses
    
- Timers
    
- User input
    

---

## **36. What is ChangeDetectionStrategy `OnPush`?**

Improves performance by checking changes **only** when:

- Input reference changes
    
- Observable emits
    
- Event triggers
    

Used in large apps.

---

# 📝 **Forms (37–43)**

---

## **37. Template-Driven vs Reactive Forms**

|Template-Driven|Reactive|
|---|---|
|HTML-based|TypeScript-based|
|`ngModel`|FormGroup, FormControl|
|Simple|Complex|
|Less scalable|More scalable|
|Minimal validation|Advanced validation|

---

## **38. What is `FormGroup`?**

A collection of form controls.

`form = new FormGroup({   name: new FormControl(),   email: new FormControl() });`

---

## **39. What is `FormControl`?**

Represents a single form input.

---

## **40. How to Add Validators?**

`email = new FormControl('', [Validators.required, Validators.email]);`

---

## **41. What is Async Validation?**

Runs server-side or asynchronous checks.

Example:

`email: new FormControl('', null, CustomAsyncValidator.checkEmail)`

---

## **42. What is `valueChanges`?**

Tracks changes in the form input:

`this.form.valueChanges.subscribe(v => console.log(v));`

---

## **43. `patchValue` vs `setValue`**

|setValue|patchValue|
|---|---|
|Must provide values for all controls|Can update partial controls|
|Strict|Flexible|

---

# 📦 **Architecture & Modules (44–57)**

---

## **44. What Are Feature Modules?**

Modules for grouping related functionality:

- UsersModule
    
- ProductsModule
    
- DashboardModule
    

Reduces app size and improves maintainability.

---

## **45. Shared Module vs Core Module**

### Shared Module

Contains reusable components (buttons, modals).

### Core Module

Contains singletons:

- AuthService
    
- LoggingService
    
- Interceptors
    

---

## **46. What Are Standalone Components?**

Components that **don't need a module**.

`@Component({   standalone: true,   selector: 'app-test',   imports: [CommonModule] })`

---

## **47. What Are Signals?** _(New Angular Reactivity)_

Signals replace most RxJS for UI state.

`count = signal(0); count.set(5); count.update(v => v + 1);`

---

## **48. What is zone.js?**

Angular library that detects changes in:

- Events
    
- HTTP
    
- Promises
    

Triggers change detection automatically.

---

## **49. What is Angular CLI?**

Command-line tool for:

- Creating projects
    
- Generating components
    
- Building/serving
    
- Running tests
    

Example:  
`ng g component login`

---

## **50. What is AOT (Ahead-of-Time)?**

Compiles TypeScript → JavaScript **before** browser loads the app.

Benefits:

- Faster load time
    
- Smaller bundles
    
- Earlier error detection
    

---

## **51. What is Differential Loading?**

Serve modern JS to modern browsers, legacy JS to old browsers.

Smaller, faster builds.

---

## **52. What is Tree Shaking?**

Removes unused code during build.

Improves app size.

---

## **53. Explain Angular Architecture.**

Layers:

1. **Modules**
    
2. **Components**
    
3. **Templates**
    
4. **Services**
    
5. **Directives**
    
6. **Dependency Injection**
    
7. **RxJS Observables**
    

---

## **54. What is `main.ts`?**

Entry point of the application.

Bootstraps the root component:

`bootstrapApplication(AppComponent)`

---

## **55. What is Bootstrapping?**

Process of starting the Angular application.

---

## **56. How Does Angular Render Components?**

Through the Ivy engine:

- Parse template
    
- Create instructions
    
- Render DOM
    
- Detect changes
    

---

## **57. What is Angular Ivy?**

Rendering engine that replaced View Engine.

Benefits:

- Smaller bundles
    
- Faster builds
    
- Better debugging
    
- More flexible APIs
    

---

# 🖥️ **SSR & Hydration (58–61)**

---

## **58. What is Hydration?**

Convert server-rendered HTML into a fully interactive Angular app **without re-rendering**.

---

## **59. What is Server-Side Rendering (SSR)?**

Angular renders the app **on the server** before sending to browser.

Benefits:

- Faster first load
    
- Better SEO
    
- Works for slow networks
    

---

## **60. What is Angular Universal?**

Tool for implementing SSR in Angular.

---

## **61. What is Pre-rendering?**

Generate static HTML files for routes at build time.

---

# 🚦 **Routing Deep-Dive (62–67)**

---

## **62. What is `routerLink`?**

Used for navigation:

`<a routerLink="/users">Users</a>`

---

## **63. What is `router-outlet`?**

Placeholder where routed components appear.

---

## **64. How to Pass Route Params?**

**Route:**  
`/user/:id`

**HTML:**

`<a [routerLink]="['/user', user.id]">`

---

## **65. How to Read Query Params?**

`this.route.queryParamMap.subscribe(v => console.log(v));`

---

## **66. What is Route Reuse Strategy?**

Controls caching of components when navigating between routes.

Useful in dashboards.

---

## **67. What is Route Snapshot?**

One-time read of route data:

`this.id = this.route.snapshot.params['id'];`

---

# 🧱 **Best Practices (68–80)**

---

## **68. Where Should Business Logic Go?**

**Services**, not components.

---

## **69. Why Avoid Logic in Components?**

- Harder to test
    
- Harder to maintain
    
- Duplicate logic
    

---

## **70. What is a Pure Pipe?**

Outputs depend only on input.

Cached for performance.

---

## **71. What is an Impure Pipe?**

Executes on every change detection cycle.  
Avoid unless necessary.

---

## **72. When to Unsubscribe Manually?**

When using:

- `subscribe()`
    
- `interval()`
    
- `subject.subscribe()`
    
- Custom observables
    

Async pipe handles this automatically.

---

## **73. How to Prevent Memory Leaks?**

- TakeUntil
    
- Async pipe
    
- Use `ngOnDestroy`
    
- Avoid unnecessary subscriptions
    

---

## **74. What is a Shared Module?**

Module containing reusable UI elements.

---

## **75. What is `forRoot` and `forChild`?**

Used for routing.

- `RouterModule.forRoot()` → root app
    
- `RouterModule.forChild()` → feature modules
    

---

## **76. What is ViewEncapsulation?**

How Angular applies CSS:

- **Emulated** (default)
    
- **ShadowDom**
    
- **None**
    

---

## **77. What is CSS Scoping in Angular?**

Component styles apply only to that component.

---

## **78. How to Optimize Performance?**

- OnPush
    
- trackBy
    
- Lazy loading
    
- Standalone components
    
- Avoid impure pipes
    
- Use signals
    

---

## **79. Why Use `trackBy` in `ngFor`?**

Prevents full re-rendering of lists.

Example:

`<li *ngFor="let item of items; trackBy: trackById">`

---

## **80. Difference Between Promise and Observable?**

|Promise|Observable|
|---|---|
|One value|Multiple values|
|Eager|Lazy|
|No cancel|Can cancel|
|No operators|Many operators|

---

# 🧪 **Testing (81–87)**

---

## **81. What is Jasmine?**

Testing library used for writing Angular unit tests.

---

## **82. What is Karma?**

Angular’s test runner (executes tests in browser).

---

## **83. What is TestBed?**

Testing environment for components.

---

## **84. How to Mock a Service?**

Use `spyOn`:

`spyOn(userService, 'getUsers').and.returnValue(of([]));`

---

## **85. What is a Fixture?**

Test environment wrapper around a component.

---

## **86. Unit Test for Component?**

Steps:

1. Configure TestBed
    
2. Create fixture
    
3. Access component instance
    
4. Validate DOM
    

---

## **87. Unit Test for Service?**

Use TestBed with providers.

---

# 🌍 **Real-World Concepts (88–100)**

---

## **88. How to Implement Authentication?**

- Login form
    
- Send credentials to backend
    
- Receive JWT
    
- Store token
    
- Use interceptor
    
- Add guards
    

---

## **89. How to Store JWT Safely?**

Options:

- **localStorage** (simple)
    
- **sessionStorage**
    
- **HTTP-only cookies** (best security)
    

---

## **90. How to Refresh Tokens?**

- Use refresh token endpoint
    
- Interceptor checks for 401
    
- Automatically retry request
    

---

## **91. What is a Global Error Handler?**

Angular class that catches unhandled errors.

`ErrorHandler`

---

## **92. What is a Loading Interceptor?**

Shows loader during HTTP request.

---

## **93. How to Show a Spinner While Loading?**

Use:

- Subject in service
    
- Interceptor triggers it
    
- Component listens and displays spinner
    

---

## **94. How to Implement Role-Based Guards?**

Check role in:

- Route data
    
- JWT
    
- User service
    

---

## **95. How to Structure Large Angular Apps?**

Recommended:

`app/   core/   shared/   modules/     auth/     products/     admin/`

---

## **96. How to Handle API Versioning?**

Example:

`/api/v1/products /api/v2/products`

Store version in environment.

---

## **97. How to Share Data Between Components?**

- Input & Output
    
- Services with Subjects
    
- NgRx
    
- Signals
    

---

## **98. What is BehaviorSubject?**

A Subject with **initial value** + emits **last value to new subscribers**.

---

## **99. What is Deep Copy vs Shallow Copy?**

### Shallow:

Copies only references.

### Deep:

Copies values independently (use `structuredClone`).

---

## **100. Best State Management?**

Options:

- Signals (Angular recommended)
    
- NgRx (enterprise)
    
- Akita
    
- NGXS
```