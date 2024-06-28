
*Date : 06.14.2024*

## Springboot Interceptors
- used to intercept client request and response.
- Interceptors are similar to Filters(servlet), but interceptors are applied to the request that are sending to the controller.
- We have to implement `HandlerInterceptor` interface and override 3 methods.

  a. `preHandle()` - perform any operation before sending request to controller.
  b. `postHandle()` - perform any operation before sending response to client.
  c. `afterCompletion()` - perform any operation after completing request and response.

EmployeeController.java
```java
package com.pack.SpringInterceptors;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import lombok.extern.log4j.Log4j2;

@RestController
@Log4j2
public class EmployeeController {

	@GetMapping(value = "/emp")
	public String getEmployee() {
		log.info("This is inside the getemployee controller method");
		return "This is the employee class";
	}
}

```

TimeInterceptor.java
```java
package com.pack.SpringInterceptors;

import org.springframework.stereotype.Component;
import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import lombok.extern.log4j.Log4j2;

@Component //to inject as a bean
@Log4j2
public class TimerInterceptor implements HandlerInterceptor {

	@Override
	public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
			throws Exception {
		// TODO Auto-generated method stub
		log.info("Inside Prehandle methos");
		request.setAttribute("startTime", System.currentTimeMillis());
		return true;
	}

	@Override
	public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler,
			ModelAndView modelAndView) throws Exception {
		// TODO Auto-generated method stub
		log.info("Inside postHandle method");
	}

	@Override
	public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)
			throws Exception {
		// Check response time
		log.info("Inside afterCompletion Method");
		long totalTime=System.currentTimeMillis()-(long)request.getAttribute("startTime");
		log.info("Total Time taken " + totalTime);
	}

}

```

EmployeeConfig.java
```java
package com.pack.SpringInterceptors;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class EmployeeConfig implements WebMvcConfigurer{
	
	@Autowired
	TimerInterceptor timerInterceptor;
	
	@Override
	public void addInterceptors(InterceptorRegistry registry) {
		//registry.addInterceptor(timerInterceptor); // This intercepter will be invoked for all controller programs
		registry.addInterceptor(timerInterceptor).addPathPatterns("/emp"); // interceptor applies only to this path
	}

}
```

## Output:
Browser Output:
![[Pasted image 20240623230651.png]]

Console Output:
```cmd
[SpringInterceptors] [nio-2000-exec-1] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped to com.pack.SpringInterceptors.EmployeeController#getEmployee()
[SpringInterceptors] [nio-2000-exec-1] c.p.SpringInterceptors.TimerInterceptor : Inside Prehandle methos
[SpringInterceptors] [nio-2000-exec-1] c.p.S.EmployeeController : This is inside the getemployee controller method
[SpringInterceptors] [nio-2000-exec-1] m.m.a.RequestResponseBodyMethodProcessor : Using 'text/html', given [text/html, application/xhtml+xml, image/avif, image/webp, application/xml;q=0.9, */*;q=0.8] and supported [text/plain, */*, application/json, application/*+json]

[SpringInterceptors] [nio-2000-exec-1] m.m.a.RequestResponseBodyMethodProcessor : Writing ["This is the employee class"]
[SpringInterceptors] [nio-2000-exec-1] c.p.SpringInterceptors.TimerInterceptor : Inside postHandle method
[SpringInterceptors] [nio-2000-exec-1] c.p.SpringInterceptors.TimerInterceptor : Inside afterCompletion Method
[SpringInterceptors] [nio-2000-exec-1] c.p.SpringInterceptors.TimerInterceptor : Total Time taken 36
[SpringInterceptors] [nio-2000-exec-1] o.s.web.servlet.DispatcherServlet : Completed 200 OK
```


## Interceptors Uses
Interceptors are a powerful tool in Spring Boot that act as intermediaries between incoming requests and your application's controllers. They offer a centralized way to handle common tasks before a request reaches the controller (pre-handling) or after a response is generated (post-handling). Here are some of the key reasons why developers use interceptors in Spring Boot:

- **Reusability:** You can create an interceptor to handle a specific functionality, like authentication or logging, and then apply it to multiple controllers or endpoints. This reduces code duplication and keeps your controllers clean.
    
- **Security and Authentication:** A common use case for interceptors is to implement security checks. You can intercept requests in the `preHandle` method and validate tokens, user roles, or other credentials before allowing the request to proceed.
    
- **Logging and Monitoring:** By intercepting requests and responses, you can easily gather valuable data for logging and monitoring purposes. You can log details like request URLs, timestamps, user information, and response times within your interceptor (We implemented this).
    
- **Cross-cutting Concerns:** Interceptors are ideal for handling aspects that apply to many parts of your application, but aren't necessarily core functionalities of any specific controller. This can include things like adding headers to responses, validating data in requests, or performing cleanup tasks after handling a request.
    
In summary, interceptors in Spring Boot provide a flexible way to centralize common tasks, improve code organization, and implement essential functionalities like security and logging without cluttering your controllers.

---
# JDBC
# JPA
- Internally uses hibernate (ORM Tool)

## Spring Data JPA
- Used to persist data into database.
- It is a library that adds as an extra layer of abstraction on top of JPA Providers, mainly to reduce the work of developers.

### JPA Providers 
- vendors that provide implementation of JPA specification like Hibernate, iBatis, Toplink etc. 

### JPA Specification 
- provide mapping of entity class with column of database table using `@Entity`, `@Table`, `@Id` etc.

#### 3 layers

##### 1. Spring Data JPA  - create JPA Repository - 2 interface
a. `JpaRepository<Entityclassname,datatype of PK>` interface - used to perform CRUD and batch operation(multiple inserts/interaction records). We have separate concept specific for batch operations that is Spring Batch Processing(CSV file).
- `T getById(int id)` - Deprecated
- `T getOne(int id)` - Deprecated 
- `T getReferenceById(int id)` - fetch single object 
- `List<T> findAll()` - return multiple object
- `T saveAndFlush(T t)` - used to save single object
- `void saveAllAndFlush(Iterable)` - store multiple object inside DB
- `void deleteAllByIdInBatch(Iterable)`
- `void deleteAllInBatch()`

b. `JpaSpecificationExecutor<Entityclassname>` interface - used to retrieve data based on some condition

##### 2. Spring data commons layer - 3 interface
a. `Repository<Entityclassname,datatype of PK>` interface - marker interface, no predefined implementation
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

> We always use JpaRepository interface, because it extends all the other interfaces.


## Implementation

>[!CAUTION]
>The below are implemented in Spring Boot 3.0 version, we we will be importing everything from `jakarta` package and not `javax`. No more servlet concept available after Spring Boot 3.0. When migrating from SB 2.0 to 3.0 one important change we need to make is to change all `javax` to `jakarta`

1. Create spring boot project with `spring data jpa`, `mysql driver`, `lombok` dependency 
	- Use  `mvn dependency::tree` if faced "BUILD FAILURE" with `mvn clean install` 
	- And define the data source properties if you are using Data JPA.
	- Remove the Dialect property from properties file.

2.  Create the required DB in MySQL. (`jpa`)
```mysql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| javabatch          |
| jpa                |
| mysql              |
| performance_schema |
| sakila             |
| sys                |
| world              |
+--------------------+
8 rows in set (0.00 sec)
```

3. Configure DB info in `application.properties`

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/jpa
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.jpa.show-sql = true
spring.jpa.hibernate.ddl-auto = update
#dialect will generate the query based on particular db, not required in the latest version
#spring.jpa.database-platform=org.hibernate.dialect.MySQL5Dialect
```

`application.yml`
```yaml
spring:
  application:
    name: SpringbootJPA
  datasource:
    url: jdbc:mysql://localhost:3306/jpa
    username: root
    password: root
    driver-class-name: com.mysql.jdbc.Driver
  jpa:
    show-sql: true
    #database-platform: org.hibernate.dialect.MySQL5Dialect
    hibernate:
      ddl-auto: update
```

4. `mvn clean install` & Update Maven Project
	- running `mvn clean install` before configuring Data Source props in `properties.yml` will cause build failures.


5. Create entity class
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

6. Create repository interface
```java
public interface EmployeeRepository extends JpaRepository<Employee, Integer>{

}
```
- when the above line of code is written, Spring Data JPA will take care of all the DB implementations and we are not required to write any logic.

5. Main method with `CommandLineRunner` implementing `run` method to preload DB.

#### `save()`
```java
package com.pack.SpringbootJPA;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import com.pack.SpringbootJPA.repository.IEmployeeRepository;

@SpringBootApplication
public class SpringbootJpaApplication implements CommandLineRunner{

	@Autowired
	IEmployeeRepository empRepo;
	
	public static void main(String[] args) {
		SpringApplication.run(SpringbootJpaApplication.class, args);
	}

	//Runs before the main method
	@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub
		insertEmployee();
		
	}

	private void insertEmployee() {
		// TODO Auto-generated method stub
		Employee e1 = new Employee(100,"Ram","male","ram@gmail.com","HR", 25000.0);
		empRepo.save(e1);
	}

}
```

Updated DB:
```mysql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| javabatch          |
| jpa                |
| mysql              |
| performance_schema |
| sakila             |
| sys                |
| world              |
+--------------------+
8 rows in set (0.00 sec)


mysql> use jpa;
Database changed

mysql> show tables;
+---------------+
| Tables_in_jpa |
+---------------+
| empl2024      |
+---------------+
1 row in set (0.00 sec)

mysql> select * from empl2024;
+-----+------------+---------------+--------+------+--------+
| id  | department | email         | gender | name | salary |
+-----+------------+---------------+--------+------+--------+
| 100 | HR         | ram@gmail.com | male   | Ram  |  25000 |
+-----+------------+---------------+--------+------+--------+
1 row in set (0.00 sec)
```

Console Output:
```cmd
Hibernate: create table empl2024 (id integer not null, department varchar(255), email varchar(255), gender varchar(255), name varchar(255), salary float(53), primary key (id)) engine=InnoDB
2024-06-27T08:15:39.731+05:30  INFO 32568 --- [SpringbootJPA] [           main] c.p.S.SpringbootJpaApplication           : Started SpringbootJpaApplication in 3.778 seconds (process running for 4.145)
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: insert into empl2024 (department,email,gender,name,salary,id) values (?,?,?,?,?,?)
```

#### `saveAll()`
```java
@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub
		insertEmployee();
		
	}

	private void insertEmployee() {
		// TODO Auto-generated method stub
		List<Employee> l1=new ArrayList<>();
        Employee e1=new Employee(101,"Sam","male","sam@gmail.com","IT",35000.0);
        l1.add(e1);
        Employee e2=new Employee(102,"Saj","male","saj@gmail.com","Sales",30000.0);
        l1.add(e2);
        Employee e3=new Employee(103,"Tam","male","tam@gmail.com","HR",45000.0);
        l1.add(e3);
        Employee e4=new Employee(104,"Lam","female","lam@gmail.com","Sales",25000.0);
        l1.add(e4);
        Employee e5=new Employee(105,"Lim","female","lim@gmail.com","IT",40000.0);
        l1.add(e5);
        Employee e6=new Employee(106,"John","male","John@gmail.com","HR",15000.0);
        l1.add(e6);
       
        empRepo.saveAll(l1);
	}
```


Console Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: insert into empl2024 (department,email,gender,name,salary,id) values (?,?,?,?,?,?)
Hibernate: insert into empl2024 (department,email,gender,name,salary,id) values (?,?,?,?,?,?)
Hibernate: insert into empl2024 (department,email,gender,name,salary,id) values (?,?,?,?,?,?)
Hibernate: insert into empl2024 (department,email,gender,name,salary,id) values (?,?,?,?,?,?)
Hibernate: insert into empl2024 (department,email,gender,name,salary,id) values (?,?,?,?,?,?)
Hibernate: insert into empl2024 (department,email,gender,name,salary,id) values (?,?,?,?,?,?)
```

Updated DB:
```mysql
mysql> select * from empl2024;
+-----+------------+----------------+--------+------+--------+
| id  | department | email          | gender | name | salary |
+-----+------------+----------------+--------+------+--------+
| 100 | HR         | ram@gmail.com  | male   | Ram  |  25000 |
| 101 | IT         | sam@gmail.com  | male   | Sam  |  35000 |
| 102 | Sales      | saj@gmail.com  | male   | Saj  |  30000 |
| 103 | HR         | tam@gmail.com  | male   | Tam  |  45000 |
| 104 | Sales      | lam@gmail.com  | female | Lam  |  25000 |
| 105 | IT         | lim@gmail.com  | female | Lim  |  40000 |
| 106 | HR         | John@gmail.com | male   | John |  15000 |
+-----+------------+----------------+--------+------+--------+
7 rows in set (0.00 sec)
```


#### `findById(id)`

```java
	@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub
		fetchEmployee(104);
		
	}

	private void fetchEmployee(int i) {
		// TODO Auto-generated method stub
		System.out.println(empRepo.findById(i).get());	
	
```

Console Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Employee(id=104, name=Lam, gender=female, email=lam@gmail.com, department=Sales, salary=25000.0)
```

#### `findAll()`
```java
@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub
		fetchAllEmployees();
		
	}

	private void fetchAllEmployees() {
		// TODO Auto-generated method stub
		List<Employee> l1 = empRepo.findAll();
		l1.forEach(System.out::println);
		
	}
```

Console Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=25000.0)
Employee(id=101, name=Sam, gender=male, email=sam@gmail.com, department=IT, salary=35000.0)
Employee(id=102, name=Saj, gender=male, email=saj@gmail.com, department=Sales, salary=30000.0)
Employee(id=103, name=Tam, gender=male, email=tam@gmail.com, department=HR, salary=45000.0)
Employee(id=104, name=Lam, gender=female, email=lam@gmail.com, department=Sales, salary=25000.0)
Employee(id=105, name=Lim, gender=female, email=lim@gmail.com, department=IT, salary=40000.0)
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=15000.0)
```

#### `Update`
```java
@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub
		updateEmployee(104);
	}

	private void updateEmployee(int i) {
		// TODO Auto-generated method stub
		if(empRepo.existsById(i)) {
			Employee e = empRepo.findById(i).get();
			e.setSalary(40000.00);
			empRepo.save(e);
		}
	}
```

Console Output:
```cmd
Hibernate: select count(*) from empl2024 e1_0 where e1_0.id=?
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: update empl2024 set department=?,email=?,gender=?,name=?,salary=? where id=?
```

Updated DB:  104 salary 25000 -> 40000
```mysql
mysql> select * from empl2024;
+-----+------------+----------------+--------+------+--------+
| id  | department | email          | gender | name | salary |
+-----+------------+----------------+--------+------+--------+
| 100 | HR         | ram@gmail.com  | male   | Ram  |  25000 |
| 101 | IT         | sam@gmail.com  | male   | Sam  |  35000 |
| 102 | Sales      | saj@gmail.com  | male   | Saj  |  30000 |
| 103 | HR         | tam@gmail.com  | male   | Tam  |  45000 |
| 104 | Sales      | lam@gmail.com  | female | Lam  |  25000 |
| 105 | IT         | lim@gmail.com  | female | Lim  |  40000 |
| 106 | HR         | John@gmail.com | male   | John |  15000 |
+-----+------------+----------------+--------+------+--------+
7 rows in set (0.00 sec)

mysql> select * from empl2024;
+-----+------------+----------------+--------+------+--------+
| id  | department | email          | gender | name | salary |
+-----+------------+----------------+--------+------+--------+
| 100 | HR         | ram@gmail.com  | male   | Ram  |  25000 |
| 101 | IT         | sam@gmail.com  | male   | Sam  |  35000 |
| 102 | Sales      | saj@gmail.com  | male   | Saj  |  30000 |
| 103 | HR         | tam@gmail.com  | male   | Tam  |  45000 |
| 104 | Sales      | lam@gmail.com  | female | Lam  |  40000 |
| 105 | IT         | lim@gmail.com  | female | Lim  |  40000 |
| 106 | HR         | John@gmail.com | male   | John |  15000 |
+-----+------------+----------------+--------+------+--------+
7 rows in set (0.00 sec)
```



#### `delete()`

```java
@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub
		deleteEmployee(104);
	}

	private void deleteEmployee(int i) {
		// TODO Auto-generated method stub
		if(empRepo.existsById(i)) {
			Employee e = empRepo.findById(i).get();
			empRepo.delete(e);
		}
```

Console Output :
```cmd
Hibernate: select count(*) from empl2024 e1_0 where e1_0.id=?
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.id=?
Hibernate: delete from empl2024 where id=?
```

Updated DB: deleted 104
```mysql
mysql> select * from empl2024;
+-----+------------+----------------+--------+------+--------+
| id  | department | email          | gender | name | salary |
+-----+------------+----------------+--------+------+--------+
| 100 | HR         | ram@gmail.com  | male   | Ram  |  25000 |
| 101 | IT         | sam@gmail.com  | male   | Sam  |  35000 |
| 102 | Sales      | saj@gmail.com  | male   | Saj  |  30000 |
| 103 | HR         | tam@gmail.com  | male   | Tam  |  45000 |
| 105 | IT         | lim@gmail.com  | female | Lim  |  40000 |
| 106 | HR         | John@gmail.com | male   | John |  15000 |
+-----+------------+----------------+--------+------+--------+
6 rows in set (0.00 sec)
```


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
                             //insertEmployee(); to insert data into DATABASE
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
                                           //empRepo.deleteById(i); can use both
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
                             empRepo.save(e1);*/ //To save a single record, takes object as argument
                             
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
                             empRepo.saveAll(l1); // takes list as argument
              }

}
```


## Different ways to communicate with database

### 1. Using predefined methods
 - `T save(T t)` - store single object 
 - `void saveAll(Iterable) `- store multiple object
 - `Optional findById(int id)` - return single object based on id
 - `Iterable findAll(`) - return multiple object
 - `boolean existsById(int id)`
 - `void deleteById(int id)` - delete single object based on id
 - `void delete(T t)` - delete single object
 - `void deleteAll()`

### 2. Using Custom JPA Method 
 - derived methods used for fetching the data based on other properties except `id`.
 - name of the method should starts with either `findBy/getBy/queryBy/readBy`
 - only declare the custom JPA method inside repository interface, so spring data jpa will automatically write logic on behalf of user


>[!CAUTION]
>Custom JPA methods are not predefined, we need to try with Trial and Error and see which declaration is understood by the JPA and which gives us the expected outcome.


```java
List<Employee> findByDept(String dname); //here dept must be a property of Entity
List<Employee> readByDeptAndSalaryLessThan(String dname,Double sal); //Here salary is a Entity property

like - Pattern matching (%,_)

List<Employee> queryByNameLike(String name);
List<Employee> getByNameLikeAndSalaryGreaterThan(String name, Double sal);
List<Employee> findByDeptIsNull();
List<Employee> getByNameStartsWith(String name);
List<Employee> findByNameContainingOrDeptContainingAllIgnoreCase(String name,String dname)
```

3. Limiting the records based on custom JPA methods 
	- using `First` or `Top` keyword

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

## Custom JPA Methods

1. Add the declaration in `IEmployeeRepository` interface
```java
package com.pack.SpringbootJPA.repository;

import java.util.List;

import org.springframework.data.jpa.repository.JpaRepository;

import com.pack.SpringbootJPA.Employee;

public interface IEmployeeRepository extends JpaRepository<Employee, Integer> {
	// Here Department is a property of the Employee Entity
	// Return type should be list as it would return a list of employees
	List<Employee> findByDepartment(String dname); 
}
```

2. Add the implementation of `CustomJPAMethod` in Main class.
```java
	@Override
	public void run(String... args) throws Exception {
		// TODO Auto-generated method stub
		customJPAMethod();	
	}

	//caan be any method name
	private void customJPAMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.findByDepartment("HR");
		l.forEach(System.out::println);
		
	}
```

3. Console Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department=?
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=25000.0)
Employee(id=103, name=Tam, gender=male, email=tam@gmail.com, department=HR, salary=45000.0)
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=15000.0)
```



##### Example 1: `readByDepartmentAndSalaryLessThan(String dname, Double sal)`
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.readByDepartmentAndSalaryLessThan("HR", 26000.00);
		l.forEach(System.out::println);	
	}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department=? and e1_0.salary<?
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=25000.0)
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=15000.0)
```


##### Example 2: `findByDepartmentAndSalaryLessThan(String dname, Double sal)`
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.findByDepartmentAndSalaryLessThan("HR", 25000.00);
		l.forEach(System.out::println);	
	}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department=? and e1_0.salary<?
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=15000.0)
```

##### Example 3: `queryByNameLike(String name)`
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.queryByNameLike("S%");
		l.forEach(System.out::println);
}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.name like ? escape '\\'
Employee(id=101, name=Sam, gender=male, email=sam@gmail.com, department=IT, salary=35000.0)
Employee(id=102, name=Saj, gender=male, email=saj@gmail.com, department=Sales, salary=30000.0)
```

##### Example 4: `getByNameLikeAndSalaryGreaterThan(String name, Double sal)`
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.getByNameLikeAndSalaryGreaterThan("S%", 30000.00);
		l.forEach(System.out::println);	
	}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.name like ? escape '\\' and e1_0.salary>?
Employee(id=101, name=Sam, gender=male, email=sam@gmail.com, department=IT, salary=35000.0)
```

##### Example 5: `findByDepartmentIsNull()`
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.findByDepartmentIsNull();
		l.forEach(System.out::println);	
	}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department is null
```

##### Example 6: `getByNameStartsWith(String name)`
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.getByNameStartsWith("s");
		l.forEach(System.out::println);	
	}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.name like ? escape '\\'
Employee(id=101, name=Sam, gender=male, email=sam@gmail.com, department=IT, salary=35000.0)
Employee(id=102, name=Saj, gender=male, email=saj@gmail.com, department=Sales, salary=30000.0)
```

##### Example 7:
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.findByDepartmentAndSalaryLessThan("HR", 26000.00);
		l.forEach(System.out::println);	
	}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department=? and e1_0.salary<?
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=25000.0)
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=15000.0)
```

#### Example 1:
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.findByDepartmentAndSalaryLessThan("HR", 26000.00);
		l.forEach(System.out::println);	
	}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department=? and e1_0.salary<?
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=25000.0)
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=15000.0)
```

#### Example 1:
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.findByDepartmentAndSalaryLessThan("HR", 26000.00);
		l.forEach(System.out::println);	
	}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department=? and e1_0.salary<?
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=25000.0)
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=15000.0)
```

#### Example 1:
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.findByDepartmentAndSalaryLessThan("HR", 26000.00);
		l.forEach(System.out::println);	
	}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department=? and e1_0.salary<?
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=25000.0)
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=15000.0)
```

#### Example 1:
```java
private void customMethod() {
		// TODO Auto-generated method stub
		List<Employee> l = empRepo.findByDepartmentAndSalaryLessThan("HR", 26000.00);
		l.forEach(System.out::println);	
	}
```

Output:
```cmd
Hibernate: select e1_0.id,e1_0.department,e1_0.email,e1_0.gender,e1_0.name,e1_0.salary from empl2024 e1_0 where e1_0.department=? and e1_0.salary<?
Employee(id=100, name=Ram, gender=male, email=ram@gmail.com, department=HR, salary=25000.0)
Employee(id=106, name=John, gender=male, email=John@gmail.com, department=HR, salary=15000.0)
```