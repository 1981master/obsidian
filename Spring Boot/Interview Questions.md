## **Section 1: Spring Boot Basics (Questions 1–15)**

1. **Q:** What is Spring Boot?  
    **A:** Spring Boot is a framework built on top of Spring that simplifies configuration, setup, and deployment by providing auto-configuration, embedded servers, and starter dependencies.
    
2. **Q:** Difference between Spring and Spring Boot?  
    **A:** Spring is a general framework, requires manual setup. Spring Boot auto-configures components, embeds servers, and reduces boilerplate code.
    
3. **Q:** What is a starter in Spring Boot?  
    **A:** A starter is a dependency (e.g., `spring-boot-starter-web`) that pulls in all required dependencies for a particular functionality.
    
4. **Q:** How does Spring Boot reduce boilerplate code?  
    **A:** Through auto-configuration, embedded servers, starter dependencies, default configurations, and annotations like `@SpringBootApplication`.
    
5. **Q:** What is `@SpringBootApplication`?  
    **A:** Combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`.
    
6. **Q:** How do you run a Spring Boot application?  
    **A:** Using `SpringApplication.run(App.class, args)` in the main method or `mvn spring-boot:run`.
    
7. **Q:** How does Spring Boot handle server configuration?  
    **A:** By embedding servers like Tomcat, Jetty, or Undertow and allowing properties in `application.properties` or `application.yml`.
    
8. **Q:** What is the difference between `application.properties` and `application.yml`?  
    **A:** Both configure app properties; `.yml` supports hierarchical structures and is more readable.
    
9. **Q:** Explain Spring Boot auto-configuration.  
    **A:** It automatically configures beans based on classpath, properties, and existing beans.
    
10. **Q:** How do you exclude an auto-configuration?  
    **A:** Use `@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)`.
    
11. **Q:** What is Spring Boot CLI?  
    **A:** A command-line tool for quickly running Spring scripts and apps without Maven/Gradle setup.
    
12. **Q:** How do you create a custom Spring Boot starter?  
    **A:** Create a Maven project, define dependencies and auto-configuration class, and package it.
    
13. **Q:** What is `@ComponentScan`?  
    **A:** Scans packages for Spring-managed components (`@Component`, `@Service`, `@Controller`).
    
14. **Q:** Difference between `@Component`, `@Service`, `@Repository`, `@Controller`?  
    **A:** All are stereotypes; `@Service` for services, `@Repository` for data access, `@Controller` for web endpoints.
    
15. **Q:** What is Spring Boot DevTools?  
    **A:** A module for hot reload, live restart, and improved development workflow.
    

---

## **Section 2: Dependency Injection & Bean Management (16–30)**

16. **Q:** What is dependency injection?  
    **A:** Technique where the framework injects dependencies into beans instead of creating them manually.
    
17. **Q:** Types of DI in Spring Boot?  
    **A:** Constructor injection, setter injection, field injection.
    
18. **Q:** What is `@Autowired`?  
    **A:** Annotation to automatically inject a bean.
    
19. **Q:** Difference between `@Autowired` and `@Inject`?  
    **A:** `@Autowired` is Spring-specific; `@Inject` is Java standard (JSR-330).
    
20. **Q:** What is `@Qualifier` used for?  
    **A:** To specify which bean to inject when multiple beans of the same type exist.
    
21. **Q:** What is the Spring Bean lifecycle?  
    **A:** Instantiation → Dependency injection → Aware interfaces → PostConstruct → afterPropertiesSet → init-method → Bean ready → PreDestroy → destroy-method.
    
22. **Q:** Difference between singleton and prototype beans?  
    **A:** Singleton: one instance per container; prototype: new instance every injection.
    
23. **Q:** What is `@Scope`?  
    **A:** Defines bean scope: singleton, prototype, request, session, application.
    
24. **Q:** Difference between `ApplicationContext` and `BeanFactory`?  
    **A:** ApplicationContext is advanced, supports events, internationalization, AOP. BeanFactory is minimal DI container.
    
25. **Q:** How do you access ApplicationContext in a bean?  
    **A:** Implement `ApplicationContextAware` or use `@Autowired ApplicationContext`.
    
26. **Q:** What is `@PostConstruct` and `@PreDestroy`?  
    **A:** Lifecycle annotations for initialization and destruction of beans.
    
27. **Q:** Difference between `InitializingBean` and `@PostConstruct`?  
    **A:** `InitializingBean.afterPropertiesSet()` is Spring-specific; `@PostConstruct` is Java standard.
    
28. **Q:** What is `FactoryBean`?  
    **A:** A bean that produces other beans. Access factory via `&beanName`.
    
29. **Q:** How does Spring create proxies for AOP?  
    **A:** Using JDK dynamic proxies for interfaces or CGLIB for classes.
    
30. **Q:** Can self-invocation trigger AOP?  
    **A:** No, self-invocation bypasses the proxy.
    

---

## **Section 3: Data Access / JPA / Databases (31–45)**

31. **Q:** How do you connect Spring Boot to a database?  
    **A:** Configure `spring.datasource.url`, `username`, `password` in properties.
    
32. **Q:** What is Spring Data JPA?  
    **A:** Provides repository interfaces for CRUD, dynamic queries, and pagination.
    
33. **Q:** Difference between `CrudRepository` and `JpaRepository`?  
    **A:** JpaRepository extends CrudRepository with JPA-specific methods like flushing and paging.
    
34. **Q:** What is `@Entity`?  
    **A:** Marks a class as a JPA entity mapped to a database table.
    
35. **Q:** What is `@Table`?  
    **A:** Specifies table name and schema for the entity.
    
36. **Q:** Difference between `@OneToMany` and `@ManyToOne`?  
    **A:** OneToMany: one entity → multiple others; ManyToOne: many entities → one.
    
37. **Q:** What is `@Transactional`?  
    **A:** Annotation to manage database transactions declaratively.
    
38. **Q:** What is Lazy vs Eager fetching?  
    **A:** Lazy: loads relationship on demand; Eager: loads immediately.
    
39. **Q:** How do you write a custom query in Spring Data JPA?  
    **A:** Use `@Query` with JPQL or native SQL.
    
40. **Q:** What is PagingAndSortingRepository?  
    **A:** Provides methods for pagination and sorting.
    
41. **Q:** Difference between JPQL and SQL?  
    **A:** JPQL operates on entities, SQL on database tables.
    
42. **Q:** How to handle exceptions in Spring Boot JPA?  
    **A:** Use `@ExceptionHandler` or `@ControllerAdvice` globally.
    
43. **Q:** What is `EntityManager`?  
    **A:** Core JPA interface for CRUD operations and queries.
    
44. **Q:** What is the difference between `save` and `saveAndFlush`?  
    **A:** `saveAndFlush` forces persistence immediately; `save` may delay until transaction commit.
    
45. **Q:** How does Spring Boot auto-configure DataSource?  
    **A:** Based on classpath (H2, MySQL), properties, and `@EnableAutoConfiguration`.
    

---

## **Section 4: REST / Web Layer (46–60)**

46. **Q:** How to create REST endpoint?  
    **A:** Use `@RestController` and `@RequestMapping` / `@GetMapping`.
    
47. **Q:** Difference between `@Controller` and `@RestController`?  
    **A:** `@RestController` = `@Controller + @ResponseBody`.
    
48. **Q:** What is `@RequestParam`?  
    **A:** Binds query parameter to method argument.
    
49. **Q:** What is `@PathVariable`?  
    **A:** Binds URI path segment to method argument.
    
50. **Q:** What is `@RequestBody`?  
    **A:** Maps JSON request payload to a Java object.
    
51. **Q:** What is `@ResponseBody`?  
    **A:** Sends method return as HTTP response body (JSON/XML).
    
52. **Q:** How to handle exceptions globally?  
    **A:** Use `@ControllerAdvice` and `@ExceptionHandler`.
    
53. **Q:** What is content negotiation?  
    **A:** Serving JSON, XML, or other formats based on request `Accept` header.
    
54. **Q:** How to version REST APIs in Spring Boot?  
    **A:** URI versioning (`/v1/items`), header versioning, or params.
    
55. **Q:** What is `@CrossOrigin`?  
    **A:** Enables CORS for REST endpoints.
    
56. **Q:** Difference between `ResponseEntity` and POJO return?  
    **A:** ResponseEntity allows setting status, headers, and body.
    
57. **Q:** How to validate request body?  
    **A:** Use `@Valid` and validation annotations (`@NotNull`, `@Size`).
    
58. **Q:** What is `HandlerInterceptor`?  
    **A:** Intercepts requests pre/post controller execution.
    
59. **Q:** Difference between filter and interceptor?  
    **A:** Filter: servlet level; Interceptor: Spring MVC level.
    
60. **Q:** How does Spring Boot handle static resources?  
    **A:** Serves from `/static`, `/public`, `/resources` automatically.
    

---

## **Section 5: Spring Security (61–75)**

61. **Q:** How to enable Spring Security?  
    **A:** Add `spring-boot-starter-security` dependency.
    
62. **Q:** Default login page behavior?  
    **A:** Spring Boot generates a default login page at `/login`.
    
63. **Q:** What is `UserDetailsService`?  
    **A:** Loads user-specific data for authentication.
    
64. **Q:** How to define roles and authorities?  
    **A:** Assign `ROLE_USER`, `ROLE_ADMIN` to users; configure with `@PreAuthorize` or `.hasRole()`.
    
65. **Q:** Difference between `@PreAuthorize` and `@Secured`?  
    **A:** `@PreAuthorize` supports SpEL expressions; `@Secured` is simple role check.
    
66. **Q:** What is `BCryptPasswordEncoder`?  
    **A:** Hashes passwords for secure storage.
    
67. **Q:** How to enable JWT authentication?  
    **A:** Implement filter for token validation, set authentication in `SecurityContext`.
    
68. **Q:** What is `SecurityContextHolder`?  
    **A:** Stores authentication info for current thread.
    
69. **Q:** How to protect endpoints by role?  
    **A:** Use `http.authorizeRequests().antMatchers("/admin").hasRole("ADMIN")`.
    
70. **Q:** What is CSRF protection?  
    **A:** Prevents cross-site request forgery attacks.
    
71. **Q:** How to disable CSRF?  
    **A:** `http.csrf().disable()`.
    
72. **Q:** What is filter chain?  
    **A:** Spring Security uses `FilterChainProxy` to delegate request through security filters.
    
73. **Q:** Difference between Basic and Form authentication?  
    **A:** Basic: HTTP headers; Form: login page + session.
    
74. **Q:** How to log out programmatically?  
    **A:** Use `SecurityContextHolder.clearContext()` or `/logout` endpoint.
    
75. **Q:** Difference between session and stateless JWT?  
    **A:** Session: server maintains state; JWT: token stores authentication, stateless.
    

---

## **Section 6: Spring Boot Actuator & Monitoring (76–85)**

76. **Q:** What is Spring Boot Actuator?  
    **A:** Monitoring and management tool providing endpoints like `/health`, `/metrics`.
    
77. **Q:** How to enable Actuator endpoints?  
    **A:** Configure `management.endpoints.web.exposure.include=*` in properties.
    
78. **Q:** How to create custom health check?  
    **A:** Implement `HealthIndicator` interface.
    
79. **Q:** How to expose metrics to Prometheus?  
    **A:** Add `micrometer-registry-prometheus` dependency.
    
80. **Q:** How to secure actuator endpoints?  
    **A:** Use Spring Security and restrict `/actuator/**` by role.
    
81. **Q:** Difference between `/actuator/info` and `/actuator/health`?  
    **A:** Info: app metadata; Health: service health status.
    
82. **Q:** What is `MeterRegistry`?  
    **A:** Micrometer interface to register custom metrics.
    
83. **Q:** How to enable HTTP trace endpoint?  
    **A:** `management.endpoint.httptrace.enabled=true`.
    
84. **Q:** How to change actuator base path?  
    **A:** `management.endpoints.web.base-path=/manage`.
    
85. **Q:** How to integrate actuator with Grafana?  
    **A:** Export metrics to Prometheus, Grafana reads Prometheus metrics.
    

---

## **Section 7: Testing (86–92)**

86. **Q:** How to test Spring Boot applications?  
    **A:** Use `@SpringBootTest`, `@WebMvcTest`, `@DataJpaTest`.
    
87. **Q:** Difference between `@SpringBootTest` and `@WebMvcTest`?  
    **A:** SpringBootTest: loads full context; WebMvcTest: loads only controller layer.
    
88. **Q:** How to mock beans?  
    **A:** Use `@MockBean`.
    
89. **Q:** How to perform REST API test?  
    **A:** Use `MockMvc` or `TestRestTemplate`.
    
90. **Q:** How to test JPA repository?  
    **A:** Use `@DataJpaTest` and H2 in-memory DB.
    
91. **Q:** How to load test properties?  
    **A:** Use `@TestPropertySource` or `@DynamicPropertySource`.
    
92. **Q:** How to verify Spring Security roles in tests?  
    **A:** Use `@WithMockUser(roles="ADMIN")`.
    

---

## **Section 8: Advanced Features & Internals (93–100)**

93. **Q:** What is Spring Boot auto-configuration?  
    **A:** Automatically configures beans based on classpath, properties, and other beans.
    
94. **Q:** How does `@ConditionalOnClass` work?  
    **A:** Creates bean only if specified class exists on classpath.
    
95. **Q:** How does `@Transactional` work internally?  
    **A:** Proxy-based, `TransactionInterceptor` starts, commits, or rolls back transactions.
    
96. **Q:** What is Spring Boot startup sequence?  
    **A:** main() → SpringApplication → Environment → AutoConfiguration → ApplicationContext → Beans → DispatcherServlet → App ready.
    
97. **Q:** Difference between BeanFactory and ApplicationContext?  
    **A:** ApplicationContext adds AOP, events, i18n; BeanFactory is minimal DI container.
    
98. **Q:** How does Spring Boot handle embedded Tomcat?  
    **A:** Auto-configures ServletWebServerApplicationContext with embedded Tomcat server.
    
99. **Q:** How does Spring Boot handle externalized configuration?  
    **A:** Loads properties from application.properties/yml, environment, command-line args, and profiles.
    
100. **Q:** How to customize Spring Boot logging?  
    **A:** Use `application.properties` (`logging.level.root=INFO`) or `logback-spring.xml`.
    

---

✅ This gives **100 Spring Boot questions with answers**, covering **junior → senior level concepts**: basics, DI, REST, JPA, Security, Actuator, testing, advanced features, internals.

---
