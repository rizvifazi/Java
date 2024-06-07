
*Date : 06.07.2024*


Handson
1.	Create spring boot appl to display employee info in json format 

Spring Boot 3.0 framework
      - minimum JDK17 or above
      - open source framework, used to develop faster and both java based/web based appl, it is not replacement of Spring framework, it provides production ready appl so as a developer we are focussing mainly on business logic rather than doing all external configuration and downloading jar files
      - Developed by Pivotal team

Advantage
1. easy to understand, develop faster appl so increase productivity
2. reduce ur development time
3. Avoid xml configuration
4. Everything is autoconfigured, so no need for manual configuration
5. Spring boot comes with embedded server like Apache Tomcat(default), Jetty, Undertow
6. Spring boot comes with in-memory database called h2 database used for testing purpose
7. Spring boot comes with in-built logging framework like logback,slf4j

Drawbacks
1. Migration effort - converting from existing Spring project to Spring boot is not straight forward
2. Deploying Spring boot appl on other servers like Jboss, Weblogic etc is not straight forward
3. Developed Spring boot keeping microservice and cloud in mind

Spring 
1. used to develop JavaEE framework for building appl(client+server)
2. main feature is Dependency Injection
3. develop loosely coupled appl
4. write lot of boilerplate code
5. We have explicitly configure the server
6. doesnt have any in-memory db
7. manually define dependency in pom.xml
8. requires bean configuration in xml file

Springboot
1. used to develop REST API(server part/back end) based on MVC architecture
2. Main feature is auto configuration
3. create standalone appl with less configuration
4. reduce boilerplate code
5. Spring boot comes with embedded server
6. comes with in-memory db called h2 db
7. Spring boot comes with spring-boot-starter-parent which will internally download all necessary jar files
8. No need for xml configuration

Spring boot dependency management
      - manages dependencies and configuration in single place automatically
      - Avoid version conflicts
      - Spring-boot-starter-parent is a project starter, provide all basic configuration(jar files) to develop spring boot appl
      - dependency section tells maven what jar file to be downloaded, parent section tells what version of jar files to be downloaded

Developing Spring boot appl - 3 ways
1. Using Spring Initializr - https://start.spring.io/
2. Using STS(Spring Tool Suite) - IDE for Spring boot appl
3. SpringBoot CLI(Command Line Interface) - using command prompt


Spring Boot Annotations - 3 types
1. Spring Core Annotations
        1. @Bean
        2. @Configuration
        3. @Autowired
        4. @Qualifier
        5. @Primary
        6. @Scope
        7. @Component
        8. @Controller, @Service, @Repository

2. Spring MVC annotation 
      client gives request - Controller prg(used to handle req and res using @Controller/@RestController) - Service(used to write business logic using @Service) - Repository(using @Repository) - Database 

1. @Controller - return response in view page(JSP page)
2. @RestController - (@Controller+@ResponseBody) - return response in String or JSON format

3. @RequestMapping - used to map the request to particular method logic
@RequestMapping(value="/fetchEmployee",method=RequestMethod.GET) - used to give GET request
@RequestMapping(value="/insertEmployee",method=RequestMethod.POST) - used to give POST request
@RequestMapping(value="/updateEmployee/{empid}",method=RequestMethod.PUT) - used to give PUT request
@RequestMapping(value="/deleteEmployee",method=RequestMethod.DELETE) - used to give DELETE request

4. @GetMapping, @PostMapping, @PutMapping, @DeleteMapping

5. @RequestBody - used to read entire input data(ie) employee data in JSON format

@RequestMapping(value="/updateEmployee/{empid}",method=RequestMethod.PUT)
6. @PathVariable - used to get value from url request 

7. @RequestParam - used to get value of parameter transferred between ? and &

8. @ResponseEntity - represent HTTP response, body, status
9. @ResponseBody - return entire body in JSON 

3. Spring boot annotation
1. @SpringBootApplication - @EnableAutoConfiguration + @Configuration + @ComponentScan

1. Create Spring boot project using Spring Initialzr 

https://start.spring.io/

Project: Maven
Language: Java
Springboot version: 3.2.6

Group: com.pack
Artifact: SpringBoot1
Packaging: jar
Java: 17
Click Add dependencies

Spring Web dependency - Build web, including RESTful, applications using Spring MVC. Uses Apache Tomcat as the default embedded container.

Click Generate

2. Right click downloaded project - click Extract All - Click Browse - Choose eclipse workspace - Click Select Folder - Click Extract 

3. Goto File - New - Import - Select Existing Maven project - Click Next - Click Browse - Select extracted project from workspace - Click Select Folder - Click Finish

4. Right Click Project - Properties - Under Location - Copy project path - click Apply and close

5. Open new cmd prompt
>cd "paste ur project path"

C:\Spring\SpringBoot1>mvn clean install

6. Right click project - Maven - Update Project - check "Force Update" - click ok

7. Create Controller program

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

8. Start the appl

http://localhost:8080/msg
http://localhost:8080/msg1

By default Spring boot read all configuration from application.properties present src/main/resources

http://localhost:8080/contextpath/msg

server.port=2000
server.servlet.context-path=/app

9. Start the appl

http://localhost:2000/app/msg
http://localhost:2000/app/msg1

10. If we provide wrong request then we will be get "WhiteLabel Error page", instead we want to print some error messages for that purpose we need to implement ErrorController interface and override getErrorPath()

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

11. When we create any program it should be always present as subpackage of main package, if we create outside main pkg then we have to use @ComponentScan  which is used to scan all the packages and execute the prg

@SpringBootApplication
@ComponentScan(basePackages = {"com.hcl","com.pack.SpringBoot1"})
public class SpringBoot1Application {

              public static void main(String[] args) {
                             SpringApplication.run(SpringBoot1Application.class, args);
              }

}
12. Spring boot dev tools dependency - no need to restart server each time, when we make any changes in the appl, the server will automatically restarted 

<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
      <scope>runtime</scope>
      <optional>true</optional>
    </dependency>

Live reload plugin in chrome - ur browser automatically refreshes

13. CommandLineRunner interface
          - We can execute any task before Spring boot appl startup
          - public void run(String...s) {
            }

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

ApplicationRunner interface
          - We can execute any task before Spring boot appl startup
          - public void run(ApplicationArgument a) {
            }

