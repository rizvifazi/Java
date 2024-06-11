
*Date : 06.10.2024*

---

Spring MVC - Where we return the response in view page(JSP/Thymeleaf)

client request - controller(handle req and res) - service(business logic) - repository - view page

1. Create spring boot project with spring web dependency with war packaging 

To make spring boot to understand JSP pages, we have to provide 1 dependency

<dependency>
                                           <groupId>org.apache.tomcat.embed</groupId>
                                           <artifactId>tomcat-embed-jasper</artifactId>
                                           <scope>provided</scope>
                             </dependency>

2. Create Controller program

@Controller
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


3. Create JSP page as per return value inside webapp - WEB-INF - views(any name) - create jsp page

<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
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

4. Configure jsp info in application.properties

spring.application.name=SpringBootMVC
server.port=1500
server.servlet.context-path=/mvc
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
#prefix+viewname+suffix=/WEB-INF/views/index.jsp

To pass value from controller prg to JSP prg we can use either ModelMap class or Model class or Map interface

<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
<h2>Welcome ${name} has age ${age} lives in ${address}</h2>
</body>
</html>

Spring Boot Jetty
1. Exclude tomcat server from web dependency

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

2. Comment spring boot starter tomcat, tomcat-embed-jasper dependency

3. Add spring boot Jetty and JSP Jetty dependency

                <dependency>
                                           <groupId>org.springframework.boot</groupId>
                                           <artifactId>spring-boot-starter-jetty</artifactId>
                             </dependency>

<dependency>
    <groupId>org.eclipse.jetty</groupId>
    <artifactId>apache-jsp</artifactId>
    <version>11.0.21</version>
</dependency>


Spring Boot Profiling
      - In enterprise appl we have many env like dev, test, prod etc and each env needs specific configuration related to that env and configured in application.properties, we cant configure everything in single file,so to use different properties files in different env we use profiling

1. We need to create different properties file related to env by application-profilename.properties (eg) application-dev.properties, application-prod.properties

2. spring.profiles.active=profilename in application.properties where it will invoke the related profile

@Value - used to read single property from properties files and write into controller prg 

@Profile - used to programmatically control files based on profiles 

application.properties

spring.application.name=SpringBoot1
server.port=2000
message=Welcome default user 
spring.profiles.active=prod

application-dev.properties

message=Welcome development user
server.port=3000

application-prod.properties

message=Welcome Production user
server.port=4000

@RestController
public class ProfileController {
              
              @Value("${message}") //SpEl - Spring Expression Language 
              private String msg;

              @GetMapping("/profile")
              public String hello() {
                             return "Hello world from Controller "+ msg;
              }
}

@Configuration
@Profile("dev")
public class AppConfig {
    @PostConstruct
              public void print() {
                             System.out.println("This methosd is invoked only in dev profile");
              }
}

By default Spring boot will read all configuration either from application.properties or application.yml

application.properties
1. It is represent as a sequence of key value pair

spring.application.name=SpringBoot1
server.port=1000
server.servlet.context-path=/app

2. This file is supported only in Java lang

3. support only key value pair and both in form of string

4. If we want handle different profiles then we have to create different properties files 

application.yml
1. It is represent in hiearchial format

server:
   port: 1000
   servlet:
      context-path: /app

spring:
   application:
      name: SpringBoot1

2. This file is supported in Java, Python etc

3. support scalar datatype, map, list, key value pairs

4. All configuration related to multiple profiles can be handled in single yml file

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


@PropertySource - used to read single property file with different name or in present different location 
@PropertySources - used to read muliple property file with different name or present in different location 

@ConfigurationProperties - used to map entire properties in properties file to a separate java bean object

Lombok dependency - to reduce boilerplate code (ie) getter, setter, default constructor, parameterized constructor, toString(), equals(), hashCode(), logging

student.properties
student.id=1000
student.name=Ram
student.address=Chennai
student.age=30

student1.properties
student.email=ram@gmail.com
student.course=CSE
student.mark=89


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


@Value
1. Injecting properties one by one
2. Support SpEL(${})
3. Loose binding/Loose Grammar is not supported (ie) attribute name should be matching
4. Validation of properties is not supported
5. support only scalar datatype

@ConfigurationProperties
1. Bulk injection of properties
2. Dosent support SpEL
3. Supports Loose Binding/Loose Grammar (ie) no need to match the attribute name(ie) special char or cases (eg) NAME, firstname(first-name)
4. Validation of properties is supported
5. support all datatypes as well as objects

mail.properties

#Scalar datatypes
mail.to=abc@gmail.com
mail.from=xyz@gmail.com
mail.age=25
mail.firstname=Ram
mail.lastname=Kumar

#Complex datatypes
mail.cc=uvw@gmail.com,pqr@gmail.com
mail.bcc=efg@gmail.com,klm@gmail.com

#Nested datatype
mail.credential.username=Ram
mail.credential.password=abcd12

To do validation

                <dependency>
                                           <groupId>org.hibernate.validator</groupId>
                                           <artifactId>hibernate-validator</artifactId>
                                           <version>6.0.5.Final</version>
                             </dependency>
                             <dependency>
                                           <groupId>javax.validation</groupId>
                                           <artifactId>validation-api</artifactId>
                                           <version>2.0.0.Final</version>
                             </dependency>

@Validated - to do validating the properties in properties files
@Valid - to do validation for nested class properties

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
   private String FIRSTNAME;
   private String LAST_NAME;
   
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
