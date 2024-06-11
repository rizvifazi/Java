
*Date : 05.20.2024*


J2EE - to develop web oriented appl - J2EE Components - Traditional approach 
1. JSP - Java Server Pages - HTML+Java - used to create dynamic webpages - ui
2. Servlet - java prg used to write business logic
3. Enterprise Java Bean(EJB) - develop enterprise appl - 3 types
      1. Session bean - write business logic
      2. Entity bean - persist anything into db
      3. Message Driven Bean - send sync and async messages

Problems with traditional approach
1. J2EE applications tend to contain excessive amounts of "plumbing" code -> Thers would always be a high proportion of code that doesn't do anything: JNDI lookup code, Transfer Objects, try/catch blocks to acquire and release JDBC resources. Writing and maintaining such plumbing code proves a major drain on resources that should be focused on the application's business domain. 

2. J2EE applications are hard to unit test -> The J2EE APIs, especially, the EJB component model, does not take into account ease of unit testing. It is very difficult to test applications based on EJB and many other J2EE APIs outside an application server. 

3. Certain J2EE technologies have failed in performance. EJB 2.x, for instance -> The main offender here is entity beans, which have proven little short of disastrous for productivity.


J2EE Frameworks
There are many frameworks which claim to resolve the issues mentioned earlier. For instance, Struts.

Struts is a web framework which works on the web tier and helps us achieve MVC and is doing pretty well in the market. However Spring takes over struts in that it is not just a web framework but an application framework.

Unlike single-tier frameworks such as Struts or Hibernate, Spring aims to help structure whole applications in a consistent, productive manner. It has modules that offer services for use throughout an application.

The essence of Spring is in providing enterprise services to Plain Old Java Objects (POJOs). This is valuable in a J2EE environment.

Spring framework
    - open source framework, used to develop both standalone(java) as well as web appl. It is a framework so we have to download jar files and put inside appl

Features
1. Reduce glue code/plumbing work
Spring Framework takes lot of load off the programmer by providing dependencies when required and by using AOP(Aspect Oriented Programming) - define common functionality in single program and access it wherever it is needed. 

2. Externalize dependencies - Inversion of Control(IOC) - Dependency Injection
Dependencies are described in a separate file (xml) rather than mixing it with the business logic code itself. This gives a better control over the application.
   Loosely coupled appl - inject the value at runtime in separate xml file

3. Manage dependencies at a single place
Dependencies can be managed better due to this.

4. Improve testability
Actual code can easily be replaced by a stub for testing purposes.

5. Foster good application design
Since the actual implementation sits behind the interfaces, it fosters good application design.

6. Flexibility
Spring offers integration points with several other frameworks. So, you do not have to write them yourself. 

## 7 modules
### 1. Spring core module
  - support IOC features
  - Using BeanFactory interface

2. Spring Context module
      - support IOC features + support internationalization, lifecycle events, remoting, scheduling, emailing, integrating with EJB, Velocity, FreeMarker etc
      - Using ApplicationContext interface

3. Spring AOP(Aspect Oriented Programming)
      - define common functionality in single program and access it wherever it is needed
       eg: security, transaction, logging

4. Spring DAO(Data Access Object) module
       - Spring itself provides inbuilt interface to connect with database (JdbcTemplate)

5. Spring ORM(Object Relational Mapping) module
     - Used to integrate Spring with Hibernate

6. Spring Webflow module
     - Used to integrate Spring with Struts 

7. Spring MVC module
     - used to develop web tier based on MVC architecture within Spring itself

