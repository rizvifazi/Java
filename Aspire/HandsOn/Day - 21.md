
*Date : 06.10.2024*

# Hands-on

1. Create Spring boot application to implement profiles likes prod,dev and print value of message from properties file. 
Note: create all profiles in single file

2. Create Spring boot application to read and print all user information from user.properties file present in local machine(ie)C:/handson folder

3. Create Spring Boot MVC appl, to display employee details like name, age, salary in employee.jsp 

---

# 1. Implement Profiles using application.yml

## 1. Download Spring Initializr
- Download `Spring Initializr` with `Spring Web` Dependencies from https://start.spring.io

## 2. Follow the basic 6 steps
- `mvn clean install` and Update the project

## 3.pom.xml
- Additional configuration has been done to run the application in Jetty Server instead of Tomcat
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.2.6</version>
		<relativePath /> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.example</groupId>
	<artifactId>SpringProfiles</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>
	<name>SpringProfiles</name>
	<description>Implement Profiles using application yaml</description>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencies>
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
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-jetty</artifactId>
		</dependency>
		<dependency>
			<groupId>org.eclipse.jetty</groupId>
			<artifactId>apache-jsp</artifactId>
			<version>11.0.21</version>
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



## 4. Configure Application YAML
 - Only `application.yml` file can have different profiles configurations in a single file
 - Setting logging level, port and context-path for best practice.
 - `application.yml` file will be inside `/src/main/resources` directory
 - Here it has a custom property `message` which will display different values based on different environment
 
```yaml
# The default configuration will have the general configurations
# The environment specific configurations will be separated by `---` separator
# We can as many custom configurations as we want in a single application.yml

# Default Configuration

spring:
  application:
    name: SpringBootMVC
  mvc:
    view:
      prefix: /WEB-INF/views/
      suffix: .jsp
  profiles:
    active: dev

server:
  port: 3000
  servlet:
    context-path: /mvc

logging:
  level:
    web: DEBUG

message: Welcome default user

---
# Development Environment Configuration

spring:
  config:
    activate:
      on-profile: dev

server:
  port: 2000

message: Welcome Development user

---
# Production Environment Configuration

spring:
  config:
    activate:
      on-profile: prod

server:
  port: 4000

message: Welcome production user

```


## 5. Create ProfileController.class
 - This will obtain the `message` property from the `application.yml` using `@Value` annotation. 
 - Then the `msg` property is passed to `index.jsp` using `Map` interface.

```java
package com.example.SpringProfiles.controller;

import java.util.Map;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class ProfileController {
	
	// obtaining value from properties file
	@Value("${message}")
	private String msg;
	
	
	//passing the value to index.jsp
	@GetMapping("/profile")
	public String getProfile(Map<String,String> m) {
		m.put("message", msg);
		return "index";
	}
}
```

## 6. Create index.jsp
 - `index.jsp` need to be created inside `~ProjectDirectory~\\src\\main\\webapp\\WEB-INF\\views\\index.jsp`
 - Here `${message}` placeholder will display the custom message on each environment.
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1" pageEncoding="ISO-8859-1" %>

	<!DOCTYPE html>
	<html>

	<head>
		<meta charset="ISO-8859-1">
		<title>Insert title here</title>
	</head>

	<body>
		<h1>Welcome to Spring Boot MVC application</h1>
		<!--The below message using Spring Expression Language-->
		<!--The below message is passed here from ProfileController-->
		<h2>${message}</h2>
	</body>

	</html>

```


## 7. Run the proogram from SpringProfilesApplication class
```java
package com.example.SpringProfiles;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringProfilesApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringProfilesApplication.class, args);
	}

}
```


## 8. Outputs

- When configured active profile as `dev` in `application.yml`
```yaml
spring:
  application:
    name: SpringBootMVC
  mvc:
    view:
      prefix: /WEB-INF/views/
      suffix: .jsp
  profiles:
    active: dev
```

- Browser Output :
![[Pasted image 20240615013647.png]]


- When configured active profile as `prod` in `application.yml`
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
```

- Browser Output :
![[Pasted image 20240615013941.png]]



---
# 2. Read user.properties from local machine

Create Spring boot application to read and print all user information from `user.properties` file present in local machine i.e.: `C:/handson folder`

## 1. Download Spring Initializr
- Download `Spring Initializr` with `Spring Web`, `Dev Tools`, `Lombok` Dependencies from https://start.spring.io

## 2. Follow the basic 6 steps
- `mvn clean install` and Update the project

## 3.pom.xml
- Additional manual configuration needs to be done for `tomcat-embed-jasper`

```xml
		<!--Jasper dependeency need to be configured manually in order for Spring to process JSP pages-->
		<dependency>
			<groupId>org.apache.tomcat.embed</groupId>
			<artifactId>tomcat-embed-jasper</artifactId>
			<scope>provided</scope>
		</dependency>
```

pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.2.6</version>
		<relativePath /> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.pack</groupId>
	<artifactId>SpringUserDetails</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>
	<name>SpringUserDetails</name>
	<description>Spring MVC demo to read properties from a properties file</description>
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
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<!--Jasper dependeency need to be configured manually in order for Spring to process JSP pages-->
		<dependency>
			<groupId>org.apache.tomcat.embed</groupId>
			<artifactId>tomcat-embed-jasper</artifactId>
			<scope>provided</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<configuration>
					<excludes>
						<exclude>
							<groupId>org.projectlombok</groupId>
							<artifactId>lombok</artifactId>
						</exclude>
					</excludes>
				</configuration>
			</plugin>
		</plugins>
	</build>

</project>


```



## 4. Configure Application Properties
 - Setting logging level, port and context-path for best practice.
 - `application.properties` file will be inside `/src/main/resources` directory

 application.properties
```properties
spring.application.name=SpringUserDetails
server.port=2000
server.servlet.context-path=/mvc

spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp

logging.level.web=DEBUG
```


## 5. Create `user.properties`

`user.properties` in `C:\\user_properties\\user.properties`
```properties
user.fname=Ram
user.lname=Kumar
user.age=34
user.gender=male
user.city=Chennai
```

## 6. Create UserConfig.class
 - This is the entity configuration class with the Lombok attributes.
```java
package com.pack.SpringUserDetails;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import lombok.ToString;

@Configuration
@PropertySource("file:\\C:\\user_properties\\user.properties")
@ConfigurationProperties(prefix="user")
@Data //GetSet
@AllArgsConstructor
@NoArgsConstructor
@ToString
public class UserConfig {
	private String fname;
	private String lname;
	private Integer age;
	private String gender;
	private String city;	
}
```

## 7. Create UserController.class
- `Model` interface has been used to contain all the Model attributes, which will be referenced by `index.jsp`
```java
package com.pack.SpringUserDetails.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

import com.pack.SpringUserDetails.UserConfig;

@Controller
public class UserController {
	
	@Autowired
	private UserConfig config;
	
	@GetMapping("/user")
	public String getUser(Model model) {
		model.addAttribute("fname", config.getFname());
		model.addAttribute("lname", config.getLname());
		model.addAttribute("age", config.getAge());
		model.addAttribute("gender", config.getGender());
		model.addAttribute("city", config.getCity());
		return "index";
	}

}
```

## 8. Create `index.jsp`
- A table has been used here for better representation of data.
```jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Spring User Details</title>
</head>
<body>
	<h1>User Details</h1>
	<article>
		<table>
			<tbody>
				<tr>
					<td>User First Name :</td>
					<td><strong>${fname}</strong></td>
				</tr>
				<tr>
					<td>User Last Name :</td>
					<td><strong>${lname}</strong></td>
				</tr>
				<tr>
					<td>User Age :</td>
					<td><strong>${age}</strong></td>
				</tr>
				<tr>
					<td>User Gender :</td>
					<td><strong>${gender}</strong></td>
				</tr>
				<tr>
					<td>User City :</td>
					<td><strong>${city}</strong></td>
				</tr>
			</tbody>
		</table>
	</article>
</body>
</html>
```

## 9. Run the application from SpringUserDetailsApplication.class

```java
package com.pack.SpringUserDetails;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringUserDetailsApplication {
	public static void main(String[] args) {
		SpringApplication.run(SpringUserDetailsApplication.class, args);
	}
}
```

## 10. Outputs
- Browser Outputs:
![[Pasted image 20240616193850.png]]





---
# 3. Display Employee details in `employee.jsp`

Create Spring Boot MVC appl, to display employee details like name, age, salary in `employee.jsp `








![[Pasted image 20240617234004.png]]