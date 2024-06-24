
*Date : 06.10.2024*

---

# Spring MVC

Spring MVC - Where we return the response in `view` page using (JSP/Thymeleaf)

client request -> controller(handle req and res) -> service(business logic) -> repository -> view page

## 1. Create spring boot project with spring web dependency and `war` packaging 

`war` package will give a `webapp` folder where we will have the JSP pages.
To make spring boot to understand JSP pages, we have to provide 1 dependency

```xml
<dependency>
	   <groupId>org.apache.tomcat.embed</groupId>
	   <artifactId>tomcat-embed-jasper</artifactId>
	   <scope>provided</scope>
</dependency>
```


## 2. Create Controller program

`@Controller` program returns JSP views 
```java
@Controller   // @RestController returns JSON/ String
public class MainController {

              @GetMapping("/info")
              public String getInfo() {
                             return "index";  //view name of jsp page
              }
              
              @GetMapping("/info1")
              public String getInfo1(ModelMap m1,Model m2, Map m3) {
                             m1.addAttribute("name", "Ram");
                             m2.addAttribute("age", 24);
                             m3.put("address", "Chennai");
                             return "student";
              }
}
```


## 3. Create JSP page 
### as per return value inside webapp - WEB-INF - views(any name) - create jsp page

index.jsp (inside `src/main/webapp/WEB-INF/views/index.jsp`)
```html
<%@ page language="java" contentType="text/html; charset=ISO-8859-1" pageEncoding="ISO-8859-1" %>

	<!DOCTYPE html>
	<html>

	<head>
		<meta charset="ISO-8859-1">
		<title>Insert title here</title>
	</head>

	<body>
		<h2>Welcome to Spring Boot MVC application</h2>
	</body>

	</html>
```

## 4. Configure jsp info in `application.properties`

```properties
spring.application.name=SpringBootMVC
server.port=1500
server.servlet.context-path=/mvc
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
#prefix+viewname+suffix=/WEB-INF/views/index.jsp
```

`application.yml`
```yaml
spring:
 application:
  name: SpringBootMVC
 mvc:
  view: 
   prefix: /WEB-INF/views/
   suffix: .jsp

server:
 port: 1500
 servlet:
  context-path: /mvc
```

JSP is used to develop dynamic web pages while HTML is for static webpages.

To pass value from controller program to JSP program we can use either` ModelMap` class or `Model` class or `Map` interface

Dynamic Content  - ${parameter_name} -> Expression Language
```html
<%@ page language="java" contentType="text/html; charset=ISO-8859-1" pageEncoding="ISO-8859-1" %>

	<!DOCTYPE html>
	<html>

	<head>
		<meta charset="ISO-8859-1">
		<title>Insert title here</title>
	</head>

	<body>
		<h2>Welcome ${name} lives in ${address} having age ${age}</h2>
	</body>

	</html>
```


> JSP pages are currently less used and mostly SpringBoot is used to write the backend logic(REST API) while Angular/React being used in handle the front end counterparts. This way we can achieve a  loose coupling of Back-End and Front-End.

---
# Spring Boot Jetty
1. Exclude tomcat server from web dependency

```xml
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-web</artifactId>
   <exclusions>
	  <exclusion>
		  <groupId>org.springframework.boot</groupId>
		  <artifactId>spring-boot-starter-tomcat</artifactId>
	  </exclusion>
   </exclusions>
</dependency>
```

2. Comment spring boot starter tomcat, tomcat-embed-jasper dependency

3. Add spring boot Jetty and JSP Jetty dependency

```xml
<dependency>
	   <groupId>org.springframework.boot</groupId>
	   <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
<dependency>
    <groupId>org.eclipse.jetty</groupId>
    <artifactId>apache-jsp</artifactId>
    <version>11.0.21</version> <!--Error if wrong version-->
</dependency>
```



# Spring Boot Profiling
  - In enterprise application we have many environments like dev, test, prod and etc. And each env needs specific configuration related to that env and configured in `application.properties`, we can't configure everything in a single file, so to use different properties files in different env we use ==profiling.==

1. We need to create different properties file related to each env by `application-profilename.properties` 
		e.g.:` application-dev.properties`, `application-prod.properties`

2. `spring.profiles.active=profilename` in `application.properties` where it will invoke the related profile

`@Value`- used to read single property from properties files and write into controller program or any program

`@Profile`- used to programmatically control files/programs based on profiles 

`application.properties`
```properties
spring.application.name=SpringBoot1
server.port=2000
message=Welcome default user 
spring.profiles.active=prod
```

`application-dev.properties`
```properties
message=Welcome development user
server.port=3000
```

`application-prod.properties`
```properties
message=Welcome Production user
server.port=4000
```

```java
@RestController
public class ProfileController {
              
              @Value("${message}") //SpEl - Spring Expression Language 
              private String msg;

              @GetMapping("/profile")
              public String hello() {
                             return "Hello world from Controller "+ msg;
              }
}
```


```java
@Configuration
@Profile("dev") //will run only in dev profile
public class AppConfig {
    @PostConstruct // at the time of initializing itself we want to run this method, not tied to any object 
              public void print() {
                             System.out.println("This method is invoked only in Development environment");
              }
}
```

Console Output:
```cmd
2024-06-13T21:23:09.425+05:30  INFO 844 --- [SpringBootMVC] [           main] o.e.j.e.servlet.ServletContextHandler    : Started osbwej.JettyEmbeddedWebAppContext@348ad293{application,/mvc,b=file:/C:/Users/acer/eclipse-workspace/SpringBootMVC/src/main/webapp/,a=AVAILABLE,h=oeje10s.SessionHandler@30f74e79{STARTED}}
2024-06-13T21:23:09.428+05:30  INFO 844 --- [SpringBootMVC] [           main] org.eclipse.jetty.server.Server          : Started oejs.Server@107f4980{STARTING}[12.0.9,sto=0] @1877ms
==>This method is invoked only in Development environment==
2024-06-13T21:23:09.504+05:30  INFO 844 --- [SpringBootMVC] [           main] o.s.b.a.w.s.WelcomePageHandlerMapping    : Adding welcome page template: index

```
By default Spring boot will read all configuration either from `application.properties` or `application.yml`



## Profiling in JSP

`application.properties`
```properties
spring.application.name=SpringBootMVC
server.servlet.context-path=/mvc
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp

server.port=3000
message=Welcome default user


spring.profiles.active=dev
#Should define the active profile here 
```

`application-dev.properties`
```properties
spring.application.name=SpringBootMVC
server.servlet.context-path=/mvc
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp

server.port=2000
message=Welcome development user
```

`application-prod.properties`
```properties
spring.application.name=SpringBootMVC
server.servlet.context-path=/mvc
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp

server.port=4000
message=Welcome production user
```

Instead we can go with a single `application.yml` file, the default configuration will have the general configs while the environment specific configs will be separated by `---` separator.
```yaml
spring:
  application:
    name: SpringBootMVC
  mvc:
    view:
      prefix: /WEB-INF/views/
      suffix: .jsp
  profiles:
    active: prod

server:
  port: 3000
  servlet:
    context-path: /mvc

logging:
  level:
    web: DEBUG

message: Welcome default user

---
spring:
  config:
    activate:
      on-profile: dev

server:
  port: 2000

message: Welcome Development user

---
spring:
  config:
    activate:
      on-profile: prod

server:
  port: 4000

message: Welcome production user
```


`ProfileController.class`
```java
package com.pack.SpringBootMVC.controller;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class ProfileController {

	@Value("${message}")
	private String msg;
	
	@GetMapping("/user")
	public String getUser(Model m) {
		m.addAttribute("message", msg);
		return "user";
	}
}
```

`user.jsp` in views
```html
<%@ page language="java" contentType="text/html; charset=ISO-8859-1" pageEncoding="ISO-8859-1" %>

	<!DOCTYPE html>
	<html>

	<head>
		<meta charset="ISO-8859-1">
		<title>Insert title here</title>
	</head>

	<body>
		<h2>${message}</h2>
	</body>

	</html>
```


### `application.properties`
1. It is represent as a sequence of key value pair
```properties
spring.application.name=SpringBoot1
server.port=1000
server.servlet.context-path=/app
```

2. This file is supported only in Java lang

3. support only key value pair and both in form of string

4. If we want handle different profiles then we have to create different properties files 

### `application.yml`
1. It is represent in hiearchial format

```yml
server:
   port: 1000
   servlet:
      context-path: /app

spring:
   application:
      name: SpringBoot1
```

2. This file is supported in Java, Python etc.

3. support scalar datatype, map, list, key value pairs

4. All configuration related to multiple profiles can be handled in ==single== yaml file

```yml
server:
   port: 1000
   servlet:
      context-path: /app

spring:
   profiles:
      active: dev

---
spring:
   profiles: dev
server:
   port: 3000

---
spring:
   profiles: prod
server:
   port: 1000
```


`@PropertySource` - used to read ==single== property file with different name or in present different location 
`@PropertySources` - used to read ==multiple== property file with different name or present in different location 

The above need to be implemented using `@Value` which may become hideous when the number of properties increases. Hence we could use 
`@ConfigurationProperties` - used to map entire properties in properties file to a separate j==ava bean object==



# Lombok
Lombok dependency - to reduce boilerplate code (ie) getter, setter, default constructor, parameterized constructor, toString(), equals(), hashCode(), logging

> lombok needs to be configured in eclipse

`student.properties` in src/main/ folder
```properties
student.id=1000
student.name=Ram
student.address=Chennai
student.age=30
```

`student1.properties` in local directory
```properties
student.email=ram@gmail.com
student.course=CSE
student.mark=89
```

```java
@Configuration
//@PropertySource("classpath:student.properties")
//@PropertySource("file:\\C:\\Training\\student1.properties")
@PropertySources({
              @PropertySource("classpath:student.properties"),
              @PropertySource(file:\\C:\\Training\\student1.properties)
})
@ConfigurationProperties(prefix="student")
//@Getter
//@Setter
@Data //@getter+@setter
@NoArgsConstructor
@AllArgsConstructor
@ToString
public class StudentConfig {
    private String name;
    private String address;
    private String email;
    private Integer age;
    private String course;
}
```

```java
@RestController
public class StudentController {
              
              @Value("${student.id}")
              private Integer id;
              
              @Value("${student.mark}")
              private Integer mark;
              
              @Autowired
              StudentConfig config;

              @GetMapping("/studentInfo")
              public String getStudentInfo() {
                             return id+" "+config.getName()+" "+config.getAddress()+" "+mark;
              }
}
```


### `@Value`
1. Injecting properties one by one
2. Support SpEL(${}) - Spring Expression Language
3. Loose binding/Loose Grammar is not supported (ie) attribute name should be matching
4. Validation of properties is not supported
5. support only scalar datatype

### `@ConfigurationProperties`
1. Bulk injection of properties
2. Doesn't support SpEL
3. Supports Loose Binding/Loose Grammar (ie) no need to match the attribute name(ie) special char or cases (eg) NAME, firstname(first-name)
4. Validation of properties is supported
5. support all datatypes as well as objects

`mail.properties`
```properties
#Scalar Data Types
mail.to=abc@gmail.com
mail.from=xyz@gmail.com
mail.age=25
mail.firstname=Ram
mail.lastname=Kumar

#Complex Data Types
mail.cc=uvw@gmail.com,pqr@gmail.com
mail.bcc=efg@gmail.com,klm@gmail.com

#Nested Data Types
mail.credential.username=Ram
mail.credential.password=abcd12345
```

## Accessing Complex/Nested Data Types
pom.xml
```xml
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
	<optional>true</optional>
</dependency>
```

MailConfig.java
```java
package com.pack.SpringValidation;

import java.util.List;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;

import lombok.Data;

@Configuration
@PropertySource("classpath:mail.properties")
@ConfigurationProperties(prefix="mail")
@Data
public class MailConfig {

	private String to;
	private String from;
	private Integer age;
	private String FIRSTNAME; // ConfigProp - Loosely bound
	private String Last_Name; // Loose Bound

	private String[] cc; // Complex props
	private List<String> bcc; // Complex properties

	private Credential credential = new Credential();
	
	@Data // To access get+set of nested properties
	public class Credential {
		private String username; // nested prop
		private String password; // nested prop
	}
}
```

MailController.java
```java
package com.pack.SpringValidation.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import com.pack.SpringValidation.MailConfig;

@RestController
public class MailController {

	@Autowired
	MailConfig config;
	
	@GetMapping(value="/mail")
	public String getMail() {
		return config.getFIRSTNAME()+" "+config.getBcc()+" "+config.getCredential().getPassword();
	}
}

```

Output when running the program from `main()` method
![[Pasted image 20240623162241.png]]


# Validation
To do validation

```xml
<dependency>
	   <groupId>org.hibernate.validator</groupId>
	   <artifactId>hibernate-validator</artifactId>
	   <version>6.0.5.Final</version>
</dependency>
 <dependency>
	   <groupId>jakarta.validation</groupId>
	   <artifactId>jakarta.validation-api</artifactId>
	   <version>2.0.1</version>
 </dependency>
 
 <!-- DO NOT USE THE BELOW-->
 <dependency>
	   <groupId>javax.validation</groupId>
	   <artifactId>validation-api</artifactId>
	   <version>2.0.0.Final</version>
 </dependency>
```

>[!CAUTION]
>`javax.validation` is deprecated, you must use `jakarta.validation`


`@Validated` - to do validating the properties in properties files
`@Valid` - to do validation for nested class properties

```java
package com.pack.SpringValidation;

import java.util.List;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;
import org.springframework.validation.annotation.Validated;

import jakarta.validation.Valid;
import jakarta.validation.constraints.Max;
import jakarta.validation.constraints.Min;
import jakarta.validation.constraints.NotNull;
import jakarta.validation.constraints.Size;
import lombok.Data;

@Configuration
@PropertySource("classpath:mail.properties")
@ConfigurationProperties(prefix="mail")
@Data
@Validated 
public class MailConfig {
   @NotNull
   private String to;
   @NotNull
   private String from;
   @Min(value=20)
   @Max(value=40)
   private Integer age;
   @NotNull
   private String FIRSTNAME; //Loose binding, no need to match exact name
   private String LAST_NAME; //Loose binding, no need to match exact name
   
   private String[] cc;
   private List<String> bcc;
   
   @Valid
   private Credential credential=new Credential();
   
   public class Credential {
                 @NotNull
                 private String username;
                 @Size(max=8,min=4)
                 private String password;
   }
}
```

## Output
Console Output:
```cmd
***************************
APPLICATION FAILED TO START
***************************

Description:

Binding to target com.pack.SpringValidation.MailConfig$$SpringCGLIB$$0 failed:

    Property: mail.credential.password
    Value: "abcd12345"
    Origin: "mail.credential.password" from property source "class path resource [mail.properties]"
    Reason: size must be between 4 and 8


Action:

Update your application's configuration
```
> Application runs properly after updating the password length


Browser Output:
![[Pasted image 20240623203757.png]]





