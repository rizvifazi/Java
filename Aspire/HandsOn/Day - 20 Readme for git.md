


---
# EmployeeInfoSpring

Spring based REST API application to manage Employee details.



---
# Usage

### 1. Clone the repo
### 2. Open via IDE (Eclipse) and Import as Existing Maven Project
### 3. Show in Local terminal and run `mvn clean install`
### 4. Update the project to import all dependencies

---
# System requirements

### 1. JDK 17 or above 

---

# Implementation

## 1. Download Spring Initializr
- Download `Spring Initializr` with `Spring Web` and `Spring Dev Tools` Dependencies from https://start.spring.io

## 2. Follow the basic 6 steps
- `mvn clean install` and Update the project

## 3.pom.xml
- No any configurations to be done in pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.2.6</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.pack</groupId>
	<artifactId>Employeeinfosb</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>Employeeinfosb</name>
	<description>Display employee info in JSON format</description>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>

```



## 4. Configure Application Properties
 - Setting logging level, port and context-path for best practice.
 - `application.properties`file will be inside /src/main/resources directory
 
```properties
spring.application.name=EmployeeinfoSpring
logging.level.web=DEBUG
server.port=2020
server.servlet.context-path=/app
```


## 5. Create EmployeeInfo.class

```java
package com.pack.EmployeeinfoSpring.service;

//No annotations required here @Entity can be used if we are using JPA
public class EmployeeInfo {

	private Integer id;
	private String name;
	private Double salary;
	private String address;

	public Integer getId() {
		return id;
	}

	public void setId(Integer id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Double getSalary() {
		return salary;
	}

	public void setSalary(Double salary) {
		this.salary = salary;
	}

	public String getAddress() {
		return address;
	}

	public void setAddress(String address) {
		this.address = address;
	}

	public EmployeeInfo() {
	}

	public EmployeeInfo(String name) {
		this.name = name;
	}

	public EmployeeInfo(Integer id, String name, Double salary, String address) {
		super();
		this.id = id;
		this.name = name;
		this.salary = salary;
		this.address = address;
	}

	@Override
	public String toString() {
		return "EmployeeInfo [id=" + id + ", name=" + name + ", salary=" + salary + ", address=" + address + "]";
	}

}
```

## 6. Create EmployeeDaoService.class
- This `@Component` class will be used to preload dummy employees in the employee list, return list of employees as well as to return an individual employee details based on the `@Pathvariable` in the GetRequest URL.

```java
package com.pack.EmployeeinfoSpring.service;

import java.util.ArrayList;
import java.util.List;
import org.springframework.stereotype.Component;

@Component
public class EmployeeDaoService {

	private static List<EmployeeInfo> employees = new ArrayList<>();

	// Static block to pre-load dummy employees
	static {
		employees.add(new EmployeeInfo(1, "Alice Johnson", 52000.00, "San Francisco, CA"));
		employees.add(new EmployeeInfo(2, "Bob Williams", 48000.00, "Seattle, WA"));
		employees.add(new EmployeeInfo(3, "Charlie Miller", 61000.00, "New York, NY"));
		employees.add(new EmployeeInfo(4, "Diana Garcia", 39000.00, "Austin, TX"));
		employees.add(new EmployeeInfo(5, "Ethan Lee", 45000.00, "Chicago, IL"));
	}

	// returns list of employees
	public List<EmployeeInfo> findAll() {
		return employees;
	}

	//to return employee details based on @Pathvariable String
	public EmployeeInfo findOne(int id) {

		for (EmployeeInfo e : employees) {
			if (e.getId() == id)
				return e;
		}
		return null;
	}

}
```

## 7. Create EmployeeController.class
- This is the `@RestController` class which imlements the ErrorController FI and defines the Request mappings.

```java
package com.pack.EmployeeinfoSpring.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.web.servlet.error.ErrorController;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

import com.pack.EmployeeinfoSpring.service.EmployeeDaoService;
import com.pack.EmployeeinfoSpring.service.EmployeeInfo;

@RestController
public class EmployeeController implements ErrorController {

	// Defining for Error page
	protected static final String PATH = "/error";

	// Return a HTML based string to print useful information if entered a incorrect
	// URL
	@GetMapping(value = PATH)
	public String getErrorMessage() {
		return """
						<h2 style="font-weight: bold; color: red; margin: 2rem 0;">Error 404! Please check the URL</h2>
							<p>The requested resource was not found.</p>
						<h3 style="font-family: monospace; font-size: smaller; margin-top: 1rem;">Correct Usage:</h3>
						  <ul>
						    <li style="font-family: monospace;">localhost:2020/app/employees</li>
						    <li style="font-family: monospace;">localhost:2020/app/employee/{id}</li>
						  </ul>
				""";
	}

	// This needs to be implemented for ErrorController functional interface
	public String getErrorPath() {
		return PATH;
	}

	// Referring another (DAO) component here
	@Autowired
	private EmployeeDaoService service;

	// Get Request Mapping to list all employees
	@GetMapping(value = "/employees")
	public List<EmployeeInfo> getAllEmployees() {
		return service.findAll();
	}

	// Get Request Mapping and retrieve individual employee data
	@GetMapping(value = "/employee/{id}")
	public EmployeeInfo getEmployeeInfo(@PathVariable Integer id) {
		return service.findOne(id);
	}

}
```


## 8. EmployeeInfoSpringApplication.class
- Run the program as Java Application from EmployeeInfoSpringApplication.class

```java
package com.pack.EmployeeinfoSpring;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class EmployeeinfoSpringApplication {

	public static void main(String[] args) {
		SpringApplication.run(EmployeeinfoSpringApplication.class, args);
	}

}
```

## 9. Console Output

```cmd

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v3.2.6)

2024-06-09T23:24:58.504+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] c.p.E.EmployeeinfoSpringApplication      : Starting EmployeeinfoSpringApplication using Java 17.0.7 with PID 6228 (C:\Users\acer\eclipse-workspace\EmployeeinfoSpring\target\classes started by acer in C:\Users\acer\eclipse-workspace\EmployeeinfoSpring)
2024-06-09T23:24:58.506+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] c.p.E.EmployeeinfoSpringApplication      : No active profile set, falling back to 1 default profile: "default"
2024-06-09T23:24:58.550+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : Devtools property defaults active! Set 'spring.devtools.add-properties' to 'false' to disable
2024-06-09T23:24:59.376+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port 2020 (http)
2024-06-09T23:24:59.389+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2024-06-09T23:24:59.390+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] o.apache.catalina.core.StandardEngine    : Starting Servlet engine: [Apache Tomcat/10.1.24]
2024-06-09T23:24:59.434+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] o.a.c.c.C.[Tomcat].[localhost].[/app]    : Initializing Spring embedded WebApplicationContext
2024-06-09T23:24:59.436+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 885 ms
2024-06-09T23:24:59.450+05:30 DEBUG 6228 --- [EmployeeinfoSpring] [  restartedMain] o.s.b.w.s.ServletContextInitializerBeans : Mapping filters: characterEncodingFilter urls=[/*] order=-2147483648, formContentFilter urls=[/*] order=-9900, requestContextFilter urls=[/*] order=-105
2024-06-09T23:24:59.451+05:30 DEBUG 6228 --- [EmployeeinfoSpring] [  restartedMain] o.s.b.w.s.ServletContextInitializerBeans : Mapping servlets: dispatcherServlet urls=[/]
2024-06-09T23:24:59.592+05:30 DEBUG 6228 --- [EmployeeinfoSpring] [  restartedMain] s.w.s.m.m.a.RequestMappingHandlerMapping : 3 mappings in 'requestMappingHandlerMapping'
2024-06-09T23:24:59.638+05:30 DEBUG 6228 --- [EmployeeinfoSpring] [  restartedMain] o.s.w.s.handler.SimpleUrlHandlerMapping  : Patterns [/webjars/**, /**] in 'resourceHandlerMapping'
2024-06-09T23:24:59.658+05:30 DEBUG 6228 --- [EmployeeinfoSpring] [  restartedMain] s.w.s.m.m.a.RequestMappingHandlerAdapter : ControllerAdvice beans: 0 @ModelAttribute, 0 @InitBinder, 1 RequestBodyAdvice, 1 ResponseBodyAdvice
2024-06-09T23:24:59.685+05:30 DEBUG 6228 --- [EmployeeinfoSpring] [  restartedMain] .m.m.a.ExceptionHandlerExceptionResolver : ControllerAdvice beans: 0 @ExceptionHandler, 1 ResponseBodyAdvice
2024-06-09T23:24:59.730+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] o.s.b.d.a.OptionalLiveReloadServer       : LiveReload server is running on port 35729
2024-06-09T23:24:59.763+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port 2020 (http) with context path '/app'
2024-06-09T23:24:59.772+05:30  INFO 6228 --- [EmployeeinfoSpring] [  restartedMain] c.p.E.EmployeeinfoSpringApplication      : Started EmployeeinfoSpringApplication in 1.558 seconds (process running for 1.848)
```

Navigate to http://localhost:2020/app/employees through a browser to See the browser output in JSON format.

## 10. Browser Outputs

### http://localhost:2020/app/employees 

```JSON
[
  {
    "id": 1,
    "name": "Alice Johnson",
    "salary": 52000,
    "address": "San Francisco, CA"
  },
  {
    "id": 2,
    "name": "Bob Williams",
    "salary": 48000,
    "address": "Seattle, WA"
  },
  {
    "id": 3,
    "name": "Charlie Miller",
    "salary": 61000,
    "address": "New York, NY"
  },
  {
    "id": 4,
    "name": "Diana Garcia",
    "salary": 39000,
    "address": "Austin, TX"
  },
  {
    "id": 5,
    "name": "Ethan Lee",
    "salary": 45000,
    "address": "Chicago, IL"
  }
]
```


### http://localhost:2020/app/employee/3
```JSON
{
  "id": 3,
  "name": "Charlie Miller",
  "salary": 61000,
  "address": "New York, NY"
}
```

### Error Page
```HTML
<h2 style="font-weight: bold; color: red; margin: 2rem 0;">Error 404! Please check the URL</h2>
	<p>The requested resource was not found.</p>
<h3 style="font-family: monospace; font-size: smaller; margin-top: 1rem;">Correct Usage:</h3>
  <ul>
	<li style="font-family: monospace;">localhost:2020/app/employees</li>
	<li style="font-family: monospace;">localhost:2020/app/employee/{id}</li>
  </ul>
```




