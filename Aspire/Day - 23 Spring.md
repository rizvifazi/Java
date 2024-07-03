
*Date : 06.17.2024*

8. Instead of writing queries in repository interface, we can write queries in entity class and we can refer by their name
    JPAQL - `@NamedQuery`
    SQL - `@NamedNativeQuery`


`IEmployeeRepository.java` interface
```java
List<Employee> fetchEmpBySalary(double sal);
List<Employee> fetchEmpBySalary1(@Param("xyz") double sal);
```

`Employee.java` entity class
```java
@Entity
@Table(name="empl2024")
@Data
@NoArgsConstructor
@AllArgsConstructor
@NamedQuery(name="Employee.fetchEmpBySalary",
       query="select e from Employee e where e.salary=?1")  
@NamedNativeQuery(name="Employee.fetchEmpBySalary1", 
       query="select * from empl2024 e where e.salary=:abc",resultClass=Employee.class)
public class Employee {
              @Id
    private Integer id;
    private String name;
    private String gender;
    private String email;
    private String dept;
    private Double salary;
}

```


Custom Method in `SpringBootApplication.java`
```java
private void customMethod() {
		List<Employee> l = empRepo.fetchEmpBySalary(30000.00) ;
		l.forEach(System.out::println);
		
		List<Employee> ls = empRepo.fetchEmpBySalary1(30000.00) ;
		ls.forEach(System.out::println);
}
```

Console Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.salary=?
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=30000.0)
Employee(id=102, name=Saj, gender=male, email=saj@gmail.com, department=Sales, salary=30000.0)
Hibernate: select * from empl2024 where salary = ?
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=30000.0)
Employee(id=102, name=Saj, gender=male, email=saj@gmail.com, department=Sales, salary=30000.0)
```


9. For Sorting purpose we have `Sort` class 
```java
List<Employee> findByDeptOrderBySalaryDesc(String dname);  //custom JPA method



List<Employee> findByDepartmentt(String dname, Sort s); // in IEmployeeRepository interface

List<Employee> l=empRepo.findByDepartmentt("HR",Sort.by("salary").descending()); // in Main class
List<Employee> l1=empRepo.findByDepartment("HR",Sort.by("salary").ascending()); // in Main class
```

Console Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department=? order by e1_0.salary desc
Employee(id=103, name=Tam, gender=male, email=tam@gmail.com, department=HR, salary=54000.0)
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=30000.0)
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=18000.0)
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department=? order by e1_0.salary
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=18000.0)
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=30000.0)
Employee(id=103, name=Tam, gender=male, email=tam@gmail.com, department=HR, salary=54000.0)
```

10. Consider we have entity class with some 100 properties, but we need to display only 10 properties 
    Consider we have employee table, now we want to display total number of male and female employees so the output would be

```mysql
mysql> select count(gender) as "Total Count", gender from empl2024 group by gender;
+-------------+--------+
| Total Count | gender |
+-------------+--------+
|           5 | male   |
|           1 | female |
+-------------+--------+
2 rows in set (0.00 sec)
```

```java
@Query("select count(gender) as "Total Count", gender from empl2024 group by gender")
List<Employee> countGenderWise(); //- wrong - it will display all properties, all columns 


@Query("select count(gender) as "Total Count", gender from empl2024 group by gender")
List<Object[]> countGenderWise(); //- correct, but it is not a good practice to return an Object 

@Query("select count(gender) as "Total Count", gender from empl2024 group by gender")
Map<Integer,String> countGenderWise(); // - wrong, because Spring data jpa dosent support Map as return type

```

#### Constructor method 
- used when we want to display only specific properties from entity class

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
public class GenderCount {
    private long count;
    private String gender;
}

//assigning to constructor using new keyword
@Query("select new com.pack.SpringBootJPA.GenderCount(count(e.gender),e.gender) from Employee e group by e.gender")
              List<GenderCount> countGenderWise();

List<GenderCount> l3=empRepo.countGenderWise();
l3.forEach(System.out::println);

```

Console Output:
```cmd
Hibernate: select count(e1_0.gender),e1_0.gender from empl2024 e1_0 group by e1_0.gender
GenderCount(count=5, gender=male)
GenderCount(count=1, gender=female)
```


---


# Integrate Spring Boot and Spring data JPA to develop CRUD application
1. Create Spring boot project with spring web, spring data jpa, h2 db, lombok dependency 

2. Configure db info in `application.properties`
```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto= update

spring.h2.console.enabled=true
# default path: h2-console
spring.h2.console.path=/h2-ui

spring.mvc.pathmatch.matching-strategy = ANT_PATH_MATCHER
server.port=2000
```

`application.yml`
```yaml
spring:
  datasource:
    url: jdbc:h2:mem:testdb
    driverClassName: org.h2.Driver
    username: sa
    password:  # Password left empty

  jpa:
    show-sql: true
    hibernate:
      ddl-auto: update

  h2:
    console:
      enabled: true
      path: /h2-ui  # Custom path for H2 console

  mvc:
    pathmatch:
      matching-strategy: ANT_PATH_MATCHER

server:
  port: 2000

```


3. Create entity class 
```java
@Entity
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Movie {
   @Id
   private Integer id;
   private String name;
   private String language;
   private String type;
   private Integer rating;
}
```

4. Create repository interface
```java
public interface MovieRepository extends JpaRepository<Movie, Integer>{

}
```

5. Create controller program

`@ResponseEntity` - represent the whole response of entity entity 
`@RequestBody` - maps the input JSON request to the domain object (ie) movie object

client request - controller - service - repository 
```java
@RestController
@RequestMapping("/api")
public class MovieController {
              
              @Autowired
              MovieService movieService;

              @PostMapping("/movie")
              public ResponseEntity<Movie> createMovie(@RequestBody Movie movie) {
                             try {
                                           Movie savedMovie=movieService.createMovie(movie);
                                           return new ResponseEntity<Movie>(savedMovie, HttpStatus.CREATED);
                             }catch(Exception e) {
                                           return new ResponseEntity<>(null, HttpStatus.INTERNAL_SERVER_ERROR);
                             }
              }
              
              @GetMapping("/movie")
              public ResponseEntity<List<Movie>> getAllMovies() {
                             try {
                                           List<Movie> list=movieService.getAllMovies();
                                           if(list.isEmpty()) {
                                                          return new ResponseEntity<>(HttpStatus.NO_CONTENT);
                                           }
                                           return new ResponseEntity<>(list,HttpStatus.CREATED);
                             }catch(Exception e) {
                                           return new ResponseEntity<>(null, HttpStatus.INTERNAL_SERVER_ERROR);
                             }
              }
              
              @GetMapping("/movie/{movieId}")
              public ResponseEntity<Movie> getMovieById(@PathVariable("movieId") Integer mid) {
                             try {
                                           Movie movie=movieService.getMovieById(mid);
                                           if(movie!=null)
                                                          return new ResponseEntity<>(movie, HttpStatus.CREATED);
                                           else
                                                          return new ResponseEntity<>(HttpStatus.NOT_FOUND);
                             }catch(Exception e) {
                                           return new ResponseEntity<>(null, HttpStatus.INTERNAL_SERVER_ERROR);
                             }
              }
}

```

6. Create service program

```java
@Service
public class MovieService {
              
              @Autowired
              MovieRepository movieRepo;

              public Movie createMovie(Movie movie) {
                             return movieRepo.save(movie);
              }
              
              public List<Movie> getAllMovies() {
                             return movieRepo.findAll();
              }
              
              public Movie getMovieById(Integer id) {
                             return movieRepo.findById(id).get();
              }
}
```

7. To give request and check whether appl is working or not, we can use either Postman or Soap UI tools. instead Spring boot have provided with Swagger to test ur appl
    Swagger is a documentation tool where it will document all the request and provides an UI to check 

```xml
<dependency>
	  <groupId>org.springdoc</groupId>
	  <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
	  <version>2.2.0</version>
</dependency>
```

8. Start the appl and the access Swagger UI using 
http://localhost:2000/swagger-ui/index.html

To check h2 database http://localhost:2000/h2-ui


---
GPT

Here's a breakdown of the steps to easily create a CRUD application in Java Spring Boot:

**1. Project Setup:**

- Use Spring Initializr ([https://start.spring.io/](https://start.spring.io/)) to generate a Spring Boot project.
- Choose a project type (e.g., Maven) and provide a Group and Artifact ID.
- Select the following dependencies:
    - Spring Web - Enables building web applications.
    - Spring Data JPA - Simplifies data access with JPA.
    - (Optional) H2 Database - An in-memory database for development (consider a production-grade database later).
- Click "Generate" to download the project.

**2. Define Data Model:**

- Create a package for your model classes (e.g., com.example.crud.model).
- Define a Java class representing your entity (e.g., Product).
- Annotate the class with `@Entity` to mark it as a JPA entity.
- Define member variables for the entity's properties (e.g., id, name, description).
- Annotate each member variable with `@Column` to specify database column mappings (optional).
- Generate getters and setters for the member variables.

**3. Create Repository:**

- Create an interface in the repository package (e.g., com.example.crud.repository).
- Extend the interface with `CrudRepository<EntityType, IDType>`.
    - Replace `EntityType` with your actual entity class (e.g., Product).
    - Replace `IDType` with the data type of the entity's ID (e.g., Long).
- This interface provides essential CRUD methods (save, findById, findAll, deleteById, etc.).

**4. Implement Service Layer (Optional):**

- Create a service interface and implementation class (e.g., ProductService and ProductServiceImpl).
- The service layer can encapsulate business logic related to your entity.
- Inject the repository into the service to interact with the data.

**5. Develop REST Endpoints:**

- Create a Spring Boot controller class (e.g., ProductController).
- Annotate the class with `@RestController`.
- Use `@Autowired` to inject the service or repository (depending on your approach).
- Define methods for each CRUD operation with appropriate annotations:
    - `@PostMapping` - Create a new entity.
    - `@GetMapping("/{id}")` - Retrieve an entity by ID.
    - `@GetMapping` - Retrieve all entities (optional).
    - `@PutMapping("/{id}")` - Update an existing entity.
    - `@DeleteMapping("/{id}")` - Delete an entity by ID.

**6. Configure Database (Optional for H2):**

- Include the H2 database dependency if you chose it during project setup.
- Configure the datasource properties in `application.yml`:
    - `spring.datasource.url`: jdbc:h2:mem:testdb (in-memory database)
    - `spring.datasource.driverClassName`: org.h2.Driver
    - (Optional) `spring.datasource.username`: sa
    - (Optional) `spring.datasource.password`: (leave empty for H2)

**7. Enable H2 Console (Optional):**

- Configure H2 console access in `application.yml`:
    - `spring.h2.console.enabled: true`
    - (Optional) `spring.h2.console.path: /h2-ui` (custom path)

**8. Run the Application:**

- Use a Java IDE or command line to run the Spring Boot application (refer to IDE documentation).
- Access the H2 console (if enabled) at `http://localhost:2000/h2-ui` (or custom path) with credentials `sa` and an empty password (for H2).

**Additional Tips:**

- Use Spring Boot Actuator for monitoring and health checks.
- Implement error handling and validation for robust API endpoints.
- Consider using a proper database for production environments.
- Explore security aspects like authentication and authorization for real-world applications.

This provides a basic framework for creating a CRUD application with Spring Boot. You can customize it further based on your specific needs and complexity.

## Spring Boot CRUD with Movie Entity

Here's an example of a CRUD application in Spring Boot with a `Movie` entity:

**1. Model Class (Movie.java):**

Java

```
@Entity
public class Movie {

  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;

  private String title;
  private String genre;
  private int year;

  // Getters and Setters omitted for brevity
}
```

**2. Repository Interface (MovieRepository.java):**

Java

```
public interface MovieRepository extends CrudRepository<Movie, Long> {
}
```

**3. Service Layer (Optional - MovieService.java):**

Java

```
@Service
public class MovieService {

  @Autowired
  private MovieRepository movieRepository;

  public Movie saveMovie(Movie movie) {
    return movieRepository.save(movie);
  }

  public Movie getMovieById(Long id) {
    return movieRepository.findById(id).orElse(null);
  }

  // Implement other service methods as needed (update, delete, etc.)
}
```

**4. REST Controller (MovieController.java):**

Java

```
@RestController
@RequestMapping("/api/movies")
public class MovieController {

  @Autowired
  private MovieService movieService;

  @PostMapping
  public Movie createMovie(@RequestBody Movie movie) {
    return movieService.saveMovie(movie);
  }

  @GetMapping("/{id}")
  public Movie getMovie(@PathVariable Long id) {
    return movieService.getMovieById(id);
  }

  // Implement other CRUD endpoints using appropriate annotations
  // (e.g., @PutMapping, @DeleteMapping)
}
```

**5. application.yml (with H2 configuration):**

YAML

```
spring:
  datasource:
    url: jdbc:h2:mem:testdb
    driverClassName: org.h2.Driver
    username: sa
    password:
  jpa:
    show-sql: true
    hibernate:
      ddl-auto: update
  h2:
    console:
      enabled: true
```

**Additional Notes:**

- This example uses a service layer (optional) to encapsulate business logic related to movies.
- You can adjust the `Movie` class to include additional properties like director, cast, etc.
- Remember to implement the missing CRUD endpoints in the controller (`@PutMapping`, `@DeleteMapping`).
- This example uses H2 for development. Consider a proper database for production.

This example provides a starting point for building a CRUD application with Spring Boot and a Movie entity. You can expand on it by adding functionalities like searching, filtering, and pagination based on your requirements.



---


# SDLC
1. Estimation and Planning
2. Requirment and Analysis - what actually we are doing in the project 
3. Design - How we actually developing the project  - 40% 
4. Coding - convert algorithm into code - 20%
5. Testing - test whether the appl satisifes client requirement or not - 40%
6. Implementation
7. Maintainence 

## Unit Testing
- test the individual classes by the developers

`Junit` - unit testing in Java
`Nunit` - unit testing in .NET

Why Junit?
   - method by method we are going to test 

Junit 4 - Junit 4.13+Mockito-core-3.2.4-min - Min JDK1.5 - single jar file

Junit 5 - latest version - Jupiter(5th planet in solar system)
Junit 5 = Junit jupiter + mockito junit jupiter + junit vintage - min JDK1.8 - 3 jar files

### Assertions class 
- used to check expected and actual value 

1. Create maven Java project with Junit 5 dependency
```xml
<properties>
                 <maven.compiler.source>17</maven.compiler.source>
                 <maven.compiler.target>17</maven.compiler.target>
              </properties>
              <dependencies>
                             <dependency>
                                           <groupId>org.junit.jupiter</groupId>
                                           <artifactId>junit-jupiter</artifactId>
                                           <version>5.10.2</version>
                                           <scope>test</scope>
                             </dependency>
              </dependencies>
```

2. Create java prg
```java
public class ExampleUtil {
    public int add(int a,int b) {
               return a+b;
    }
}
```

3. Create test cases
```java
public class TestExampleUtil {

              @Test
              public void testAdd() {
                             ExampleUtil e=new ExampleUtil();
                             assertEquals(e.add(2, 3),4);
                             assertTrue("hello".length()==5);
                             assertFalse("hello".length()==4);
                             String s1="abcd";
                             String s2=null;
                             assertNotNull(s1);
                             assertNull(s2);
              }
}
```

## Lifecycle methods
1. `@BeforeAll` - the method with @BeforeAll will be invoked first before all testcases are executed - static method

2. `@AfterAll` - the method with @AfterAll will be invoked after all testcases are executed - static method

3. `@BeforeEach` - the method with @BeforeEach  will be invoked first before each testcases are executed 

4. `@AfterEach` - the method with @AfterEach  will be invoked first after each testcases are completed 

| Junit4            | Junit5           |
| ----------------- | ---------------- |
| 1. `@BeforeClass` | 1. `@BeforeAll`  |
| 2. `@AfterClass`  | 2. `@AfterAll`   |
| 3. `@Before`      | 3. `@BeforeEach` |
| 4. `@After`       | 4. `@AfterEach`  |
| 5. `@Ignore`      | 5. `@Disabled`   |

```java
public class TestExampleUtilLifeCycle {

              @BeforeAll
              public static void beforeAll() {
                             System.out.println("Executed before all testcases");
              }
              
              @AfterAll
              public static void afterAll() {
                             System.out.println("Executed after all testcases");
              }
              
              @BeforeEach
              public void beforeEach() {
                             System.out.println("Executed before each testcases");
              }
              
              @AfterEach
              public void afterEach() {
                             System.out.println("Executed after each testcases");
              }
              
              @Test
              public void test1() {
                             System.out.println("Inside test1()");
                             assertEquals(1,1);
              }
              @Test
              @Disabled("Ignoring test")
              public void test2() {
                             System.out.println("Inside test2()");
                             assertEquals(2,2);
              }
              @Test
              public void test3() {
                             System.out.println("Inside test3()");
                             assertEquals(3,3);
              }
}

```