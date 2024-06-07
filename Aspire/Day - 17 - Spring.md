
*Date : 05.27.2024*

Spring Annotations
1. @Configuration
2. @Bean
3. @Scope
4. @Primary - If same bean is configured multiple times 

public class Example3 {
   private String message3;

@Override
public String toString() {
              return "Example3 [message3=" + message3 + "]";
}

public Example3() {
              super();
              // TODO Auto-generated constructor stub
}

public Example3(String message3) {
              super();
              this.message3 = message3;
}
   
   
}


@Configuration
public class ExampleConfiguration {

              @Bean
              public Example1 example1() {
                             return new Example1();
              }
              @Bean
              @Scope("prototype")
              public Example2 example2() {
                             return new Example2();
              }
              
              @Bean
              public Example3 example3() {
                             return new Example3("Spring framework");
              }
              @Bean
              @Primary
              public Example3 example31() {
                             return new Example3("Struts framework");
              }
              @Bean
              public Example3 example32() {
                             return new Example3("Hibernate framework");
              }
}


5. @Autowired
       - used to inject one bean into an another bean, perform autowiring based on by type
       - used above only setter method or constructor or fields(variables)
       - If we use autowire by annotation, in order to make spring to understand the annotation we have to configure <context:annotation-config/> in xml file

public class Address {
   private String city;
   private String state;
   private String zipcode;
public String getCity() {
              return city;
}
public void setCity(String city) {
              this.city = city;
}
public String getState() {
              return state;
}
public void setState(String state) {
              this.state = state;
}
public String getZipcode() {
              return zipcode;
}
public void setZipcode(String zipcode) {
              this.zipcode = zipcode;
}
   
}


public class Student {
   private Integer id;
   private String name;
   private Integer age;
   @Autowired
   private Address address;  //referred another bean
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
public Integer getAge() {
              return age;
}
public void setAge(Integer age) {
              this.age = age;
}
public Address getAddress() {
              return address;
}
//@Autowired
public void setAddress(Address address) {
              this.address = address;
}
  
   
}


<context:annotation-config/>
    <bean id="addr" class="com.pack.Address">
       <property name="city" value="Chennai"/>
       <property name="state" value="Tamilnadu"/>
       <property name="zipcode" value="600117"/>
    </bean>    
    <bean id="stud" class="com.pack.Student">
       <property name="id" value="1000"/>
       <property name="name" value="Ram"/>
       <property name="age" value="20"/>
    </bean>

public class Main {

              public static void main(String[] args) {
                             ApplicationContext ctx=new FileSystemXmlApplicationContext("hello.xml");
                             Student st=(Student)ctx.getBean("stud");
                             System.out.println(st.getName()+" lives in "+st.getAddress().getCity());
              }

}


6. @Qualifier
     - If same bean is configured multiple times in xml file, which bean has to  be injected while using @Autowired is decided using @Qualifier

<context:annotation-config/>
    <bean id="addr" class="com.pack.Address">
       <property name="city" value="Chennai"/>
       <property name="state" value="Tamilnadu"/>
       <property name="zipcode" value="600117"/>
    </bean>  
    <bean id="addr1" class="com.pack.Address">
       <property name="city" value="Mumbai"/>
       <property name="state" value="Maharastra"/>
       <property name="zipcode" value="200117"/>
    </bean>    
    <bean id="stud" class="com.pack.Student">
       <property name="id" value="1000"/>
       <property name="name" value="Ram"/>
       <property name="age" value="20"/>
    </bean>

public class Student {
   private Integer id;
   private String name;
   private Integer age;
   @Autowired
   @Qualifier("addr1")
   private Address address;  //referred another bean
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
public Integer getAge() {
              return age;
}
public void setAge(Integer age) {
              this.age = age;
}
public Address getAddress() {
              return address;
}
//@Autowired
public void setAddress(Address address) {
              this.address = address;
}
  
   
}

7. Sterotype annotation
      - @Controller(indicate it is a controller prg, used to handle ur request and response)
      - @Service (indicate it is a service prg, which is used to write all business logic)
      - @Repository (indicate it is a repository prg where it will communicate with database) 
      - @Component also used to refer as a single bean prg so that we can inject this program into other program using @Autowired


BeanFactory is Lazy loading - It creates the bean only when we call getBean()

ApplicationContext is Eager loading - preloads all the beans at the time of startup itself, so we have to convert ApplicationContext to be lazy loading
  1. using lazy-init="true" in xml file
  2. using @Lazy annotation 

public class Sample1 {

              public Sample1() {
                             System.out.println("Sample1 bean is instantiated");
              }

}


public class Sample2 {
    private Sample1 sample1;

              public Sample1 getSample1() {
                             return sample1;
              }

              public void setSample1(Sample1 sample1) {
                             this.sample1 = sample1;
              }

              public Sample2() {
                             System.out.println("Sample2 bean is instantiated");
              }
    
    
}


<bean id="sample1" class="com.pack.Sample1" lazy-init="true"/>
    <bean id="sample2" class="com.pack.Sample2" lazy-init="true">
        <property name="sample1" ref="sample1"/>
    </bean>


public class Main {

              public static void main(String[] args) {
                             //Resource res=new FileSystemResource("hello.xml");
                             //BeanFactory bf=new XmlBeanFactory(res);
                             //Sample2 s2=(Sample2)bf.getBean("sample2");
                             
                             ApplicationContext ctx=new FileSystemXmlApplicationContext("hello.xml");
                             Sample2 s2=(Sample2)ctx.getBean("sample2");
              }

}

Lifecycle of Spring bean
1. Using InitializingBean and DisposableBean interface

InitializingBean interface - public void afterPropertiesSet() - invoked whenever a bean is instantiated using getBean()
DisposableBean interface - public void destroy() - invoked whenever ur bean is destroyed

ConfigurableApplicationContext interface
- abstract class AbstractApplicationContext implements ConfigurableApplicationContext
void registerShutdownHook() - used to destroy the bean
     or
void close() 

public class Person implements InitializingBean,DisposableBean{
   private String name;

public String getName() {
              return name;
}

public void setName(String name) {
              this.name = name;
}

public void destroy() throws Exception {
              System.out.println("Destroying Person bean");
}

public void afterPropertiesSet() throws Exception {
              System.out.println("Initializing Person bean "+name);
}
   
   
}

<bean id="person" class="com.pack.Person">
       <property name="name" value="Ram"/>
    </bean>


public class Main {

              public static void main(String[] args) {
                             AbstractApplicationContext ctx=new FileSystemXmlApplicationContext("hello.xml");
                             Person p=(Person)ctx.getBean("person");
                             System.out.println(p.getName());
                             //ctx.registerShutdownHook();
                             ctx.close();
              }

}

close() -- Close this application context, destroying all beans in its bean factory.
registerShutdownHook() -- Register a shutdown hook with the JVM runtime, closing this context on JVM shutdown unless it has already been closed at that time.

2. custom init and custom destroy

public class Person {
   private String name;

public String getName() {
              return name;
}

public void setName(String name) {
              this.name = name;
}

public void customInit() {
              System.out.println("Initializing Person bean");
}
   
public void customDestroy() {
              System.out.println("Destroying Person bean");
}
}

<bean id="person" class="com.pack.Person" init-method="customInit"
          destroy-method="customDestroy">
       <property name="name" value="Ram"/>
    </bean>

public class Main {

              public static void main(String[] args) {
                             ConfigurableApplicationContext ctx=new FileSystemXmlApplicationContext("hello.xml");
                             Person p=(Person)ctx.getBean("person");
                             System.out.println(p.getName());
                             //ctx.registerShutdownHook();
                             ctx.close();
              }

}

3. default-init-method="customInit" and default-destroy-method="customDestroy" in <beans> tag, so these method are applicable for all beans

4. Using @PostConstruct and @PreDestroy annotation


JPA - Java Persistence API
    - It is a specification(inbuilt annotation) to persist the data into database 

JDBC
EJB 2.x Entity Bean - Failure in performance
EJB 3.x - JPA - Java Persistence API

ORM(Object Relational Mapping) Framework
     - It is providers (or) vendors who provides the implementation using ORM tools like Hibernate, iBatis, TopLink, JDO etc
     - Used to map POJO class(entity/persistent class) to the columns of the database table

Features
1. open source and lightweight
2. Database independent query
      JPAQL(Java Persistent Query Language) - query the entity class
      SQL - query the table
3. Automatic table creation based on the entity class
4. Generate SQL queries automatically
5. Faster in performance - use cache framework
6. Simplifies complex joins

1. Configure all database info and Hibernate properties 

<!--Database information-->
<property name="connection.url">jdbc:mysql://localhost:3306/aspirejava</property>
<property name="connection.driver_class">com.mysql.jdbc.driver</property>
<property name="connection.username">root</property>
<property name="connection.password">root</property>

<!--Hibernate properties-->
<property name="hbm2ddl.auto">create/update/create-drop/validate</property> - will automatically creates the tables - 4 values
   1. create - each time it will create new table
   2. update - it will create table for first time, and next time it will update the data in table(ie) append the data
   3. create-drop - it drop the entire db and create the table
   4. validate - it dosent do anything it just validate the existing table

<property name="dialect">org.hibernate.dialect.MySQLDialect</property>
     - we can communicate with database using queries or using predefined methods
     - We wont write any sql queries, instead we use some predefined methods to process in the database, so hibernate internally generate sql queries related to the particular method and based on particular database 

<property name="show_sql">true</property>
    - used to display generated sql query on the console in single line
<property name="format_sql">true</property>
    - used to format and display generated sql query on the console
<property name="use_sql_comments">true</property>
    - used to define comment stmt for generated sql query in the console 

JPA - Java Persistence API 
    - initially present in javax.persistence.* but from Spring Boot 3.0 it is present in jakarta.persistence.*
    - It is a specification(inbuilt annotation) to persist the data into database 
    - Collection of annotataion, classes and interface to persist data into db

1. EntityManagerFactory interface - used to create EntityManager
       - EntityManager createEntityManagerFactory(String persistname);

2. EntityManager interface - core interface used to persist the data into db - acts as an interface between ur appl and database
       - void persist(Object o) - used to insert the data into db if primary does not exist, if primary key exists it performs update operation - generate insert or update query
       - Object find(Serailizable s, Object pk) - used to select single data from db - generate select query
       - void remove(Object o) - delete data from db - generate delete query
       - void close()
       - boolean contains(Object o)
       - EntityTransaction getTransaction() - create a transaction
       - Query createQuery(String query) - write JPAQL 
       - Query createNativeQuery(String query) - write sql
       - Query createNamedQuery(String name) - identify query based on names
       - CriteriaBuilder getCriteriaBuilder()

3. EntityTransaction interface - used to maintain the transaction
       - void commit()
       - void rollback()

4. Query interface - used to write database independent query




---------------------------------
References : 
- [github.com/benod44/SpringMongoMapping](https://github.com/benod44/SpringMongoMapping)

- [www.apptunix.com/blog/kotlin-vs-java/](https://www.apptunix.com/blog/kotlin-vs-java/)

- [github.com/TekskillsInc/USOnboarding](https://github.com/TekskillsInc/USOnboarding)

- [en.wikipedia.org/wiki/Java_annotation](https://en.wikipedia.org/wiki/Java_annotation)

- [medium.com/oreillymedia/write-shorter-cleaner-more-modern-java-code-with-kotlin-8f0d88b67cf9](https://medium.com/oreillymedia/write-shorter-cleaner-more-modern-java-code-with-kotlin-8f0d88b67cf9)

- [github.com/Padmini-B/springdemos](https://github.com/Padmini-B/springdemos)

