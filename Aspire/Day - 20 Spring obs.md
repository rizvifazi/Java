
*Date : 06.07.2024*

---
# Spring Boot 3.0 framework
  - minimum JDK17 or above
  - open source framework, used to develop faster and both java based/web based appl, it is not replacement of Spring framework, it provides production ready appl so as a developer we are focusing mainly on business logic rather than doing all external configuration and downloading jar files
  - Developed by Pivotal team

## Advantage
1. easy to understand, develop faster appl so increase productivity
2. reduce ur development time
3. Avoid xml configuration
4. Everything is autoconfigured, so no need for manual configuration
5. Spring boot comes with embedded server like Apache Tomcat(default), Jetty, Undertow
6. Spring boot comes with in-memory database called h2 database used for testing purpose
7. Spring boot comes with in-built logging framework like logback,slf4j

## Drawbacks
1. Migration effort - converting from existing Spring project to Spring boot is not straight forward
2. Deploying Spring boot appl on other servers like Jboss, Weblogic etc is not straight forward
3. Developed Spring boot keeping microservice and cloud in mind


| Spring                                                            | Spring Boot                                                                                              |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| used to develop JavaEE framework for building appl(client+server) | used to develop REST API(server part/back end) based on MVC architecture                                 |
| main feature is Dependency Injection                              | Main feature is auto configuration                                                                       |
| develop loosely coupled appl                                      | create standalone appl with less configuration                                                           |
| write lot of boilerplate code                                     | reduce boilerplate code                                                                                  |
| We have explicitly configure the server                           | Spring boot comes with embedded server                                                                   |
| doesnt have any in-memory db                                      | comes with in-memory db called h2 db                                                                     |
| manually define dependency in pom.xml                             | Spring boot comes with spring-boot-starter-parent which will internally download all necessary jar files |
| requires bean configuration in xml file                           | No need for xml configuration                                                                            |



## Spring boot dependency management
  - manages dependencies and configuration in single place automatically
  - Avoid version conflicts
  - Spring-boot-starter-parent is a project starter, provide all basic configuration(jar files) to develop spring boot appl
  - dependency section tells maven what jar file to be downloaded, parent section tells what version of jar files to be downloaded

## Developing Spring boot appl - 3 ways
1. Using Spring Initializr - https://start.spring.io/
2. Using STS(Spring Tool Suite) - IDE for Spring boot appl
3. SpringBoot CLI(Command Line Interface) - using command prompt


## Spring Boot Annotations - 3 types

### 1. Spring Core Annotations
	1. @Bean
	2. @Configuration
	3. @Autowired
	4. @Qualifier
	5. @Primary
	6. @Scope
	7. @Component
	8. @Controller, @Service, @Repository

### 2. Spring MVC annotation 
  client gives request - Controller prg(used to handle req and res using `@Controller/@RestController`) - Service(used to write business logic using `@Service`) - Repository(using `@Repository`) - Database 

1. `@Controller` - return response in view page(JSP page)
2. `@RestController` - (`@Controller+@ResponseBody`) - return response in String or JSON format

3. `@RequestMapping` - used to map the request to particular method logic
`@RequestMapping(value="/fetchEmployee",method=RequestMethod.GET) `- used to give GET request
`@RequestMapping(value="/insertEmployee",method=RequestMethod.POST)` - used to give POST request
`@RequestMapping(value="/updateEmployee/{empid}",method=RequestMethod.PUT)` - used to give PUT request
`@RequestMapping(value="/deleteEmployee",method=RequestMethod.DELETE)` - used to give DELETE request

4. `@GetMapping, @PostMapping, @PutMapping, @DeleteMapping`

5. `@RequestBody` - used to read entire input data(ie) employee data in JSON format

`@RequestMapping(value="/updateEmployee/{empid}",method=RequestMethod.PUT)`
6. `@PathVariable` - used to get value from url request 

7. `@RequestParam` - used to get value of parameter transferred between ? and &

8. `@ResponseEntity` - represent HTTP response, body, status (404,503,200)
9. `@ResponseBody` - return entire body in JSON 

### 3. Spring boot annotation
1. `@SpringBootApplication` - `@EnableAutoConfiguration + @Configuration + @ComponentScan`


## Create Spring boot project using Spring Initialzr 

1. Go To
https://start.spring.io/

Project: `Maven`
Language: `Java`
Springboot version: `3.2.6`

Group: `com.pack`
Artifact: `SpringBoot1`
Packaging: `jar`
Java: `17`
`Click Add dependencies`

**Spring Web dependency** - Build web, including RESTful, applications using Spring MVC. Uses Apache Tomcat as the default embedded container.

`Click Generate`

2. Right click downloaded project - click Extract All - Click Browse - Choose `eclipse workspace` - Click Select Folder - Click Extract 

3. Goto File - New - Import - Select Existing Maven project - Click Next - Click Browse - Select extracted project from workspace - Click Select Folder - Click Finish

4. Right Click Project - Properties - Under Location - Copy project path - click Apply and close

5. Open new cmd prompt
>cd "paste ur project path"

`C:\Spring\SpringBoot1>mvn clean install`

6. Right click project - Maven - Update Project - check "Force Update" - click ok

> The above 6 steps must be followed for any of the spring boot projects


1. Create Controller program

```java
@RestController
public class ExampleController {

              @RequestMapping(value="/msg", method=RequestMethod.GET)
              public String getMessage() {
                             return "Hello Spring Boot";
              }
              
              @GetMapping(value="/msg1")
              public String getMessage1() {
                             return "Welcome Spring Boot";
              }
}
```

8. Start the appl

http://localhost:8080/msg
http://localhost:8080/msg1

By default Spring boot read all configuration from application.properties present src/main/resources

`http://localhost:8080/contextpath/msg` -> Including Context Path is a good practice

**application.properties** inside /src/main/resources
```
spring.application.name=Springboot1
server.port=2000
server.servlet.context-path=/app
```


9. Start the appl

http://localhost:2000/app/msg
http://localhost:2000/app/msg1

10. If we provide wrong request then we will be get "WhiteLabel Error page", instead we want to print some error messages for that purpose we need to implement `ErrorController` interface and override `getErrorPath()`

```java
@RestController
public class ExampleController implements ErrorController{

              private static final String PATH="/error";
              
              @RequestMapping(value="/msg", method=RequestMethod.GET)
              public String getMessage() {
                             return "Hello Spring Boot";
              }
              
              @GetMapping(value="/msg1")
              public String getMessage1() {
                             return "Welcome Spring Boot";
              }
              
              @GetMapping(value=PATH)
              public String getErrorMessage() {
                             return "Requested Resource does not exists";
              }
              
              public String getErrorPath() {
                             return PATH;
              }
}
```

11. When we create any program it should be always present as subpackage of main package, if we create outside main pkg then we have to use `@ComponentScan ` which is used to scan all the packages and execute the prg

```java
@SpringBootApplication
@ComponentScan(basePackages = {"com.hcl","com.pack.SpringBoot1"})
public class SpringBoot1Application {

              public static void main(String[] args) {
                             SpringApplication.run(SpringBoot1Application.class, args);
              }

}
```
12. Spring boot dev tools dependency - no need to restart server each time, when we make any changes in the appl, the server will automatically restarted 

```xml
<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
      <scope>runtime</scope>
      <optional>true</optional>
</dependency>
```

> Live reload plugin in chrome - ur browser automatically refreshes

13. CommandLineRunner interface -> Functional Interface
  - We can execute any task before Spring boot appl startup
  - `public void run(String...s) { }`


Springboot1Application.java
```java
package com.pack.Springboot1;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.core.annotation.Order;

@SpringBootApplication
@ComponentScan(basePackages = { "com.hcl", "com.pack.Springboot1" })
@Order(value = 2)
public class Springboot1Application implements CommandLineRunner {

	protected final static Log log = LogFactory.getLog(Springboot1Application.class);

	public static void main(String[] args) {
		SpringApplication.run(Springboot1Application.class, args);
		log.info("Inside main method");

	}

	@Override
	public void run(String... args) throws Exception {
		log.info("Inside run method");
	}

}

```


CommandLineRunner1.java
```java

```

CommandLineRunner2.java
```java

```

```java
@Component
@Order(value=3)
public class CommandLineRunner1 implements CommandLineRunner{

              protected final static Log log=LogFactory.getLog(CommandLineRunner1.class);
              
              @Override
              public void run(String... args) throws Exception {
                             log.info("Inside CommandLineRunner1");
              }

}

@Component
@Order(value=1)
public class CommandLineRunner2 implements CommandLineRunner{

              protected final static Log log=LogFactory.getLog(CommandLineRunner2.class);
              
              @Override
              public void run(String... args) throws Exception {
                             log.info("Inside CommandLineRunner2");
              }

}

@SpringBootApplication
@ComponentScan(basePackages = {"com.hcl","com.pack.SpringBoot1"})
@Order(value=2)
public class SpringBoot1Application implements CommandLineRunner{

              protected final static Log log=LogFactory.getLog(SpringBoot1Application.class);
              
              public static void main(String[] args) {
                             SpringApplication.run(SpringBoot1Application.class, args);
                             log.info("Inside main method");
              }

              @Override
              public void run(String... args) throws Exception {
                             log.info("Inside run method");
              }

}
```


Console output : 
```cmd

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v3.2.6)

2024-06-09T00:00:48.383+05:30  INFO 71148 --- [Springboot1] [  restartedMain] c.p.Springboot1.Springboot1Application   : Starting Springboot1Application using Java 17.0.7 with PID 71148 (C:\Users\acer\eclipse-workspace\Springboot1\Springboot1\target\classes started by acer in C:\Users\acer\eclipse-workspace\Springboot1\Springboot1)
2024-06-09T00:00:48.386+05:30  INFO 71148 --- [Springboot1] [  restartedMain] c.p.Springboot1.Springboot1Application   : No active profile set, falling back to 1 default profile: "default"
2024-06-09T00:00:48.428+05:30  INFO 71148 --- [Springboot1] [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : Devtools property defaults active! Set 'spring.devtools.add-properties' to 'false' to disable
2024-06-09T00:00:48.428+05:30  INFO 71148 --- [Springboot1] [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : For additional web related logging consider setting the 'logging.level.web' property to 'DEBUG'
2024-06-09T00:00:49.337+05:30  INFO 71148 --- [Springboot1] [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port 2000 (http)
2024-06-09T00:00:49.349+05:30  INFO 71148 --- [Springboot1] [  restartedMain] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2024-06-09T00:00:49.349+05:30  INFO 71148 --- [Springboot1] [  restartedMain] o.apache.catalina.core.StandardEngine    : Starting Servlet engine: [Apache Tomcat/10.1.24]
2024-06-09T00:00:49.395+05:30  INFO 71148 --- [Springboot1] [  restartedMain] o.a.c.c.C.[Tomcat].[localhost].[/app]    : Initializing Spring embedded WebApplicationContext
2024-06-09T00:00:49.397+05:30  INFO 71148 --- [Springboot1] [  restartedMain] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 966 ms
2024-06-09T00:00:49.813+05:30  INFO 71148 --- [Springboot1] [  restartedMain] o.s.b.d.a.OptionalLiveReloadServer       : LiveReload server is running on port 35729
2024-06-09T00:00:49.847+05:30  INFO 71148 --- [Springboot1] [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port 2000 (http) with context path '/app'
2024-06-09T00:00:49.861+05:30  INFO 71148 --- [Springboot1] [  restartedMain] c.p.Springboot1.Springboot1Application   : Started Springboot1Application in 1.777 seconds (process running for 2.155)
2024-06-09T00:00:49.866+05:30  INFO 71148 --- [Springboot1] [  restartedMain] c.p.Springboot1.Springboot1Application   : Inside CommandLineRunner2
2024-06-09T00:00:49.866+05:30  INFO 71148 --- [Springboot1] [  restartedMain] c.p.Springboot1.Springboot1Application   : Inside run method
2024-06-09T00:00:49.866+05:30  INFO 71148 --- [Springboot1] [  restartedMain] c.p.Springboot1.Springboot1Application   : Inside CommandLineRunner1
2024-06-09T00:00:49.867+05:30  INFO 71148 --- [Springboot1] [  restartedMain] c.p.Springboot1.Springboot1Application   : Inside main method
```
ApplicationRunner interface
          - We can execute any task before Spring boot appl startup
          - public void run(ApplicationArgument a) {
            }
