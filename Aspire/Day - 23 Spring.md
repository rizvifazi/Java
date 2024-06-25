
*Date : 06.17.2024*

8. Instead of writing queries in repository interface, we can write queries in entity class and we can refer by their name
    JPAQL - `@NamedQuery`
    SQL - `@NamedNativeQuery`
    
```java
List<Employee> fetchEmpBySalary(double sal);
List<Employee> fetchEmpBySalary1(@Param("abc")double sal);

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


List<Employee> l=empRepo.fetchEmpBySalary(20000.0);

List<Employee> l=empRepo.fetchEmpBySalary1(20000.0);

9. For Sorting purpose we have Sort class 

List<Employee> findByDeptOrderBySalaryDesc(String dname);  //custom JPA method
              
List<Employee> findByDept(String dname, Sort s);

List<Employee> l=empRepo.findByDept("HR",Sort.by("salary").descending());
List<Employee> l1=empRepo.findByDept("HR",Sort.by("salary").ascending());
```

10. Consider we have entity class with some 100 properties, but we need to display only 10 properties 
    Consider we have employee table, now we want to display total number of male and female employees so the output would be

```mysql
mysql> select count(gender) as "Total Count", gender from empl2024 group by gender;
+-------------+--------+
| Total Count | gender |
+-------------+--------+
|           5 | male   |
|           2 | female |
+-------------+--------+
2 rows in set (0.00 sec)
```

```java
@Query("select count(gender) as "Total Count", gender from empl2024 group by gender")
List<Employee> countGenderWise(); //- wrong - it will display all properties


@Query("select count(gender) as "Total Count", gender from empl2024 group by gender")
List<Object[]> countGenderWise(); //- correct, but it is not practise to return an Object 

@Query("select count(gender) as "Total Count", gender from empl2024 group by gender")
Map<Integer,String> countGenderWise(); // - wrong, because Spring data jpa dosent support Map as return type


Constructor method //- used when we want to display only specific properties from entity class
```

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
public class GenderCount {
    private long count;
    private String gender;
}

@Query("select new com.pack.SpringBootJPA.GenderCount(count(e.gender),e.gender) from Employee e group by e.gender")
              List<GenderCount> countGenderWise();

List<GenderCount> l3=empRepo.countGenderWise();
l3.forEach(System.out::println);
```

# Integrate Spring Boot and Spring data JPA to develop CRUD appl
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
`@RequestBody` - maps the input json request to the domain object (ie) movie object

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