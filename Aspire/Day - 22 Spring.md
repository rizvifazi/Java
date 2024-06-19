
*Date : 06.14.2024*


## Springboot Interceptors
- used to intercept client request and response
- Interceptors are similar to Filters(servlet), but interceptors are applied to the request that are sending to the controller
- We have to implement HandlerInterceptor interface and override 3 methods

  a. preHandle() - perform any operation before sending request to controller
  b. postHandle() - perform any operation before sending response to client
  c. afterCompletion() - perform any operation after completing request and response
  
```java
@RestController
@Log4j2
public class EmployeeController {

              @GetMapping("/emp")
              public String getEmpInfo() {
                             log.info("Inside Employee controller");
                             return "Employees are working";
              }
}


@Component
@Log4j2
public class TimerInterceptor implements HandlerInterceptor{
     
               @Override
            public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
                                                          throws Exception {
                                           log.info("Inside preHandle");
                                           request.setAttribute("startTime", System.currentTimeMillis());;
                                           return true;
                             }
              
               @Override
              public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler,
                                           ModelAndView modelAndView) throws Exception {
                             // TODO Auto-generated method stub
                             log.info("Inside postHandle");
              }
              
               @Override
              public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)
                                           throws Exception {
                             // TODO Auto-generated method stub
                             log.info("Inside afterCompletion");
                             long totalTime=System.currentTimeMillis()-(long)request.getAttribute("startTime");
                             System.out.println("Total time taken to execute is "+totalTime);
              }
}


@Configuration
public class EmployeeConfig implements WebMvcConfigurer{
              
              @Autowired
              TimerInterceptor timerInterceptor;

              @Override
              public void addInterceptors(InterceptorRegistry registry) {
                             //registry.addInterceptor(timerInterceptor); //this interceptor will be invoked for all controller prg
                      registry.addInterceptor(timerInterceptor).addPathPatterns("/emp");
              }
}
```


# JDBC
# JPA

## Spring Data JPA
- Used to persist data into database
- It is a library that adds as an extra layer of abstraction on top of JPA Providers, mainly to reduce the work of developers 

### JPA Providers 
- vendors that provide implementation of JPA specification like Hibernate, iBatis, Toplink etc. 

### JPA Specification 
- provide mapping of entity class with column of database table using @Entity, @Table, @Id etc.

#### 3 layers

##### 1. Spring Data JPA  - create JPA Repository - 2 interface
a. `JpaRepository<Entityclassname,datatype of PK>` interface - used to perform CRUD and batch operation 
- `T getById(int id)` - Deprecated
- `T getOne(int id)` - Deprecated 
- `T getReferenceById(int id)` - fetch single object 
- `List<T> findAll()` - return multiple object
- `T saveAndFlush(T t)` - used to save single object
- `void saveAllAndFlush(Iterable)` - store multiple object inside db
- `void deleteAllByIdInBatch(Iterable)`
- `void deleteAllInBatch()`
b. `JpaSpecificationExecutor<Entityclassname>` interface - used to retrieve data based on some condition

##### 2. Spring data commons layer - 3 interface
a. `Repository<Entityclassname,datatype of PK>` interface - marker interface
b. `CrudRepository<Entityclassname,datatype of PK>` interface - used to perform only CRUD operation
 - `T save(T t)` - store single object 
 - `void saveAll(Iterable)` - store multiple object
 - `Optional findById(int id)` - return single object
 - `Iterable findAll()` - return multiple object
 - `boolean existsById(int id)`
 - `void deleteById(int id)` - delete single object based on id
 - `void delete(T t)` - delete single object
 - `void deleteAll()`
c. `PagingAndSortingRepository<Entityclassname,datatype of PK>` interface - used for paging and sorting purpose

##### 3. JPA Providers - vendors that provide implementation of JPA specification like Hibernate, iBatis, Toplink etc 


Repository interface
  extends 
CrudRepository interface
  extends
PagingAndSortingRepository interface
   extends
JpaRepository interface

1. Create spring boot project with spring `data jpa`, `mysql driver`, `lombok` dependency 

2. Configure db info in `application.properties`

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/jpa
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.jpa.show-sql = true
spring.jpa.hibernate.ddl-auto = update
#dialect will generate the query based on particular db
spring.jpa.database-platform=org.hibernate.dialect.MySQL5Dialect
```

3. Create entity class
```java
@Entity
@Table(name="empl2024")
@Data
@NoArgsConstructor
@AllArgsConstructor
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

4. Create repository interface
```java
public interface EmployeeRepository extends JpaRepository<Employee, Integer>{

}
```
5. 
```java
@SpringBootApplication
public class SpringBootJpaApplication implements CommandLineRunner {
              
              @Autowired
              EmployeeRepository empRepo;

              public static void main(String[] args) {
                             SpringApplication.run(SpringBootJpaApplication.class, args);
              }

              @Override
              public void run(String... args) throws Exception {
                             //insertEmployee();
                             //fetchEmployee(104);
                             //fetchAllEmployees();
                             //updateEmployee(104);
                             //deleteEmployee(104);
                             customJPAMethod();
              }

              private void customJPAMethod() {
                             List<Employee> l=empRepo.findByDept("HR");
                             l.forEach(System.out::println);
                             
                             List<Employee> l1=empRepo.queryByNameLike("R%");
                             l1.forEach(System.out::println);
                             
                             List<Employee> l2=empRepo.findByNameContainingOrDeptContainingAllIgnoreCase("AM", "MIN");
                             l2.forEach(System.out::println);
              }

              private void deleteEmployee(int i) {
                             if(empRepo.existsById(i)) {
                                           //empRepo.deleteById(i);
                                           Employee e=empRepo.findById(i).get();
                                           empRepo.delete(e);
                             }
              }

              private void updateEmployee(int i) {
        if(empRepo.existsById(i)) {
               Employee e=empRepo.findById(i).get();
               e.setSalary(22000.0);
               empRepo.save(e);
        }
              }

              private void fetchAllEmployees() {
                             List<Employee> l=empRepo.findAll();
                             l.forEach(System.out::println);
              }

              private void fetchEmployee(int i) {
                             System.out.println(empRepo.findById(i).get());
              }

              private void insertEmployee() {
                             /*Employee e1=new Employee(100,"Ram","male",ram@gmail.com,"HR",25000.0);
                             empRepo.save(e1);*/
                             
                             List<Employee> l1=new ArrayList<>();
                             Employee e1=new Employee(101,"Sam","male",sam@gmail.com,"IT",35000.0);
                             l1.add(e1);
                             Employee e2=new Employee(102,"Saj","male",saj@gmail.com,"Sales",30000.0);
                             l1.add(e2);
                             Employee e3=new Employee(103,"Tam","male",tam@gmail.com,"HR",45000.0);
                             l1.add(e3);
                             Employee e4=new Employee(104,"Lam","female",lam@gmail.com,"Sales",25000.0);
                             l1.add(e4);
                             Employee e5=new Employee(105,"Lim","female",lim@gmail.com,"IT",40000.0);
                             l1.add(e5);
                             Employee e6=new Employee(106,"John","male",John@gmail.com,"HR",15000.0);
                             l1.add(e6);
                             empRepo.saveAll(l1);
              }

}
```


## Different ways to communicate with database

1. Using predefined methods
     - `T save(T t)` - store single object 
     - `void saveAll(Iterable) `- store multiple object
     - `Optional findById(int id)` - return single object based on id
     - `Iterable findAll(`) - return multiple object
     - `boolean existsById(int id)`
     - `void deleteById(int id)` - delete single object based on id
     - `void delete(T t)` - delete single object
     - `void deleteAll()`

2. Using Custom JPA Method 
     - derived methods used for fetching the data based on other properties except id
     - name of the method should starts with either `findBy/getBy/queryBy/readBy`
     - declare the custom jpa method inside repository interface, so spring data jpa will automatically write logic on behalf of user


```java
List<Employee> findByDept(String dname);
List<Employee> readByDeptAndSalaryLessThan(String dname,Double sal);

like - Pattern matching (%,_)

List<Employee> queryByNameLike(String name);
List<Employee> getByNameLikeAndSalaryGreaterThan(String name, Double sal);
List<Employee> findByDeptIsNull();
List<Employee> getByNameStartsWith(String name);
List<Employee> findByNameContainingOrDeptContainingAllIgnoreCase(String name,String dname)
```

3. Limiting the records based on custom JPA methods 
	- using First or Top keyword

```java
Employee findFirstByOrderBySalaryDesc();
Employee findTopByOrderBySalaryAsc();
List<Employee> findFirst3ByOrderBySalaryDesc();
List<Employee> findTop5ByOrderBySalaryAsc();
List<Employee> findFirst3ByDeptOrderBySalaryDesc(String dname);
```

4. Count the elements based on custom JPA method
   - using countBy 

```java
long countByDept(String dname);  long l=empRepo.countByDept("HR");  //2
long countByNameEndingWith(String name); 
      long l=empRepo.countByNameEndingWith("ar");
long countBySalaryGreaterThanEqual(double sal);
```

5. If we want to perform joins or subqueries then we cant use custom JPA method, in that case we have to write the queries using @Query
    - 2 types of query
   1. JPAQL - `@Query` - query the entity class
   2. SQL - `@Query` - query the table directly

```java
		@Query("select e from Employee e")  //JPAQL 
		List<Employee> fetchAllEmployee();
		  
		@Query(value="select * from empl2024",nativeQuery=true)  //SQL 
		List<Employee> fetchAllEmployee1();
```

6. Passing parameters to the queries - 2 ways

1. Positional parameter - using ? - `?1,?2,?3`...
```java
@Query("select e from Employee e where e.name like ?1 and e.salary=?2")
List<Employee> findEmpByNameAndSalary(String name, Double sal);

List<Employee> l1=empRepo.findEmpByNameAndSalary("R%",20000.0);
```

2. Named Parameter - using : - `:a, :abc, :one`

`@Param` - used to assign value to named parameter
```java
@Query("select e from Employee e where e.name like :ab and e.salary=:xy")
List<Employee> findEmpByNameAndSalary1(@Param("ab")String name,@Param("xy") Double sal);

List<Employee> l1=empRepo.findEmpByNameAndSalary1("R%",20000.0);
```

7. If we want to perform DML operations(insert,update,delete) using `@Query`, apart from `@Query` we have to provide 2 more annotation `@Modifying`, `@Transactional`
```java
	  @Modifying
	  @Transactional
	  @Query("update Employee e set e.salary=e.salary+e.salary*:percent/100 where e.dept=:dept")
	  int updateSalary(@Param("dept")String dname,@Param("percent")double percentage);
```

