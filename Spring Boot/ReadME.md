#  Spring Boot

**Spring Boot fundamentals, persistence, REST APIs, advanced features, testing, and interview prep**.  


---

## 🔹 1. Core Spring Boot Concepts (Days 1–3)

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

## 🔹 2. Spring Boot Data & Persistence (Days 4–6)

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

## 🔹 3. REST APIs & Exception Handling (Days 7–9)

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

## 🔹 4. Spring Boot Advanced Features (Days 10–13)

### Topics
- **Security**
  - Basics of Spring Security
  - `@EnableWebSecurity`, `WebSecurityConfigurerAdapter`
  - JWT Authentication (simple flow)
- **Caching**
  - `@Cacheable`, `@CacheEvict`, `@CachePut`
- **Actuator**
  - Health checks, metrics, monitoring endpoints

### Hands-on
- Add basic authentication and caching to your API

---

## 🔹 5. Testing & Microservices Concepts (Days 14–16)

### Topics
- **Unit Testing**
  - `@SpringBootTest`, `@MockBean`
  - JUnit + Mockito
- **Integration Testing**
  - MockMVC, H2 for tests
- **Microservices**
  - REST communication (`RestTemplate`, `WebClient`)
  - Feign clients (optional, for extra edge)

### Hands-on
- Write unit and integration tests for your API
- Experiment with inter-service calls using `RestTemplate`

---

## 🔹 6. Interview Patterns & Prep (Days 17–20)

### Topics
- Common Interview Qs:
  - Difference between `@Component`, `@Service`, `@Repository`
  - Lazy vs Eager loading
  - Bean scopes
  - `@RestController` vs `@Controller`
  - Pros and cons of Spring Boot over Spring
- Revision of your mini-project
- Be ready to discuss design choices

### Hands-on
- Revise CRUD API
- Practice interview-style Spring Boot questions
- Solve coding tasks involving service-layer logic

---

## ✅ Tips
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



DAO
Repository interface handles CRUD
DAO = Data Access Object, separates persistence logic from business logic
Usually, no extra DAO class is needed with Spring Data JPA




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

Logging Configuration (log4j2 / Spring Boot)
properties



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









