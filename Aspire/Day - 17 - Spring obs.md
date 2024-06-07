
*Date : 05.27.2024*


# Spring Annotations

```java
@Configuration
@Bean
@Scope  // prototype 
@Primary // If same bean is configured multiple times
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
```

```java
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
```


Main.java
```java
package com.pack;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {

	public static void main(String[] args) {

		ApplicationContext context = new AnnotationConfigApplicationContext(ExampleConfiguration.class);
		
		Example1 e1 = (Example1)context.getBean(Example1.class);
		e1.setMessage1("Hello world!");
		System.out.println(e1);
		
		Example1 e2 = (Example1)context.getBean(Example1.class);
		e2.setMessage1("Hello world!");
		System.out.println(e2);
		
		Example1 e3 = (Example1)context.getBean(Example1.class);
		e3.setMessage1("Hello world!");
		System.out.println(e3);
		
		Example3 e4 = (Example3)context.getBean(Example3.class);
		System.out.println(e4); // Example3 [message3=Struts Framework]
	
	}

}
```

Output :
```cmd
com.pack.Example1@5af3afd9
com.pack.Example1@323b36e0
com.pack.Example1@44ebcd03
Example3 [message3=Struts Framework]

```
## `@Autowired`  
- Used to inject one bean into another bean, perform autowiring based on `ByType` . This will be checked internally   
- Used above only `setter method` or `constructor` or `fields` (variables).  
- If we use autowire by annotation, in order to make Spring understand the annotation we have to configure `<context:annotation-config/>` in the XML file.
- We are not using the ExampleConfiguration class here, instead we are going for the XMLconfiguration

Address.java
```java
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
```

Student.java
```java
public class Student {
    private Integer id;
    private String name;
    private Integer age;
    
    @Autowired //mentioned above field
    private Address address; // referred another bean

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

    // @Autowired - can be also mentioned above settor method or constructor
    public void setAddress(Address address) {
        this.address = address;
    }
}
```

Hello.java  -  `<context:annotation-config/>` can be added above addr bean or stud bean
```xml
<context:annotation-config/>
	<bean id="addr" class="com.pack.Address">
		<property name="city" value="Chennai"></property>
		<property name="state" value="Tamilnadu"></property>
		<property name="zipcode" value="600028"></property>
	</bean>
	
	
	<bean id="stud" class="com.pack.Student">
		<property name="id" value="1000"></property>
		<property name="name" value="Ram"></property>
		<property name="age" value="20"></property>
	</bean>
```

Main.java
```java
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx = new FileSystemXmlApplicationContext("hello.xml");
        Student st = (Student) ctx.getBean("stud");
        System.out.println(st.getName() + " lives in " + st.getAddress().getCity());
    }
}
```

Output:
```cmd
Ram lives in Chennai
```

## `@Qualifier`  
If the same bean is configured multiple times in the XML file, which bean has to be injected while using `@Autowired` is decided using `@Qualifier`. This always need to be defined with autowired.

```xml
<context:annotation-config/>
	<!--@Autowired will choose by type, Address type is configured twice here-->
	<!--@Qualifier(id) always need to be used with only @Autowired-->
	<bean id="addr" class="com.pack.Address">
		<property name="city" value="Chennai"></property>
		<property name="state" value="Tamilnadu"></property>
		<property name="zipcode" value="600028"></property>
	</bean>
	
	<bean id="addr1" class="com.pack.Address"> 
		<property name="city" value="Mumbai"></property>
		<property name="state" value="Maharashtra"></property>
		<property name="zipcode" value="000108"></property>
	</bean>
	
	
	<bean id="stud" class="com.pack.Student">
		<property name="id" value="1000"></property>
		<property name="name" value="Ram"></property>
		<property name="age" value="20"></property>
	</bean>
```

Student.java
```java
public class Student {
    private Integer id;
    private String name;
    private Integer age;

    @Autowired
    @Qualifier("addr1")
    private Address address; // referred another bean

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

    // @Autowired
    // @Qualifier("addr1")
    public void setAddress(Address address) {
        this.address = address;
    }
}
```

Output:
```cmd
Ram lives in Mumbai
```

## `@Required`
- Used to annotate the required fields. Deprecated, so no need to focus on this.

## Stereotype Annotation
- `@Controller` (indicates it is a controller program, used to handle your request and response)
- `@Service` (indicates it is a service program, which is used to write all business logic)
- `@Repository` (indicates it is a repository program where it will communicate with the database)
- `@Component` also used to refer as a single bean program so that we can inject this program into another program using `@Autowired`

## Lazy Loading vs Eager Loading

### BeanFactory is Lazy loading 
- It creates the bean only when we call `getBean()` method.
- BeanFactory only supports IOC, dependency injection through XML file.
- Performance wise BF is more advantageous.
- To get lazy loading in AC we use 
	- Using `lazy-init="true"` in XML file
	- Using `@Lazy` annotation

e.g.:

Sample.java
```java
public class Sample {

	public Sample() {
		System.out.println("Sample1 bean is initiated with constructor");
	}
}
```

Sample2.java
```java
public class Sample2 {
	private Sample sample;

	public Sample getSample() {
		return sample;
	}

	public void setSample(Sample sample) {
		this.sample = sample;
	}
	
	public Sample2() {
		System.out.println("Sample2 bean is initiated with constructor");
	}

}
```

Hello.xml
```xml
	<bean id="sample" class="com.pack.Sample"></bean>
	<bean id="sample2" class="com.pack.Sample2">
		<property name="sample" ref="sample"/>
	</bean>
```

Main.java -1
```java
import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.FileSystemResource;
import org.springframework.core.io.Resource;

public class Main {

	public static void main(String[] args) {
		
		Resource res = new FileSystemResource("Hello.xml");
		BeanFactory bf = new XmlBeanFactory(res);
		Sample2 s2 = (Sample2) bf.getBean("sample2"); //id from Hello.xml
		
	}

}
```

Output -1
```cmd
Sample2 bean is initiated with constructor
Sample1 bean is initiated with constructor
```

Main.java -2
```java
public class Main {

	public static void main(String[] args) {
		
		Resource res = new FileSystemResource("Hello.xml");
		BeanFactory bf = new XmlBeanFactory(res);
		//Sample2 s2 = (Sample2) bf.getBean("sample2"); //id from Hello.xml
		
	}

}
```

Output -2 : No output
```cmd

```

### ApplicationContext is Eager loading 
- Preloads all the beans at the time of startup itself.
- It supports IOC and more features like Internationalization, Remoting, Life Cycle events, Scheduling , emailing and etc.
- Feature wise ApplicationContext is advantageous. 

Using `lazy-init="true"` for the bean in XML file
Using `@Lazy` annotation

```java
public class Main {

	public static void main(String[] args) {
		
		//Resource res = new FileSystemResource("Hello.xml");
		//BeanFactory bf = new XmlBeanFactory(res);
		//Sample2 s2 = (Sample2) bf.getBean("sample2"); //id from Hello.xml
		
		ApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml");
		
	}

}
```

Output:
```cmd
Sample1 bean is initiated with constructor
Sample2 bean is initiated with constructor
```

 so we have to convert ApplicationContext to be lazy loading.

Hello.xml
```xml
<bean id="sample" class="com.pack.Sample" lazy-init="true"></bean>
<bean id="sample2" class="com.pack.Sample2" lazy-init="true">
	<property name="sample" ref="sample"/>
</bean>
	
```

Main.java
```java
public class Main {
	public static void main(String[] args) {
		
		ApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml");
		
	}
}
```

Output: No output
```cmd
```

Altering Main.java
```java
public class Main {
	public static void main(String[] args) {
		
		ApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml");
		Sample2 s2 = (Sample2)context.getBean("sample2");
		
	}
}
```

Output: 
```cmd
Sample2 bean is initiated with constructor
Sample1 bean is initiated with constructor
```

### @Lazy - example

Configuration class with constructor without @Lazy
```java
import org.springframework.context.annotation.Configuration;


@Configuration
public class ExampleConfiguration {
	
	public ExampleConfiguration() {
		System.out.println("ExampleConfiguration initiated!");
	}
}
```

Main.java
```java
package com.pack;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {

	public static void main(String[] args) {
		
		ApplicationContext context =  new AnnotationConfigApplicationContext(ExampleConfiguration.class);	
	}

}

```

Output: 
```cmd
ExampleConfiguration initiated!
```

Updated Configuration with @Lazy
```java
@Configuration
@Lazy
public class ExampleConfiguration {
	
	public ExampleConfiguration() {
		System.out.println("ExampleConfiguration initiated!");
	}
}
```

Output: No output
```cmd
```


## Lifecycle of Spring Bean


- Manage lifecycle using `InitializingBean` and `DisposableBean` interface .
	`InitializingBean` interface - 1 method`public void afterPropertiesSet()` - Invoked whenever a bean is instantiated using `getBean()` method
	`DisposableBean` interface - 1 method `public void destroy()` - Invoked whenever your bean is destroyed

### 1. ConfigurableApplicationContext interface
or
Abstract class `AbstractApplicationContext` implements `ConfigurableApplicationContext`  

Either you can use  `ConfigurableApplicationContext` or  `AbstractApplicationContext` instead of `ApplicationContext`
#### Destroy a bean
`void registerShutdownHook()` - Used to destroy the bean, this is best practice than the following
or  
`void close()`


`close()` -- Close this application context, destroying all beans in its bean factory.  
`registerShutdownHook()` -- Register a shutdown hook with the JVM runtime, closing this context on JVM shutdown unless it has already been closed at that time.


Person.java
```java
package com.pack;

import org.springframework.beans.factory.DisposableBean;
import org.springframework.beans.factory.InitializingBean;

public class Person implements InitializingBean,DisposableBean {  //Note the interfaces 
	
	private String name;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public void destroy() throws Exception { //Method from DisposableBean interface
		System.out.println("Destroynig the bean");
	}

	@Override
	public void afterPropertiesSet() throws Exception { //Methos from  InitializingBean interface
		System.out.println("Initializing the bean");
	}
}

```

Hello.xml - Setter injection 
```xml
	<bean id="person" class="com.pack.Person">
		<property name="name" value="Ram"/>			
	</bean>
```

Main.java
```java
package com.pack;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Main {

	public static void main(String[] args) {

		AbstractApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml"); //can use ConfigurableApplicationInterface
		Person p = (Person) context.getBean("person");
		System.out.println("Name is : " + p.getName());
		context.registerShutdownHook();  //best practice
		//context.close  //not recomended
	}

}

```

Output:
```cmd
Initializing the bean
Name is : Ram
Destroynig the bean
```

> Spring can understand the predefined lifecycle methods and annotations above. For specifying custom methods see below.
### 2. Custom Init and Custom Destroy
- Configuring the custom methods in the bean class and configure the beans inside xml.

Person.java with custom lifecycle methods.
```java
package com.pack;

public class Person {
	
	private String name;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public void customInit() { // Custom destroy method
		System.out.println("Initializing the bean");
	}
	
	public void customDestroy() { //Custom destroy method
		System.out.println("Destroynig the bean");
	}
}

```

Hello.xml with custom init and destroy methods configured in beans
```xml
	<bean id="person" class="com.pack.Person" init-method="customInit" destroy-method="customDestroy">
		<property name="name" value="Ram"/>			
	</bean>
```

Main.java
```java
package com.pack;

import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Main {

	public static void main(String[] args) {

		ConfigurableApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml"); //Abstract can use
		Person p = (Person) context.getBean("person");
		System.out.println("Name is : " + p.getName());
		context.registerShutdownHook();
	}

}

```

Output:
```cmd
Initializing the bean
Name is : Ram
Destroynig the bean
```

> This need to configured for all the beans individually, so it is better to go with the default init and destroy methods below.


### 3. Default init and destroy method.

`default-init-method="customInit"` and `default-destroy-method="customDestroy"` in tag, so these methods are applicable for all beans

Person.java
```java
package com.pack;

public class Person {
	
	private String name;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public void customInit() { // Custom destroy method
		System.out.println("Initializing the bean");
	}
	
	public void customDestroy() { //Custom destroy method
		System.out.println("Destroynig the bean");
	}
}

```


Hello.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
						http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd"
						default-init-method="customInit" default-destroy-method="customDestroy">


	<bean id="person" class="com.pack.Person">
		<property name="name" value="Ram"/>			
	</bean>

</beans>
```

Main.java
```java
package com.pack;

import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Main {

	public static void main(String[] args) {

		ConfigurableApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml");
		Person p = (Person) context.getBean("person");
		System.out.println("Name is : " + p.getName());
		context.registerShutdownHook();
	}

}

```

Output:
```
Initializing the bean
Name is : Ram
Destroynig the bean
```

### 4. Using `@PostConstruct` and `@PreDestroy` annotations.

- We'll look into this in later parts using Spring Boot.





# JPA - Java Persistence API
- It is a specification (inbuilt annotation) to persist the data into the database
- Initially we used JDBC concept

> Every programs goal will be to capture data into the database. For that purpose we use JDBC concept.
## JDBC  
EJB 2.x Entity Bean - Failure in performance  
EJB 3.x - JPA - Java Persistence API

- JPA will contain inbuilt annotations to connect with the database and ORM framework actually let JPA connect with the database.


### ORM (Object Relational Mapping) Framework  
- It is providers (or) vendors who provide the implementation using ORM tools like **Hibernate**, **iBatis**, **TopLink**, **JDO**, etc.  
- Used to map POJO class (entity/persistent class) to the columns of the database table.

#### Features
1. Open source and lightweight
2. Database independent query
	- JPAQL (Java Persistent Query Language) - Query the entity class
	- SQL - Query the table
3. Automatic table creation based on the entity class
4. Generate SQL queries automatically
5. Faster in performance - Uses **cache framework**, consequent DB reads will be read from cache, primary cache.
6. Simplifies complex joins


### Steps to Configure JPA

1. Configure all database info and Hibernate properties

```xml
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
```


## JPA - Java Persistence API
- Initially present in `javax.persistence` but from Spring Boot 3.0 it is present in `jakarta.persistence`.
- It is a specification (inbuilt annotation) to persist the data into the database.
- Collection of annotations, classes, and interfaces to persist data into DB.

##### 1.`EntityManagerFactory` interface - Used to create `EntityManager`

`EntityManager createEntityManagerFactory(String persistname);`  

##### 2.`EntityManager` interface - Core interface used to persist the data into DB - Acts as an interface between your application and database

```java
void persist(Object o) // Used to insert the data into DB if the primary key does not exist, if the primary key exists it performs update operation - generates insert or update query
Object find(Serializable s, Object pk) // Used to select single data from DB - generates select query
void remove(Object o) // Deletes data from DB - generates delete query
void close()
boolean contains(Object o)
EntityTransaction getTransaction() // Creates a transaction
Query createQuery(String query) // Writes JPAQL
Query createNativeQuery(String query) // Writes SQL
Query createNamedQuery(String name) // Identifies query based on names
CriteriaBuilder getCriteriaBuilder()
```

##### 3.`EntityTransaction` interface - Used to maintain the transaction

```java
void commit()
void rollback()
```

##### 4. `Query` interface - Used to write database independent query

---------------------------------
References : 
- [github.com/benod44/SpringMongoMapping](https://github.com/benod44/SpringMongoMapping)

- [www.apptunix.com/blog/kotlin-vs-java/](https://www.apptunix.com/blog/kotlin-vs-java/)

- [github.com/TekskillsInc/USOnboarding](https://github.com/TekskillsInc/USOnboarding)

- [en.wikipedia.org/wiki/Java_annotation](https://en.wikipedia.org/wiki/Java_annotation)

- [medium.com/oreillymedia/write-shorter-cleaner-more-modern-java-code-with-kotlin-8f0d88b67cf9](https://medium.com/oreillymedia/write-shorter-cleaner-more-modern-java-code-with-kotlin-8f0d88b67cf9)

- [github.com/Padmini-B/springdemos](https://github.com/Padmini-B/springdemos)

