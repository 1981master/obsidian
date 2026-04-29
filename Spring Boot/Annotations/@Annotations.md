# 🌟 **Spring Boot / Spring Annotations**

---

## **1. Core & Configuration Annotations**

| Annotation                  | Description                                                                           |
| --------------------------- | ------------------------------------------------------------------------------------- |
| `@SpringBootApplication`    | Combines `@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan`               |
| `@Configuration`            | Marks a class as a source of bean definitions                                         |
| `@Bean`                     | Declares a bean method inside a `@Configuration` class                                |
| `@ComponentScan`            | Scans packages for components                                                         |
| `@Import`                   | Imports additional configuration classes                                              |
| `@ImportResource`           | Imports XML-based configuration                                                       |
| `@ConditionalOnClass`       | Auto-configure if a class is on the classpath                                         |
| `@ConditionalOnMissingBean` | Auto-configure only if bean is missing                                                |
| `@ConditionalOnProperty`    | Configure bean based on property value                                                |
| `@ConditionalOnBean`        | Configure bean only if another bean exists                                            |
| `@Profile`                  | Load bean only for a specific Spring profile                                          |
| `@Primary`                  | Marks a bean as primary when multiple beans exist                                     |
| `@Lazy`                     | Lazy initialization of bean                                                           |
| `@scpe`                     | change the default singleton to like prototype: create new instance for each request. |
```java
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;

@Configuration
@PropertySource("classpath:custom.properties")
public class AppConfig {
    // Beans and configuration here
}

```
```java
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@ConfigurationProperties(prefix = "app")
public class AppProperties {

    private String name;//this must be in app.name
    private int version;//this must be in app.version

    // Getters and setters

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getVersion() {
        return version;
    }

    public void setVersion(int version) {
        this.version = version;
    }
}

```
---

## **2. Stereotype / Component Annotations**

|Annotation|Description|
|---|---|
|`@Component`|Generic Spring-managed bean|
|`@Service`|Business service layer bean|
|`@Repository`|DAO / persistence layer bean, translates exceptions|
|`@Controller`|MVC controller (returns views)|
|`@RestController`|`@Controller + @ResponseBody`, returns JSON|
|`@ControllerAdvice`|Global exception handling for controllers|
|`@RestControllerAdvice`|Exception handling for REST controllers|

---

## **3. Dependency Injection / Bean Wiring**

|Annotation|Description|
|---|---|
|`@Autowired`|Inject bean dependency|
|`@Qualifier`|Specify which bean to inject when multiple exist| always win over @Primary and/or @Required(Deprecated not used now)
|`@Inject`|Standard JSR-330 injection (like `@Autowired`)|
|`@Value`|Inject property value from properties file|
|`@Resource`|JSR-250 injection by name|
|`@Required`|Marks a required property (legacy, rarely used)|Deprecated used now @Primary

---

## **4. Spring MVC / Web Annotations**

|Annotation|Description|
|---|---|
|`@RequestMapping`|Maps URL to handler method|
|`@GetMapping`|Shortcut for GET request mapping|
|`@PostMapping`|Shortcut for POST request mapping|
|`@PutMapping`|Shortcut for PUT request mapping|
|`@DeleteMapping`|Shortcut for DELETE request mapping|
|`@PatchMapping`|Shortcut for PATCH request mapping|
|`@PathVariable`|Bind URI path variable to method parameter|
|`@RequestParam`|Bind query parameter or form data|
|`@RequestBody`|Bind JSON/XML request body to object|
|`@ResponseBody`|Send method return as HTTP response|
|`@CrossOrigin`|Enable CORS for endpoints|
|`@ModelAttribute`|Bind form/request data to model object|
|`@SessionAttributes`|Store model attributes in session|
|`@ExceptionHandler`|Handle exceptions for controller methods|
|`@InitBinder`|Customize web data binding|
|`@ControllerAdvice`|Global exception/response handling|
|`@ResponseStatus`|Set HTTP status for response or exception|

---

## **5. Spring Data / JPA Annotations**

|Annotation|Description|
|---|---|
|`@Entity`|Marks a class as a JPA entity|
|`@Table`|Maps entity to DB table|
|`@Id`|Primary key field|
|`@GeneratedValue`|Auto-generate ID values|
|`@Column`|Maps field to column|
|`@OneToOne`|One-to-one relationship|
|`@OneToMany`|One-to-many relationship|
|`@ManyToOne`|Many-to-one relationship|
|`@ManyToMany`|Many-to-many relationship|
|`@JoinColumn`|Specifies foreign key column|
|`@JoinTable`|Specifies join table for many-to-many|
|`@Transient`|Exclude field from persistence|
|`@Embedded`|Embeddable object in entity|
|`@EmbeddedId`|Composite primary key|
|`@NamedQuery`|Predefined JPQL query|
|`@Query`|Custom JPQL / native query|
|`@Modifying`|Mark query as update/delete|
|`@EnableJpaRepositories`|Enable Spring Data JPA repositories|

---

## **6. Spring AOP / Transaction Annotations**

|Annotation|Description|
|---|---|
|`@Aspect`|Marks a class as an aspect|
|`@Before`|Advice before method execution|
|`@After`|Advice after method execution|
|`@AfterReturning`|Advice after successful execution|
|`@AfterThrowing`|Advice after exception thrown|
|`@Around`|Advice wraps method execution|
|`@Pointcut`|Define pointcut expression|
|`@EnableAspectJAutoProxy`|Enable AOP proxy creation|
|`@Transactional`|Declarative transaction management|

---

## **7. Spring Boot Actuator Annotations**

|Annotation|Description|
|---|---|
|`@Endpoint`|Create custom actuator endpoint|
|`@ReadOperation`|GET operation for actuator endpoint|
|`@WriteOperation`|POST/PUT operation for actuator endpoint|
|`@DeleteOperation`|DELETE operation for actuator endpoint|
|`@Selector`|Bind path variable in custom actuator endpoint|

---

## **8. Spring Boot Testing Annotations**

|Annotation|Description|
|---|---|
|`@SpringBootTest`|Load full application context for tests|
|`@WebMvcTest`|Load only controller layer for testing|
|`@DataJpaTest`|Load repository layer with in-memory DB|
|`@MockBean`|Mock a Spring bean in test context|
|`@TestConfiguration`|Custom test-specific configuration|
|`@AutoConfigureMockMvc`|Configure MockMvc for web tests|
|`@ActiveProfiles`|Set Spring profile for tests|
|`@WithMockUser`|Mock authenticated user for Spring Security tests|

---

## **9. Spring Boot Scheduling & Async Annotations**

|Annotation|Description|
|---|---|
|`@EnableScheduling`|Enable scheduled tasks|
|`@Scheduled`|Schedule method execution|
|`@EnableAsync`|Enable asynchronous execution|
|`@Async`|Mark method for async execution|

---

## **10. Spring Boot Miscellaneous Annotations**

|Annotation|Description|
|---|---|
|`@Conditional`|Generic conditional configuration|
|`@EventListener`|Listen to Spring events|
|`@EnableConfigurationProperties`|Enable `@ConfigurationProperties` binding|
|`@ConfigurationProperties`|Bind properties to POJO|
|`@Order`|Set order for beans/aspects|
|`@EnableCaching`|Enable caching|
|`@Cacheable`|Cache method return values|
|`@CacheEvict`|Remove from cache|
|`@CachePut`|Update cache without skipping method execution|
|`@EnableTransactionManagement`|Enable annotation-driven transactions|
|`@EnableWebSecurity`|Enable Spring Security|
|`@EnableOAuth2Client`|Enable OAuth2 client support|

---

✅ This is **essentially all commonly used Spring Boot / Spring Framework annotations**, categorized for easy reference.

> Note: Spring Boot builds on Spring Framework, so many annotations (like `@Component`, `@Transactional`, etc.) are technically Spring annotations but are heavily used in Spring Boot.

---

# **1. `@ControllerAdvice`**

`@ControllerAdvice` is a **specialized component** in Spring MVC used for **global exception handling, data binding, and model attribute management** across multiple controllers.

Think of it as a **global controller “interceptor” for cross-cutting concerns**.

---

## **1.1 Key Features**

- **Global Exception Handling**: Handle exceptions thrown by any controller.
    
- **Global Data Binding**: Prepopulate model attributes for all controllers.
    
- **Global Model Attributes**: Add attributes to all responses.
    

---

## **2. Basic Example**

### Exception Handling

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleNotFound(ResourceNotFoundException ex) {
        return ResponseEntity
                .status(HttpStatus.NOT_FOUND)
                .body(ex.getMessage());
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGeneral(Exception ex) {
        return ResponseEntity
                .status(HttpStatus.INTERNAL_SERVER_ERROR)
                .body("Something went wrong!");
    }
}

//Right now you're returning plain strings. In real applications, it's often better to return a structured response:
public class ErrorResponse {
    private String message;
    private int status;
    private long timestamp;

    // constructors, getters, setters
}
//then:
return ResponseEntity
        .status(HttpStatus.NOT_FOUND)
        .body(new ErrorResponse(ex.getMessage(), 404, System.currentTimeMillis()));
        
        
```

```java
//Full with Real world eg:
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.context.request.WebRequest;

import jakarta.servlet.http.HttpServletRequest;
import java.time.LocalDateTime;
import java.util.stream.Collectors;

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(
            ResourceNotFoundException ex,
            HttpServletRequest request
    ) {
        ErrorResponse error = ErrorResponse.builder()
                .timestamp(LocalDateTime.now())
                .status(HttpStatus.NOT_FOUND.value())
                .error(HttpStatus.NOT_FOUND.name())
                .message(ex.getMessage())
                .path(request.getRequestURI())
                .build();

        return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(org.springframework.web.bind.MethodArgumentNotValidException.class)
    public ResponseEntity<ErrorResponse> handleValidation(
            org.springframework.web.bind.MethodArgumentNotValidException ex,
            HttpServletRequest request
    ) {
        String validationMessage = ex.getBindingResult()
                .getFieldErrors()
                .stream()
                .map(err -> err.getField() + ": " + err.getDefaultMessage())
                .collect(Collectors.joining(", "));

        ErrorResponse error = ErrorResponse.builder()
                .timestamp(LocalDateTime.now())
                .status(HttpStatus.BAD_REQUEST.value())
                .error(HttpStatus.BAD_REQUEST.name())
                .message(validationMessage)
                .path(request.getRequestURI())
                .build();

        return new ResponseEntity<>(error, HttpStatus.BAD_REQUEST);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneral(
            Exception ex,
            HttpServletRequest request
    ) {
        ErrorResponse error = ErrorResponse.builder()
                .timestamp(LocalDateTime.now())
                .status(HttpStatus.INTERNAL_SERVER_ERROR.value())
                .error(HttpStatus.INTERNAL_SERVER_ERROR.name())
                .message("Unexpected error occurred")
                .path(request.getRequestURI())
                .build();

        return new ResponseEntity<>(error, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}

import java.time.LocalDateTime;

public class ErrorResponse {

    private LocalDateTime timestamp;
    private int status;
    private String error;
    private String message;
    private String path;

    private ErrorResponse(Builder builder) {
        this.timestamp = builder.timestamp;
        this.status = builder.status;
        this.error = builder.error;
        this.message = builder.message;
        this.path = builder.path;
    }

    public static Builder builder() {
        return new Builder();
    }

    public static class Builder {
        private LocalDateTime timestamp;
        private int status;
        private String error;
        private String message;
        private String path;

        public Builder timestamp(LocalDateTime timestamp) {
            this.timestamp = timestamp;
            return this;
        }

        public Builder status(int status) {
            this.status = status;
            return this;
        }

        public Builder error(String error) {
            this.error = error;
            return this;
        }

        public Builder message(String message) {
            this.message = message;
            return this;
        }

        public Builder path(String path) {
            this.path = path;
            return this;
        }

        public ErrorResponse build() {
            return new ErrorResponse(this);
        }
    }

    public LocalDateTime getTimestamp() { return timestamp; }
    public int getStatus() { return status; }
    public String getError() { return error; }
    public String getMessage() { return message; }
    public String getPath() { return path; }
}
```

- `@ExceptionHandler` methods inside `@ControllerAdvice` **catch exceptions thrown from any controller**.
    
- Avoid writing repetitive try-catch in each controller.
    

---

### Model Attributes Example

`@ControllerAdvice public class GlobalModelAdvice {      @ModelAttribute("appName")     public String appName() {         return "Osly Online Shopping";     } }`

- The attribute `appName` will be available in **all controllers’ models**.
    

---

### Data Binding Example

`@ControllerAdvice public class GlobalBindingAdvice {      @InitBinder     public void initBinder(WebDataBinder binder) {         binder.setDisallowedFields("id"); // Prevent binding for certain fields     } }`

- Customizes **binding behavior globally** for all controllers.
    

---

## **3. Difference Between `@ControllerAdvice` and `@RestControllerAdvice`**

- `@ControllerAdvice` → used with **traditional MVC controllers**, can return views.
    
- `@RestControllerAdvice` → combines `@ControllerAdvice + @ResponseBody`, returns JSON responses automatically (used for REST APIs).
    

---

## **4. When to Use `@ControllerAdvice`**

- Global exception handling → reduces boilerplate.
    
- Pre-populate common model attributes.
    
- Custom global data binding rules.
    

---

## **5. Flow Diagram**

`Client Request → Controller → Throws Exception                   │                   ▼           @ControllerAdvice                   │                   ▼        ExceptionHandler method executes                   │                   ▼            Response returned`

---

✅ **Key Point:** `@ControllerAdvice` is like a **global aspect for controllers**. It is not for normal business logic — only for **cross-cutting concerns like error handling, model attributes, or binding**.


# **1. Core / Boot Annotations**

- `@SpringBootApplication` → main app configuration
    
- `@Configuration` → marks a config class
    
- `@Bean` → defines a bean
    
- `@ComponentScan` → scans for components
    
- `@EnableAutoConfiguration` → enables auto-configuration (part of `@SpringBootApplication`)
    
- `@ConditionalOnClass`, `@ConditionalOnMissingBean`, `@ConditionalOnProperty` → conditional beans
    
- `@Profile` → bean active for specific profile
    
- `@Primary` → resolve multiple bean conflicts
    
- `@Lazy` → lazy initialization
    

---

# **2. Stereotype / Component Annotations**

- `@Component` → generic bean
    
- `@Service` → service layer
    
- `@Repository` → DAO layer (handles exceptions)
    
- `@Controller` → MVC controller
    
- `@RestController` → controller returning JSON
    
- `@ControllerAdvice` → **global exception / model handling**
    
- `@RestControllerAdvice` → `@ControllerAdvice + @ResponseBody`
    
- `@Aspect` → for AOP
    

> **Often missed:** `@ControllerAdvice` / `@RestControllerAdvice` for **global handling**.

---

# **3. Dependency Injection**

- `@Autowired` → inject dependency
    
- `@Qualifier` → choose specific bean
    
- `@Value` → inject property
    
- `@Inject` → JSR-330 standard
    
- `@Resource` → inject by name
    
- `@Required` → legacy, rarely used
    

---

# **4. Web / REST**

- `@RequestMapping` → base mapping
    
- `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping` → HTTP shortcuts
    
- `@RequestParam` → query parameter
    
- `@PathVariable` → path segment
    
- `@RequestBody` → JSON to object
    
- `@ResponseBody` → method return as HTTP response
    
- `@CrossOrigin` → CORS
    
- `@ModelAttribute` → model binding
    
- `@SessionAttributes` → session storage
    
- `@ExceptionHandler` → method-level exception
    
- `@InitBinder` → customize binding
    

> **Often missed:** `@ExceptionHandler` inside `@ControllerAdvice`, `@ModelAttribute` for global attributes.

---

# **5. Data / JPA**

- `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, `@Column`
    
- `@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`
    
- `@JoinColumn`, `@JoinTable`
    
- `@Transient` → ignore field
    
- `@Embedded`, `@EmbeddedId`
    
- `@NamedQuery`, `@Query`, `@Modifying`
    
- `@EnableJpaRepositories`
    

> **Often missed:** `@Modifying` for update/delete queries, `@Embedded` for composite objects.

---

# **6. Transactions / AOP**

- `@Transactional` → transactional management
    
- `@EnableAspectJAutoProxy` → enable AOP proxies
    
- `@Before`, `@After`, `@Around`, `@AfterReturning`, `@AfterThrowing`, `@Pointcut`
    

> **Often missed:** Self-invocation bypasses `@Transactional`.

---

# **7. Actuator**

- `@Endpoint` → custom actuator endpoint
    
- `@ReadOperation`, `@WriteOperation`, `@DeleteOperation`
    
- `@Selector` → path variable for custom endpoint
    

---

# **8. Testing**

- `@SpringBootTest` → full context
    
- `@WebMvcTest` → controller layer
    
- `@DataJpaTest` → repository layer
    
- `@MockBean` → mock a bean
    
- `@AutoConfigureMockMvc`
    
- `@ActiveProfiles` → set profile
    
- `@WithMockUser` → Spring Security testing
    

> **Often missed:** `@WithMockUser` for security tests.

---

# **9. Scheduling / Async**

- `@EnableScheduling` → enable scheduler
    
- `@Scheduled` → schedule method
    
- `@EnableAsync` → async execution
    
- `@Async` → mark method as async
    

---

# **10. Misc / Config**

- `@Conditional` → custom conditional
    
- `@EventListener` → listen to Spring events
    
- `@EnableConfigurationProperties` → enable properties binding
    
- `@ConfigurationProperties` → bind properties to POJO
    
- `@EnableCaching`, `@Cacheable`, `@CacheEvict`, `@CachePut`
    
- `@EnableTransactionManagement` → annotation-driven transactions
    
- `@EnableWebSecurity`, `@EnableOAuth2Client` → security config
    

---

### ✅ **Key “Often Missing” Annotations**

- `@ControllerAdvice` / `@RestControllerAdvice`
    
- `@ExceptionHandler`
    
- `@ModelAttribute` (for global model attributes)
    
- `@InitBinder`
    
- `@WithMockUser` (security tests)
    
- `@Modifying` (Spring Data update/delete queries)
    
- `@Async` / `@EnableAsync` (async methods)
    
- `@ConfigurationProperties` (property binding)
    
- `@Selector` / custom actuator annotations








========================================================================
# **1. JWT in Spring Boot**

- JWT (JSON Web Token) is **just a token**; Spring Security handles authentication and authorization.
    
- You usually implement **filters** that parse JWT tokens from requests and set authentication in `SecurityContextHolder`.
    
- Annotations are used to **protect endpoints** or **inject authenticated user info**.
    

---

# **2. Common Annotations Used with JWT**

| Annotation                                                    | Purpose                                                    |
| ------------------------------------------------------------- | ---------------------------------------------------------- |
| `@PreAuthorize("hasRole('ADMIN')")`                           | Protect method by role, works if JWT contains roles        |
| `@PostAuthorize("returnObject.owner == authentication.name")` | Access check after method execution                        |
| `@Secured("ROLE_USER")`                                       | Role-based method security                                 |
| `@AuthenticationPrincipal`                                    | Inject currently authenticated user (from JWT) into method |
| `@EnableWebSecurity`                                          | Enable Spring Security config (needed for JWT)             |

---

# **3. Example: Protecting Endpoint with JWT**

`@RestController @RequestMapping("/api") public class ProductController {      @GetMapping("/admin")     @PreAuthorize("hasRole('ADMIN')")  // JWT must contain role ADMIN     public String adminAccess() {         return "Only admin can access";     }      @GetMapping("/profile")     public String getProfile(@AuthenticationPrincipal UserDetails user) {         return "Hello " + user.getUsername();     } }`

- JWT token is **parsed in a filter**, not via annotation.
    
- `@PreAuthorize` / `@Secured` uses the **authentication from JWT**.
    

---

# **4. JWT Handling Flow**

`Client Request → JWT Filter → Validate Token → Set Authentication in SecurityContext                    │                    ▼              Controller / Method                    │                    ▼              @PreAuthorize / @AuthenticationPrincipal works`

---

# **5. Key Points**

- There is **no special `@JWT` annotation** in Spring Security.
    
- JWT support is **implemented via filter** + standard security annotations (`@PreAuthorize`, `@AuthenticationPrincipal`).
    
- Spring Security reads **roles/claims from JWT** to enforce access.







---------------------------------------------------------------------
# **1. Jackson / JSON Annotations in Spring Boot**

|Annotation|Purpose|
|---|---|
|`@JsonProperty`|Maps JSON property name to Java field (can rename fields).|
|`@JsonIgnore`|Ignore a field during serialization/deserialization.|
|`@JsonIgnoreProperties`|Ignore multiple fields globally or on class.|
|`@JsonInclude`|Include properties conditionally (e.g., non-null, non-empty).|
|`@JsonFormat`|Format fields like dates, e.g., `yyyy-MM-dd`.|
|`@JsonCreator`|Custom constructor/factory method for deserialization.|
|`@JsonValue`|Serialize a method’s return value instead of the object.|
|`@JsonAnyGetter`|Serialize extra dynamic properties from Map.|
|`@JsonAnySetter`|Deserialize extra unknown properties into Map.|
|`@JsonManagedReference`|Handle forward part of bi-directional relationships.|
|`@JsonBackReference`|Handle backward part of bi-directional relationships (prevents infinite recursion).|
|`@JsonTypeInfo`|Include type information for polymorphic types.|
|`@JsonTypeName`|Specify type name for polymorphic serialization.|
|`@JsonDeserialize`|Specify custom deserializer class.|
|`@JsonSerialize`|Specify custom serializer class.|

---

# **2. Examples**

### Ignore Fields

`public class User {     private String username;      @JsonIgnore     private String password;  // Will not appear in JSON }`

### Rename Field

`public class User {     @JsonProperty("full_name")     private String name; }`

**Input JSON:** `{"full_name": "Mohmmed"}` → mapped to `name` field.

---

### Handle Bi-directional Relationships

`public class User {     @JsonManagedReference     private List<Order> orders; }  public class Order {     @JsonBackReference     private User user; }`

- Prevents **infinite recursion** when serializing parent-child relationships.
    

---

### Format Date

`public class Event {     @JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd HH:mm:ss")     private LocalDateTime eventTime; }`

---

### Custom Serializer / Deserializer

`@JsonSerialize(using = CustomDateSerializer.class) @JsonDeserialize(using = CustomDateDeserializer.class) private LocalDate date;`

- Useful for **custom JSON formats**.
    

---

### Dynamic Properties

`public class Dynamic {     private Map<String, Object> properties = new HashMap<>();      @JsonAnySetter     public void set(String key, Object value) {         properties.put(key, value);     }      @JsonAnyGetter     public Map<String, Object> any() {         return properties;     } }`

- Any unknown JSON property goes into the Map.
    

---

# **3. Common Patterns in Spring Boot**

1. Use `@JsonIgnore` for **sensitive fields** (like passwords or tokens).
    
2. Use `@JsonProperty` to **align JSON with frontend naming**.
    
3. Use `@JsonFormat` for **date formatting**.
    
4. Use `@JsonManagedReference` / `@JsonBackReference` to **prevent infinite recursion in JPA entities**.

# **. Scheduling / Async**

- Enable scheduler: `@EnableScheduling`, `@Scheduled`
    
- Enable async: `@EnableAsync`, `@Async`