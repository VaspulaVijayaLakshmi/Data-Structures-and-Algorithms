#  Spring Boot

**Spring Boot fundamentals, persistence, REST APIs, advanced features, testing, and interview prep**.  


---

## 🔹 1. Core Spring Boot Concepts

### Topics
- Spring vs Spring Boot
- Auto-configuration, starter dependencies
- Spring Boot annotations:  
  - `@SpringBootApplication`, `@RestController`, `@Service`, `@Repository`
- Application Properties:
  - `application.properties` vs `application.yml`
  - Profiles and environment-specific configurations
- Embedded Server:
  - How Spring Boot runs standalone (Tomcat/Jetty)
  - Changing default ports

### Hands-on
- Create a small REST API with CRUD operations
- Test endpoints using Postman or cURL

---

## 🔹 2. Spring Boot Data & Persistence

### Topics
- **Spring Data JPA**
  - `@Entity`, `@Id`, `@GeneratedValue`
  - `CrudRepository` vs `JpaRepository`
  - Query methods, JPQL, `@Query`
- **Database Integration**
  - H2 in-memory DB for testing
  - MySQL/PostgreSQL integration
- **Transactions**
  - `@Transactional` usage and pitfalls

### Hands-on
- Build a simple API to manage users/products with a database

---

## 🔹 3. REST APIs & Exception Handling

### Topics
- REST Principles
  - HTTP methods: GET, POST, PUT, DELETE
  - `@RequestMapping`, `@GetMapping`, `@PostMapping`, etc.
- DTOs & Validation
  - `@Valid`, `@NotNull`, `@Size`, `@Pattern`
  - Using `BindingResult`
- Exception Handling
  - `@ControllerAdvice`, `@ExceptionHandler`

### Hands-on
- Implement validation and custom exceptions in your CRUD API

---

## 🔹 4. Spring Boot Advanced Features

### Topics
- **Security**
  - Basics of Spring Security
  - `@EnableWebSecurity`, `WebSecurityConfigurerAdapter`
  - JWT Authentication (simple flow)
- **Caching**
  - `@Cacheable`, `@CacheEvict`, `@CachePut`


### Hands-on
- Add basic authentication and caching to your API

---

## 🔹 5. Testing & Microservices Concepts

### Topics
- **Unit Testing**
  - `@SpringBootTest`, `@MockBean`
  - JUnit + Mockito
- **Integration Testing**
  - MockMVC, H2 for tests
- **Microservices**
  - REST communication (`RestTemplate`, `WebClient`)


---

## 🔹 6. Interview Patterns & Prep

### Topics
- Common Interview Qs:
  - Difference between `@Component`, `@Service`, `@Repository`
  - Lazy vs Eager loading
  - Bean scopes
  - `@RestController` vs `@Controller`
  - Pros and cons of Spring Boot over Spring


---

## Tips
- Maintain a small **CRUD mini-project** throughout the plan (add new concepts as you learn).  
- Use **H2 DB** for quick prototyping, switch to **MySQL/Postgres** for real DB experience.  
---


____________________________

Comtroller 




@RestController

Purpose: Marks a class as a REST API controller.
Usage: Handle HTTP requests like GET, POST, PUT, DELETE.



@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return userService.getUserById(id);
    }
}

____________

@Service

Purpose: Marks a service layer class — contains business logic.
Spring registers it as a Spring Bean automatically.


@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public User getUserById(Long id) {
        return userRepository.findById(id).orElse(null);
    }
}

_________________

@Repository

Purpose: Marks a DAO/repository class — interacts with the database.
Adds exception translation: Converts JPA or JDBC exceptions into Spring’s DataAccessException hierarchy.

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
}



__________________


Spring Boot makes it easy to create stand-alone, production-grade Spring-based applications that you can "just run".
Add dependencies in pom.xml and configure application.yml to set the app configs.


______________



Create Entities:


public interface ProductRepository extends JpaRepository<Product, Long> {
    // Spring Data JPA generates basic CRUD automatically
}


Basic CRUD with ProductRepository

productRepository.save(product);
productRepository.findById(1L);
productRepository.findAll();
productRepository.deleteById(2L);
productRepository.count();

____________________

Custom Query Methods:

Spring Data can generate queries from method names.


public interface ProductRepository extends JpaRepository<Product, Long> {
    List<Product> findByName(String name);
    List<Product> findByPriceLessThan(double price);
    List<Product> findByCategoryAndPriceLessThan(String category, double price);
}



Translates to SQL:


SELECT * FROM product WHERE name = ?;
SELECT * FROM product WHERE price < ?;
SELECT * FROM product WHERE category = ? AND price < ?;
Custom Queries (JPQL)
If the method name is too complex, use @Query.

@Param is used in @Query to bind method parameters to query parameters.




public interface ProductRepository extends JpaRepository<Product, Long> {

    @Query("SELECT p FROM Product p WHERE p.name LIKE %:keyword%")
    List<Product> searchByName(@Param("keyword") String keyword);

    @Query(value = "SELECT * FROM product WHERE price > :price", nativeQuery = true)
    List<Product> findExpensive(@Param("price") double price);
}



SQL works on tables & columns.
JPQL works on entities & their fields.

JPQL is object-oriented and database-agnostic, while SQL is tied to the database schema.



___________________

## Transactions

All repository methods are already wrapped with @Transactional by Spring Data:

Write methods (save, delete) → transactional with commit
Read methods (findBy...) → transactional with read-only

Most of the time, you don’t need to manually add @Transactional.



________________________

Common Annotations

@SpringBootApplication → main entry point, enables auto-configuration
@Entity → JPA entity
@Id, @GeneratedValue → primary key
@Column → configure column details
@Repository → persistence layer (JpaRepository already adds this)
@Service → service layer
@RestController → REST APIs
@Data → generates getters, setters, toString(), equals(), hashCode()
@Builder → enables builder pattern



@Builder
@Data
public class Product {
    private Long id;
    private String name;
    private Double price;
}



Usage:
Product p = Product.builder()
                   .id(1L)
                   .name("Laptop")
                   .price(899.0)
                   .build();


____________________

@Autowired
Spring’s way of doing Dependency Injection (DI)
Injects required bean wherever you need it.



@Service
public class OrderService {

    private final ProductRepository productRepository;
    private final PaymentService paymentService;
    private final NotificationService notificationService;

    @Autowired  
    public OrderService(ProductRepository productRepository,
                        PaymentService paymentService,
                        NotificationService notificationService) {
        this.productRepository = productRepository;
        this.paymentService = paymentService;
        this.notificationService = notificationService;
    }
}


_______________

Request Mappings
@RequestMapping, @GetMapping, @PostMapping → endpoint mappings

_______________


@Transactional
Defines transaction boundaries for DB operations

Ensures all-or-nothing behavior.

________________

@Transactional
public void transferMoney(Long fromAccount, Long toAccount, double amount) {
    accountRepository.debit(fromAccount, amount); // Step 1
    accountRepository.credit(toAccount, amount);  // Step 2
    // If Step 2 fails, Step 1 is rolled back automatically
}




______________________



MVC (Model–View–Controller):


Model → data (entities, business objects, database layer)
View → UI (HTML, JSON, etc.)
Controller → logic that connects model and view

________________

DAO
Repository interface handles CRUD
DAO = Data Access Object, separates persistence logic from business logic
Usually, no extra DAO class is needed with Spring Data JPA


_________________________

Logging Levels:


TRACE	Very detailed, usually for deep debugging
DEBUG	Debug info for developers
INFO	General runtime info, like “server started”
WARN	Something unexpected but not fatal
ERROR	Something broke, must fix




Logging Example (SLF4J)


import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

@Service
public class ProductService {

    private static final Logger logger = LoggerFactory.getLogger(ProductService.class);

    public void addProduct(Product product) {
        logger.info("Adding product: {}", product.getName());
        logger.debug("Product details: {}", product);
    }
}


____________________

Lombok shortcut with @Slf4j:


import lombok.extern.slf4j.Slf4j;

@Slf4j
@Service
public class ProductService {

    public void addProduct(Product product) {
        log.info("Adding product: {}", product.getName());
        log.debug("Product details: {}", product);
    }
}


LoggerFactory.getLogger(ProductService.class) creates a logger instance for the class

private static final → shared, constant, class-level



# Set global log level
logging.level.root=INFO



# Enable DEBUG logs globally
logging.level.root=DEBUG


_____________

Example Entity with Annotations

@AllArgsConstructor
@NoArgsConstructor
@Builder
@Data
@Entity
@Table(name = "price", schema = "service_prices")
public class Price {

    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "sequence_price_generator")
    @GenericGenerator(
        name = "sequence_price_generator",
        strategy = "org.hibernate.id.enhanced.SequenceStyleGenerator",
        parameters = {
            @Parameter(name = "sequence_name", value = "service_prices.price_id_seq"),
            @Parameter(name = "initial_value", value = "1000"),
            @Parameter(name = "increment_size", value = "1")
        }
    )
    private Long id;

    @Column(name = "book_id", nullable = false)
    private long bookId;

    @Column(nullable = false, precision = 10, scale = 4)
    private BigDecimal price;
}





__________________

@Configuration
@PropertySource("classpath:application.properties") // load the properties file
public class AppConfig {

    @Value("${db.driver}")
    private String driver;

    @Value("${db.url}")
    private String url;

    @Value("${db.username}")
    private String username;

    @Value("${db.password}")
    private String password;

    @Bean
    public DataSource dataSource() {
        BasicDataSource ds = new BasicDataSource();
        ds.setDriverClassName(driver);
        ds.setUrl(url);
        ds.setUsername(username);
        ds.setPassword(password);
        return ds;
    }
}
_________________________


Using @Value with a properties file

Create application.properties (in src/main/resources):

db.driver=com.mysql.cj.jdbc.Driver
db.url=jdbc:mysql://localhost:3306/testdb
db.username=root
db.password=password


_______________________



Spring 



<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans 
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/testdb"/>
        <property name="username" value="root"/>
        <property name="password" value="password"/>
    </bean>

</beans>


______________________________



# H2 In-Memory Database and Production Databases

## 1. H2 In-Memory Database

**Purpose:**  
- Useful for **development and testing**.  
- Lightweight, in-memory, no installation required.  
- Resets data every time the application restarts.  

**Production Databases:**  
- MySQL/PostgreSQL: Persistent, production-ready.  
- Spring Boot automatically configures `DataSource` and JPA if you provide dependencies and `application.properties`.

> “For development/testing, Spring Boot often uses H2 in-memory database. For production, it integrates with MySQL or PostgreSQL via JDBC"

---

### Dependency

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```


application.properties

```
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
```


Access H2 Console
```
Open browser → http://localhost:8080/h2-console
JDBC URL: jdbc:h2:mem:testdb
Username: sa
Password: (leave empty)
```

___________________________________


# JPA vs JDBC Template in Spring

## JPA (Java Persistence API)

JPA is a Java specification for **object-relational mapping (ORM)**. It defines a standard way to map Java objects (entities) to relational database tables. It is **not an implementation** — you need an ORM tool like Hibernate to actually perform the database operations.

### Why JPA?
- Simplifies database access in Java applications.  
- Avoids writing boilerplate SQL for basic CRUD operations.  
- Supports transactions, caching, and lazy/eager loading.  
- Provides a **DB-agnostic** way to interact with relational databases.

### Using JPA with Spring Data
- Repository interfaces usually extend `JpaRepository` or `CrudRepository`.  
- SQL is generated automatically; manual SQL is only needed with `@Query`.  
- Spring Data JPA generates the implementation at runtime.



```
@Repository
public interface UserRepository extends JpaRepository<User, Long> {

    // Optional: custom queries
    List<User> findByUsername(String username);

    @Query("SELECT u FROM User u WHERE u.email = :email")
    User findByEmail(@Param("email") String email);
}
```
__________________



# JDBC Template (Classic JDBC) in Spring

If you don’t use JPA, you can use `JdbcTemplate` for **direct SQL queries**.  
- You need to write SQL manually.  


```
@Repository
public class UserRepository {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public User findById(Long id) {
        return jdbcTemplate.queryForObject(
            "SELECT * FROM users WHERE id = ?",
            new Object[]{id},
            (rs, rowNum) -> new User(rs.getLong("id"), rs.getString("username"))
        );
    }

    public void save(User user) {
        jdbcTemplate.update(
            "INSERT INTO users(username,email) VALUES(?,?)",
            user.getUsername(), user.getEmail()
        );
    }
}
```





| Feature               | JDBC                                                      | JPA                                                  |
|-----------------------|-----------------------------------------------------------|------------------------------------------------------|
| Definition            | Java API for executing SQL queries directly              | Java Persistence API — ORM standard for mapping Java objects to DB tables |
| Abstraction           | Low-level, manual SQL                                     | High-level, works with entities and objects         |
| SQL Writing           | Required for all operations                               | Mostly optional (auto-generated by JPA/Hibernate)  |
| Mapping               | Manual mapping of ResultSet to objects                   | Automatic mapping via `@Entity`, `@Id`, etc.       |
| CRUD                  | Write SQL for every operation                             | Provided by `JpaRepository` / `CrudRepository`     |
| Transaction Handling  | Manual using `Connection` or Spring `@Transactional`     | Simplified with Spring `@Transactional`            |
| Boilerplate Code      | High                                                      | Low — fewer lines of code                            |
| Portability           | SQL-specific; harder to switch DBs                        | DB-agnostic; easier to switch databases            |
| Performance           | Slightly faster (no abstraction)                          | Slightly slower due to ORM layer (negligible in most apps) |




_________________
_________________



## Actuator : Health checks, metrics, monitoring endpoints


Useful for monitoring, alerting, and troubleshooting in production environments.


Spring Boot Actuator provides built-in **production-ready features** to help monitor and manage your application.

## Key Features
- **Health Checks:** Monitor application health (`/actuator/health`).  
- **Metrics:** Track application metrics like memory usage, JVM stats, HTTP requests (`/actuator/metrics`).  
- **Monitoring Endpoints:** Access info about beans, environment, and more (`/actuator/beans`, etc.).  



Example Usage

Access health endpoint: http://localhost:8080/actuator/health
Access metrics endpoint: http://localhost:8080/actuator/metrics
Access beans endpoint: http://localhost:8080/actuator/beans

______________________
_______________________


## Difference between `@Component`, `@Service`, `@Repository`

All three are stereotype annotations and register beans with the Spring container.
Use @Component for generic beans, @Service for business logic, and @Repository for persistence layer with built-in exception translation.”

_______________________

 ## Bean scopes
  - `@RestController` vs `@Controller`

| Feature     | @Controller                                                                              | @RestController                                                                 
|-------------|----------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------
| Purpose     | Marks a class as a **web controller** (MVC pattern).                                     | Marks a class as a **REST API controller**.                                     
| Return Type | Usually returns **views** (HTML/JSP/Thymeleaf). Needs `@ResponseBody` toreturn JSON/XML. | Returns data directly as **JSON/XML** (because it combines `@Controller + @ResponseBody`). 
| Use Case    | Traditional MVC web apps with views.                                                     | RESTful APIs (most common in Spring Boot).                                      

_____

Pros and Cons of Spring over Spring Boot


## Overview
Spring gives you full control but requires lots of configuration, while Spring Boot is opinionated and reduces boilerplate by offering auto-configuration, starters, and embedded servers. In short, Spring Boot makes Spring development faster and easier.

---

## Spring Boot Pros
- Rapid development — less setup, fewer lines of code.  
- Built-in auto-configuration and starter dependencies.  
- Standalone apps with embedded servers.  
- Great for microservices and cloud-native development.  
- Spring Boot favors convention over configuration.  
- Spring Boot is opinionated but still customizable.

---

## Spring (Core) Pros
- Very flexible — you can configure everything exactly how you want.  
- Good for large, complex, enterprise-grade applications.  
- Mature ecosystem with lots of extensions.





| **Aspect**                | **Spring (Core Spring Framework)**                                                  | **Spring Boot**                                                                                      |
| ------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Setup & Configuration** | Requires a lot of **manual configuration** (XML or Java config).                    | Provides **auto-configuration** and sensible defaults, reducing boilerplate.                         |
| **Dependencies**          | You need to manage and add each dependency manually (e.g., web, JPA, validation).   | Provides **starter dependencies** (`spring-boot-starter-web`, `spring-boot-starter-data-jpa`, etc.). |
| **Deployment**            | Typically needs to be deployed on an **external server** (Tomcat, JBoss, WebLogic). | Comes with an **embedded server** (Tomcat/Jetty/Undertow), so apps run standalone (`java -jar`).     |
| **Learning Curve**        | Steeper — more concepts to understand upfront.                                      | Easier to start with — opinionated defaults and less setup.                                          |
| **Flexibility**           | Very flexible but verbose — you decide everything.                                  | Opinionated, but still customizable. Prioritizes **convention over configuration**.                  |
| **Microservices**         | Possible but requires lots of manual setup for each service.                        | Built with **microservices** in mind — easy integration with Spring Cloud, Actuator, etc.            |
| **Code Boilerplate**      | Higher — need to write more config, XML, boilerplate classes.                       | Much lower — Boot handles wiring and default configs.                                                |
| **Control**               | Full control over every aspect of configuration.                                    | Slightly less control (you can override, but Boot sets defaults).                                    |
| **Use Case**              | Enterprise apps where fine-grained control is required.                             | Modern apps, microservices, quick prototypes, cloud-ready apps.                                      |





_____________________________


Lazy vs Eager loading


Eager = upfront loading (more memory, possible over-fetching).
Lazy = load on demand (efficient, but extra queries).



| Aspect        | Eager Loading                                                                         | Lazy Loading                                                                               |
| ------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Definition    | Loads associated entities **immediately** with the parent entity.                     | Loads associated entities **only when accessed** (on-demand).                              |
| Performance   | May load unnecessary data, which can slow down performance if associations are large. | Faster initial load since only the main entity is fetched.                                 |
| Memory Usage  | Higher — since all related data is fetched upfront.                                   | Lower — only needed data is loaded when required.                                          |
| Use Case      | Useful when you **always need related entities**.                                     | Useful when related entities are **not always needed** .                                   |
| Configuration | `@OneToMany(fetch = FetchType.EAGER)` or default in some mappings.                    | `@OneToMany(fetch = FetchType.LAZY)` (default in many cases like collections).             |
| SQL Queries   | Often results in **JOINs** at query time.                                             | triggers **separate SQL queries** when accessed.                                           |

____________
