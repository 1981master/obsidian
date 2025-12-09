```text
# ✅ **(2) Angular Complete Table Refresher**

### **Angular Core Concepts — Full Table**

|Topic|Description|Example|
|---|---|---|
|**Component**|Building block of UI|`@Component({ selector: 'app-user' })`|
|**Module**|Groups components/services|`@NgModule({ declarations: [...] })`|
|**Template**|Component’s HTML|`<h1>{{title}}</h1>`|
|**Data Binding**|Sync data ↔ UI|`{{name}}`, `[value]`, `(click)`|
|**Event Binding**|Component responds to events|`(click)="save()"`|
|**Property Binding**|Pass value into elements|`[disabled]="isLoading"`|
|**Two-way Binding**|Sync input with model|`[(ngModel)]="email"`|
|**Directives**|Change DOM structure|`*ngIf`, `*ngFor`, `ngClass`|
|**Services**|Shared logic (DI)|`UserService`|
|**Dependency Injection**|Provide services|`constructor(private service: ...)`|
|**Routing**|Navigation between pages|`<router-outlet>`|
|**Route Params**|Dynamic routes|`/user/:id`|
|**Guards**|Protect routes|`canActivate()`|
|**HTTPClient**|API calls|`http.get('/api')`|
|**RxJS Observables**|Async streams|`this.http.get().subscribe()`|
|**Operators**|Transform streams|`map`, `switchMap`, `filter`|
|**Pipes**|Transform data in template|`{{price|
|**Forms Module**|Template-driven forms|`ngModel`|
|**Reactive Forms**|FormGroup + FormControl|`form = new FormGroup({...})`|
|**Lifecycle Hooks**|Component lifecycle|`ngOnInit()`, `ngOnDestroy()`|
|**Input Decorator**|Parent → Child|`@Input() user`|
|**Output Decorator**|Child → Parent|`@Output() clicked`|
|**Async Pipe**|Auto-subscribe to observable|`{{ user$|
|**Interfaces**|Data models|`interface User { id: number; }`|
|**Feature Modules**|Organize large apps|`UsersModule`|
|**Lazy Loading**|Load modules on demand|`loadChildren`|
|**Resolvers**|Fetch data before route loads|`resolve()`|
|**Interceptors**|Intercept HTTP requests|Token injection|
|**Environment Files**|Dev/prod configs|`environment.ts`|
|**Change Detection**|Optimizes app updates|`OnPush`|
|**Standalone Components**|Components w/o modules|`standalone: true`|
|**Signals**|Reactivity (new Angular feature)|`signal(0)`|
```

```
## **📌 Features You Will Build**

### **Phase 1 — Basic**

✔ Angular project setup  
✔ Navigation (Home, Products, Login)  
✔ Components, modules  
✔ Services (ProductService)  
✔ Display list of products  
✔ Add, edit, delete product (in-memory)

---

### **Phase 2 — Intermediate**

✔ Reactive Forms  
✔ Image upload preview  
✔ Category filter  
✔ Search bar  
✔ Pagination  
✔ Pipes (price, date, custom pipe)

---

### **Phase 3 — Advanced**

✔ Full CRUD with backend (Spring Boot)  
✔ JWT login + register  
✔ Route Guards  
✔ HttpInterceptor for token  
✔ Role-based access  
✔ Dashboard stats using charts  
✔ Lazy loaded modules  
✔ Standalone Components  
✔ Signals for state management

---

## **📌 Tech Stack**

- Angular 17 or 18
    
- Angular Material / Ant Design
    
- RxJS
    
- Spring Boot backend (you already have experience!)
    
- MySQL or H2
    

---

## **📌 Component Structure**

`src/app/    modules/       auth/       products/       dashboard/    services/    guards/    interceptors/    models/`

---

## **📌 Product Model**

`export interface Product {   id: number;   title: string;   price: number;   category: string;   imageUrl: string;   description: string; }`

---

## **📌 Key Screens**

1. **Login Screen** (JWT)
    
2. **Register Screen**
    
3. **Product List Page**
    
4. **Add Product Form**
    
5. **Edit Product Page**
    
6. **Admin Dashboard (charts)**
    

---

## **📌 What You Will Practice**

- All Angular core concepts
    
- RxJS streams
    
- HTTP methods
    
- Guards, interceptors
    
- Reactive forms
    
- Real authentication
    
- Modular architecture
    
- Best practices
    

---

If you want, I can generate:

✅ Full **step-by-step implementation**  
✅ All Angular code (components, services, guards)  
✅ Spring Boot backend code  
✅ Database schema  
✅ Full UI with Ant Design  
✅ And output the **entire project as a downloadable ZIP**
```