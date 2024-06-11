
*Date : 05.24.2024*

# Inversion of Control 
- Achieved through DI.

# Dependency Injection - 3 types
   - objects are given their dependencies at **runtime** in separate **xml** file.

### 1. Setter injection - Spring 
  - dependencies are configured through beans **setter method** for their properties using `<property>` tag. 
### 2. Constructor injection - Spring
 - dependencies are configured through **beans constructor** for their properties using `<constructor-args>` tag
### 3. Interface injection - Avalon 
  - dependencies are configured **through interface** for their properties. Spring doesn't support interface injection.

## Spring IOC containers - 2 types of IOC container are there to perform DI
We can use either of the below 2 to perform DI.

### 1. BeanFactory interface
   - `org.springframework.beans.factory.*` package
   - It is **lazy loading** by default
   - used to **create** and **destroy** the bean at runtime.
   - Cannot create objects as it's an interface.
   - Using `XmlBeanFactory(Resource r)`class - used to load the beans defined in xml file
   - `Object getBean(String)` - used to instantiate the bean and runtime and performs DI    
   - Only supports IOC container. This is more memory efficient.
### 2. ApplicationContext interface
   - `org.springframework.context.* `package
   - It is **eager loading**
   - used to create and destroy the bean 
   - Has a lot of features.
   - 3 classes
	1. `ClasspathXmlApplicationContext(String xmlfilename)` - loads the xml file present in **classpath** (ie) /src (main java folder)
	2. `FileSystemXmlApplicationContext(String xmlfilename)` - loads the xml file present in **project** or inside the **file system** (ie) c:/ or d:/
	3. `WebXmlApplicationContext(String xmlfilename)` - loads the xml file from **web.xml**

### To build any Spring Application - 3 programs
1. **Bean program** - simple **POJO(Plain Old Java Object)** class that contains `getters` and `setters`
2. **xml file** - configure bean program to perform DI
3. **main class**


> As Spring is a framework, we need to include all the JAR files. Instead we can use the Maven Tool to download all the required JAR files.

## Apache maven
- It is a project development tool, instead of downloading jar files manually, maven will download all jar files on behalf of the user from internet
- **pom.xml**(project object model) - we have to provide the dependencies
- Maven contains 2 repo
	1. **Remote repository** - for first time maven will download all jar files remotely present in internet and put in the local repo.
	2. **Local repository** - maven will internally create a repo locally in your machine(ie) .m2 folder.

### Setup Maven
1. Download maven
	https://maven.apache.org/download.cgi
	Binary zip archive -> apache-maven-3.9.6-bin.zip

2. Extract zip file

3. Set env variable for maven

4. Type env in search - Select "Edit env variable for your account"

5. Under User variables - Select New

6. Variable name: MAVEN_HOME
	Variable value: C:\Softwares\apache-maven-3.6.3

7. Click ok

8.  Select Path - Click Edit - Click New - Paste C:\Softwares\apache-maven-3.6.3\bin

9. Click OK - Click ok

10. Open new cmd prompt

```PowerShell
Microsoft Windows [Version 10.0.22635.3640]
(c) Microsoft Corporation. All rights reserved.

C:\Users\acer>mvn --version
Apache Maven 3.9.6 (bc0240f3c744dd6b6ec2920b3cd08dcc295161ae)
Maven home: C:\apache-maven-3.9.6-bin\apache-maven-3.9.6
Java version: 17.0.7, vendor: Oracle Corporation, runtime: C:\Program Files\Java\jdk-17
Default locale: en_US, platform encoding: Cp1252
OS name: "windows 11", version: "10.0", arch: "amd64", family: "windows"

C:\Users\acer>mvn clean
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.078 s
[INFO] Finished at: 2024-05-25T12:37:01+05:30
[INFO] ------------------------------------------------------------------------
[ERROR] The goal you specified requires a project to execute but there is no POM in this directory (C:\Users\acer). Please verify you invoked Maven from the correct directory. -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MissingProjectException

C:\Users\acer>cd .m2

C:\Users\acer\.m2> --Local Repository
```


## Getting Started with Maven Project
1. Create java maven project 
	Click File -> New -> Other -> Maven project -> Next 

- [ ] check Create a simple project -> click Next 

	Group id: `com.pack`(any pkg name)
	Artifact id: `Spring1`(any project name)
	Packaging: `jar` (jar for Java Application / war for Web Application)
	click Finish

2. Configure spring dependency in `pom.xml` . (We will be only discussing **Core** and **Context** out of 7 spring modules.)
	- Search and configure dependencies from Maven Repository https://mvnrepository.com (Remote Repo)
		
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd"> --If error right click Force download
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.pack</groupId>
	<artifactId>Spring1</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<dependencies>
		<!-- https://mvnrepository.com/artifact/org.springframework/spring-core -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-core</artifactId>
			<version>5.3.9</version> <!--Use 5.3.9 as BeanFactory is not supported beyond that-->
		</dependency>
		<!--https://mvnrepository.com/artifact/org.springframework/spring-context -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
			<version>5.3.9</version> <!--Use 5.3.9 as BeanFactory is not supported beyond that-->
		</dependency>
	</dependencies>

</project>
```


3. Right click project (`Spring1`) -> click `Properties` -> copy path from Location `C:\Users\acer\eclipse-workspace\Spring1` -> click `apply and close` 

4. Open `cmd` prompt
```PowerShell
C:\Users\acer\.m2> cd C:\Users\acer\eclipse-workspace\Spring1

C:\Users\acer\eclipse-workspace\Spring1>mvn clean install -- This will download all dependencied to the local repository (.m2)
[INFO] Scanning for projects...
[INFO]
[INFO] --------------------------< com.pack:Spring1 >--------------------------
[INFO] Building Spring1 0.0.1-SNAPSHOT
[INFO]   from pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- clean:3.2.0:clean (default-clean) @ Spring1 ---
[INFO] Deleting C:\Users\acer\eclipse-workspace\Spring1\target
[INFO]
[INFO] --- resources:3.3.1:resources (default-resources) @ Spring1 ---
[WARNING] Using platform encoding (Cp1252 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] Copying 0 resource from src\main\resources to target\classes
[INFO]
[INFO] --- compiler:3.11.0:compile (default-compile) @ Spring1 ---
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- resources:3.3.1:testResources (default-testResources) @ Spring1 ---
[WARNING] Using platform encoding (Cp1252 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] Copying 0 resource from src\test\resources to target\test-classes
[INFO]
[INFO] --- compiler:3.11.0:testCompile (default-testCompile) @ Spring1 ---
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- surefire:3.2.2:test (default-test) @ Spring1 ---
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/3.2.2/maven-surefire-common-3.2.2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/3.2.2/maven-surefire-common-3.2.2.pom (6.1 kB at 4.5 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/3.2.2/surefire-api-3.2.2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/3.2.2/surefire-api-3.2.2.pom (3.4 kB at 12 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-logger-api/3.2.2/surefire-logger-api-3.2.2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-logger-api/3.2.2/surefire-logger-api-3.2.2.pom (3.2 kB at 11 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-shared-utils/3.2.2/surefire-shared-utils-3.2.2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-shared-utils/3.2.2/surefire-shared-utils-3.2.2.pom (4.1 kB at 13 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-extensions-api/3.2.2/surefire-extensions-api-3.2.2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-extensions-api/3.2.2/surefire-extensions-api-3.2.2.pom (3.2 kB at 11 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/3.2.2/surefire-booter-3.2.2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/3.2.2/surefire-booter-3.2.2.pom (4.3 kB at 15 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-extensions-spi/3.2.2/surefire-extensions-spi-3.2.2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-extensions-spi/3.2.2/surefire-extensions-spi-3.2.2.pom (1.7 kB at 2.8 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/4.0.0/plexus-utils-4.0.0.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/4.0.0/plexus-utils-4.0.0.pom (8.7 kB at 7.1 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/13/plexus-13.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/13/plexus-13.pom (27 kB at 55 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/eclipse/sisu/org.eclipse.sisu.plexus/0.9.0.M2/org.eclipse.sisu.plexus-0.9.0.M2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/eclipse/sisu/org.eclipse.sisu.plexus/0.9.0.M2/org.eclipse.sisu.plexus-0.9.0.M2.pom (15 kB at 33 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/eclipse/sisu/sisu-plexus/0.9.0.M2/sisu-plexus-0.9.0.M2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/eclipse/sisu/sisu-plexus/0.9.0.M2/sisu-plexus-0.9.0.M2.pom (15 kB at 32 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/eclipse/sisu/org.eclipse.sisu.inject/0.9.0.M2/org.eclipse.sisu.inject-0.9.0.M2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/eclipse/sisu/org.eclipse.sisu.inject/0.9.0.M2/org.eclipse.sisu.inject-0.9.0.M2.pom (17 kB at 23 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/eclipse/sisu/sisu-inject/0.9.0.M2/sisu-inject-0.9.0.M2.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/eclipse/sisu/sisu-inject/0.9.0.M2/sisu-inject-0.9.0.M2.pom (15 kB at 27 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-component-annotations/2.1.0/plexus-component-annotations-2.1.0.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-component-annotations/2.1.0/plexus-component-annotations-2.1.0.pom (750 B at 2.7 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/commons-io/commons-io/2.12.0/commons-io-2.12.0.pom
Downloaded from central: https://repo.maven.apache.org/maven2/commons-io/commons-io/2.12.0/commons-io-2.12.0.pom (20 kB at 16 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/commons/commons-parent/57/commons-parent-57.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/commons/commons-parent/57/commons-parent-57.pom (83 kB at 46 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-java/1.2.0/plexus-java-1.2.0.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-java/1.2.0/plexus-java-1.2.0.pom (4.3 kB at 13 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-languages/1.2.0/plexus-languages-1.2.0.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-languages/1.2.0/plexus-languages-1.2.0.pom (3.2 kB at 9.7 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/15/plexus-15.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus/15/plexus-15.pom (28 kB at 39 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/junit/junit-bom/5.10.0/junit-bom-5.10.0.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/junit/junit-bom/5.10.0/junit-bom-5.10.0.pom (5.6 kB at 15 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/ow2/asm/asm/9.6/asm-9.6.pom
Downloaded from central: https://repo.maven.apache.org/maven2/org/ow2/asm/asm/9.6/asm-9.6.pom (2.4 kB at 7.4 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/3.2.2/maven-surefire-common-3.2.2.jar
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/maven-surefire-common/3.2.2/maven-surefire-common-3.2.2.jar (309 kB at 46 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/3.2.2/surefire-api-3.2.2.jar
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-logger-api/3.2.2/surefire-logger-api-3.2.2.jar
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-extensions-api/3.2.2/surefire-extensions-api-3.2.2.jar
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/3.2.2/surefire-booter-3.2.2.jar
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-extensions-spi/3.2.2/surefire-extensions-spi-3.2.2.jar
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-extensions-spi/3.2.2/surefire-extensions-spi-3.2.2.jar (8.2 kB at 9.2 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/commons-io/commons-io/2.12.0/commons-io-2.12.0.jar
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-extensions-api/3.2.2/surefire-extensions-api-3.2.2.jar (26 kB at 29 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-java/1.2.0/plexus-java-1.2.0.jar
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-logger-api/3.2.2/surefire-logger-api-3.2.2.jar (14 kB at 15 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/ow2/asm/asm/9.6/asm-9.6.jar
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-booter/3.2.2/surefire-booter-3.2.2.jar (118 kB at 88 kB/s)
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-shared-utils/3.2.2/surefire-shared-utils-3.2.2.jar
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-api/3.2.2/surefire-api-3.2.2.jar (171 kB at 111 kB/s)
Downloaded from central: https://repo.maven.apache.org/maven2/org/ow2/asm/asm/9.6/asm-9.6.jar (124 kB at 61 kB/s)
Downloaded from central: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-java/1.2.0/plexus-java-1.2.0.jar (58 kB at 16 kB/s)
Downloaded from central: https://repo.maven.apache.org/maven2/commons-io/commons-io/2.12.0/commons-io-2.12.0.jar (474 kB at 74 kB/s)
Downloaded from central: https://repo.maven.apache.org/maven2/org/apache/maven/surefire/surefire-shared-utils/3.2.2/surefire-shared-utils-3.2.2.jar (2.3 MB at 181 kB/s)
[INFO]
[INFO] --- jar:3.3.0:jar (default-jar) @ Spring1 ---
[INFO] Building jar: C:\Users\acer\eclipse-workspace\Spring1\target\Spring1-0.0.1-SNAPSHOT.jar
[INFO]
[INFO] --- install:3.1.1:install (default-install) @ Spring1 ---
[INFO] Installing C:\Users\acer\eclipse-workspace\Spring1\pom.xml to C:\Users\acer\.m2\repository\com\pack\Spring1\0.0.1-SNAPSHOT\Spring1-0.0.1-SNAPSHOT.pom
[INFO] Installing C:\Users\acer\eclipse-workspace\Spring1\target\Spring1-0.0.1-SNAPSHOT.jar to C:\Users\acer\.m2\repository\com\pack\Spring1\0.0.1-SNAPSHOT\Spring1-0.0.1-SNAPSHOT.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  34.075 s
[INFO] Finished at: 2024-05-25T13:15:44+05:30
[INFO] ------------------------------------------------------------------------
```

5. Right click `Project` - click `Maven` - Click `Update Project` - choose - `[x] Force update on snapshot` -> Click `Finish` 
> 	 Whenever adding/removing dependencies -> mvn clean install && Update Project.

###### *All the above 5 steps are mandatory for any Spring Project, new you can move ahead with your custom programming logic.*

### Creating the required 3 programs

6. Create bean program inside `src/main/java`

Student.java
```java
public class Student {
	private Integer id;
	private String name;
	private int age;

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

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}
}
```


**Whenever we create a bean program we need to configure it in the xml file.**

7. Create xml file in **any name** inside `src` or inside `project`
      - used to configure bean program inside xml file and to perform DI
      - contain root element called `<beans>` and each bean is configured using `<bean>`.
   1. ` id` - any name - which acts as an object for bean class.
   2. `class` - fully qualified path of bean class.

hello.xml
- Force download any links if shown as error.
- The following will be injected to the program at **runtime**.
- The following XML Schema definition is provided by spring so the program will be able to identify at runtime.
```xml

<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns=http://www.springframework.org/schema/beans
    xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance
    xmlns:context=http://www.springframework.org/schema/context
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context-3.0.xsd"> <!--XML Schema definition-->
	<!--Setter Injection with the help of poperty tag-->
    <bean id="stud" class="com.pack.Student">
       <property name="id" value="1000"/>
       <property name="name" value="Ram"/>
       <property name="age" value="20"/>
    </bean>

</beans>
```

8. Create main class

	Resource is an **interface** used to locate xml file - 2 classes
	  1. `ClassPathResource class` - if xml file present inside src
	  2. `FileSystemResource class` - if xml file present inside project/filesystem

### Using BeanFactory
Main.java
```java
package com.pack;

import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.ClassPathResource;
import org.springframework.core.io.Resource;

public class Main {

	public static void main(String[] args) {
		Resource res = new ClassPathResource("Hello.xml"); // locate the XML file inside /src
		BeanFactory factory = new XmlBeanFactory(res); // Deprecated/ load beans from xml file
		Student s = (Student) factory.getBean("stud"); // should be the id from Hello.xml <bean id="stud"
														// class="com.pack.Student">
		// instantiate the bean with id stud and performs DI -- Setter Injection for Id,
		// name, and age
		// factory will return Object so it need to be type-casted for Student Object.

		System.out.println(s.getName() + " " + s.getAge());
	}

}
```

Output
```cmd
Ram 20
```


> Move Hello.xml to the project folder by Refactoring, then the above needs to be converted as below using **FileSystemResource** class.

```java
//Resource res = new ClassPathResource("Hello.xml"); // locate the XML file inside /src
Resource res = new FileSystemResource("Hello.xml"); // locate the XML file inside project /Filesystem
```
Output
```cmd
Ram 20
```


### Using Application Context
Main.java
```java
package com.pack;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Main {

	public static void main(String[] args) {

		ApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml"); //since Hello.xml is moved from src to filesystem.
		Student s = (Student) context.getBean("stud");
		System.out.println(s.getName() + " " + s.getAge());

	}

}
```


### Create new Employee bean class (For constructor DI)

Employee.java
```java
package com.pack;

public class Employee {

	private Integer id;
	private String name;
	private Double salary;
	private int age; // Note this is int not Integer
	
	//No need to create getters and setters as we are using this for constructor injection
	//default constructor
	public Employee() {
		super();
	}

	//parameterized constructor
	public Employee(Integer id, String name, Double salary, int age) {
		super();
		this.id = id;
		this.name = name;
		this.salary = salary;
		this.age = age;
	}

	//To String Method
	@Override
	public String toString() {
		return "Employee [id=" + id + ", name=" + name + ", salary=" + salary + ", age=" + age + "]";
	}
	
}

```

Employee bean class need to be configured in `Hello.xml`
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
						http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd">

	<bean id="stud" class="com.pack.Student">
		<property name="id" value="1000" />
		<property name="name" value="Ram" />
		<property name="age" value="20" />
	</bean>
	
	<!--Using Constructor injection-->
	<bean id="emp" class="com.pack.Employee">
		<constructor-arg name="id" type="java.lang.Integer" value="1001"></constructor-arg>
		<constructor-arg name="name" type="java.lang.String" value="Sam"></constructor-arg>
		<constructor-arg name="salary" type="java.lang.Double" value="20000"></constructor-arg>
		<constructor-arg name="age" type="int" value="25"></constructor-arg>
		<!--Above is int and all the others are wrapper classes-->
	</bean>
</beans>
```

Main.java
```java
package com.pack;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Main {

	public static void main(String[] args) {

		ApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml");
		Employee employee = (Employee) context.getBean("emp");
		System.out.println(employee.toString());
	}
}

```

Output
```cmd
Employee [id=1001, name=Sam, salary=20000.0, age=25]
```


Instead of injecting using the name attribute, we can use the index attribute, index is in the order of parameter list in the constructor.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
						http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd">

	<bean id="stud" class="com.pack.Student">
		<property name="id" value="1000" />
		<property name="name" value="Ram" />
		<property name="age" value="20" />
	</bean>
	
	<!--
	<bean id="emp" class="com.pack.Employee">
		<constructor-arg name="id" type="java.lang.Integer" value="1001"></constructor-arg>
		<constructor-arg name="name" type="java.lang.String" value="Sam"></constructor-arg>
		<constructor-arg name="salary" type="java.lang.Double" value="20000"></constructor-arg>
		<constructor-arg name="age" type="int" value="25"></constructor-arg>
		Above is int and all the others are wrapper classes
	</bean>-->
	
	<bean id="emp" class="com.pack.Employee">
		<constructor-arg index="0" type="java.lang.Integer" value="1001"></constructor-arg>
		<constructor-arg index="1" type="java.lang.String" value="Sam"></constructor-arg>
		<constructor-arg index="2" type="java.lang.Double" value="20000"></constructor-arg>
		<constructor-arg index="3" type="int" value="25"></constructor-arg>
	</bean>
	
</beans>

```

Output
```cmd
Employee [id=1001, name=Sam, salary=20000.0, age=25]
```



## Spring Scope
   - lifetime of bean object - 5 types

1. **singleton** - default - how many bean object we are creating it will have same reference. One object will be created per container.

Comment out the `toString()` method in  Employee class.

Employee.java
```java
/**To String Method
	@Override
	public String toString() {
		return "Employee [id=" + id + ", name=" + name + ", salary=" + salary + ", age=" + age + "]";
	}
	**/
```

Main.java
```java
package com.pack;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Main {

	public static void main(String[] args) {

		ApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml");
		
		Employee employee = (Employee) context.getBean("emp");
		System.out.println(employee);
		Employee employee1 = (Employee) context.getBean("emp");
		System.out.println(employee1);
		Employee employee2 = (Employee) context.getBean("emp");
		System.out.println(employee2);

	}

}
```

Output : Outputs the same object reference
```cmd
com.pack.Employee@4a22f9e2
com.pack.Employee@4a22f9e2
com.pack.Employee@4a22f9e2
```


2. **prototype** - how many bean object we are creating it will have different/new reference. Whenever it sends the request, every time it creates a new object.

```xml
	<bean id="emp" class="com.pack.Employee" scope="prototype"> <!--Scope is set to prototype-->
       <constructor-arg index="0" type="java.lang.Integer" value="1001"></constructor-arg>
       <constructor-arg index="1" type="java.lang.String" value="Sam"></constructor-arg>
       <constructor-arg index="2" type="java.lang.Double" value="20000"></constructor-arg>
       <constructor-arg index="3" type="int" value="25"></constructor-arg>
    </bean>
```

Output : Outputs the different object reference 
```cmd
com.pack.Employee@4a22f9e2
com.pack.Employee@3c419631
com.pack.Employee@418e7838
```

> No any changes required to the Main class

To have different data we need to create 3 different beans.

Below are only for web applications
3. request
4. session
5. global-session 


> Creation of object using new operator is done at Compile-time, dependency injection is done at Runtime. Even if we built the application, we can pass the values to the application using DI- Runtime. No re compilation required. Unit Test done with this use case.

## Injecting collections
- Apart from primitive datatypes we can also inject collections (ie)` List, Set, Map, Properties`

List - Ordered and Allow duplicates
Set - Unordered and No Duplicates, Unique
Map - No duplicate key/ key value pair
Properties - Key also a string

![[Collections#^b03bcd]]




CollectionExamle.java
```java
package com.pack;

import java.util.List;
import java.util.Map;
import java.util.Set;
import java.util.Properties;


public class CollectionExamle {

	private List nameList;
	private Set nameSet;
	private Map nameMap;
	private Properties nameProp;
	
	public List getNameList() {
		return nameList;
	}
	public void setNameList(List nameList) {
		this.nameList = nameList;
	}
	public Set getNameSet() {
		return nameSet;
	}
	public void setNameSet(Set nameSet) {
		this.nameSet = nameSet;
	}
	public Map getNameMap() {
		return nameMap;
	}
	public void setNameMap(Map nameMap) {
		this.nameMap = nameMap;
	}
	public Properties getNameProp() {
		return nameProp;
	}
	public void setNameProp(Properties nameProp) {
		this.nameProp = nameProp;
	}
	
}
```


Hello.xml
```xml
<bean id="collect" class="com.pack.CollectionExamle">
		<property name="nameList">
			<list>
				<value>Ram</value>
				<value>Sam</value>
				<value>Ram</value>
				<value>Tam</value>
			</list>
		</property>
		<property name="nameSet">
			<set>
				<value>Ram</value>
				<value>Sam</value>
				<value>Ram</value>
				<value>Tam</value>
			</set>
		</property>
		<property name="nameMap">
			<map>
				<entry key="1" value="Ram"></entry>
				<entry key="2" value="Sam"></entry>
				<entry key="3" value="Ram"></entry>
				<entry key="4" value="Tam"></entry>
			</map>
		</property>
		<property name="nameProp">
			<props>
				<prop key="one">Ram</prop>
				<prop key="two">Sam</prop>
				<prop key="three">Ram</prop>
				<prop key="four">Tam</prop>
			</props>
		</property>
	</bean>
	
</beans>
```

Main.java

```java
package com.pack;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Main {

	public static void main(String[] args) {

		ApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml");
		CollectionExamle clt = (CollectionExamle)context.getBean("collect");
		
		System.out.println(clt.getNameList());
		System.out.println(clt.getNameSet());
		System.out.println(clt.getNameMap());
		System.out.println(clt.getNameProp());
	
	}

}
```

Output:
```cmd
[Ram, Sam, Ram, Tam]
[Ram, Sam, Tam]
{1=Ram, 2=Sam, 3=Ram, 4=Tam}
{four=Tam, one=Ram, two=Sam, three=Ram}
```


# Wiring - referring one bean into an another bean
## ref attribute
- used to refer one bean into an another bean
- ref="id of the bean"


Address.java class to be included with Student class
```java
package com.pack;

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

New Student class with Address
```java
package com.pack;

public class Student {
	private Integer id;
	private String name;
	private int age;
	private Address address; //referred another bean

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

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public Address getAddress() {
		return address;
	}

	public void setAddress(Address address) {
		this.address = address;
	}
	

}

```

Updates Hello.xml
```xml
	<bean id="addr" class="com.pack.Address">
		<property name="city" value="Chennai"></property>
		<property name="state" value="Tamilnadu"></property>
		<property name="zipcode" value="600028"></property>
	</bean>


	<bean id="stud" class="com.pack.Student">
		<property name="id" value="1000"></property>
		<property name="name" value="Ram"></property>
		<property name="age" value="20"></property>
		<property name="address" ref="addr"></property> <!--Setter injection is done when comming to this line-->
		<!--ref attribute for manually wiring address--> 
	</bean>
```

Main.java
```java
package com.pack;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Main {

	public static void main(String[] args) {

		ApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml");
		Student s=(Student)context.getBean("stud");
		System.out.println(s.getName()+" lives in "+s.getAddress().getCity()); // getting the city from address
	
	}

}
```

Output
```cmd
Ram lives in Chennai
```

## Auto-wiring
- used only in case of referring one bean into an another bean
- Instead of using `"ref"` attribute we can go for **autowiring** to inject one bean into an another bean automatically

### Types of Autowiring

1. `autowire=none` - default - where we have to do injection using ref attribute, when no autowiring is defined.


Match.java
```java
package com.pack;

public class Match {
	private String location;
	private String distance;

	public String getLocation() {
		return location;
	}

	public void setLocation(String location) {
		this.location = location;
	}

	public String getDistance() {
		return distance;
	}

	public void setDistance(String distance) {
		this.distance = distance;
	}

}

```

Student.java
```java
package com.pack;

public class Player {
	private Integer playerId;
	private String name;
	private Match match;

	public Integer getPlayerId() {
		return playerId;
	}

	public void setPlayerId(Integer playerId) {
		this.playerId = playerId;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Match getMatch() {
		return match;
	}

	public void setMatch(Match match) {
		this.match = match;
	}

}

```

Hello.xml
```xml
	<bean id="match" class="com.pack.Match">
		<property name="location" value="Chennai"></property>
		<property name="distance" value="1000km"></property>
	</bean>
	
	<bean id="play" class="com.pack.Player">
		<property name="playerId" value="100"></property>
		<property name="name" value="Virat"></property>
		<property name="match" ref="match"></property> <!--refer the id of the match class-->
	</bean>

```

Main.java
```java
package com.pack;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Main {

	public static void main(String[] args) {

		ApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml");
		Player p = (Player) context.getBean("play");
		System.out.println(p.getName() + " plays in " + p.getMatch().getLocation()); //get location from match

	}

}

```

Output
```cmd
Virat plays in Chennai
```


2. `autowire=byName` - name of the property in class matches id of the bean in xml file, then it will do autowire by name. 
```xml
	<bean id="match" class="com.pack.Match">
		<property name="location" value="Chennai"></property>
		<property name="distance" value="1000km"></property>
	</bean>
	
	<bean id="play" class="com.pack.Player" autowire="byName">
		<property name="playerId" value="100"></property>
		<property name="name" value="Virat"></property>
		<!-- ref attribute removed -->
	</bean>
```
Output
```cmd
Virat plays in Chennai
```



3. `autowire=byType` - If datatype of the property should be configured in xml file then it will do autowire by type 
We can configure the same bean multiple times but it should not have the same id.
```xml
	<bean id="match1" class="com.pack.Match"> <!--Type of match class is defined here using class-->
		<property name="location" value="Chennai"></property>
		<property name="distance" value="1000km"></property>
	</bean>
	
	<bean id="play" class="com.pack.Player" autowire="byType">
		<property name="playerId" value="100"></property>
		<property name="name" value="Virat"></property>
		 <!-- ref attribute removed -->
	</bean>

```
Output
```cmd
Virat plays in Chennai
```


4. `autowire=constructor`  - similar to `byType` but it will do injection through constructor 
Remove the Getters and setter -> create default and parameterized constructor.

Match.java
```java
package com.pack;

public class Match {
	private String location;
	private String distance;

	public Match() {
		super();
	}

	public Match(String location, String distance) {
		super();
		this.location = location;
		this.distance = distance;
	}

	@Override
	public String toString() {
		return "Match [location=" + location + ", distance=" + distance + "]";
	}

}
```

Player.java
```java
package com.pack;

public class Player {
	private Integer playerId;
	private String name;
	private Match match;

	public Player() {
		super();
	}

	public Player(Integer playerId, String name, Match match) {
		super();
		this.playerId = playerId;
		this.name = name;
		this.match = match;
	}

	@Override
	public String toString() {
		return "Player [playerId=" + playerId + ", name=" + name + ", match=" + match + "]";
	}

}

```


Hello.xml -> Use `<constructor-arg>` for constructor injection
```xml
	<bean id="match1" class="com.pack.Match"> <!--Type of match class is defined here using class-->
		<constructor-arg name="location" value="Chennai"></constructor-arg>
		<constructor-arg name="distance" value="1000km"></constructor-arg>
	</bean>
	
	<bean id="play" class="com.pack.Player" autowire="constructor">
		<constructor-arg name="playerId" value="100"></constructor-arg>
		<constructor-arg name="name" value="Virat"></constructor-arg>
		 <!-- ref attribute removed -->
	</bean>
```


Main.java
```java
package com.pack;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

public class Main {

	public static void main(String[] args) {

		ApplicationContext context = new FileSystemXmlApplicationContext("Hello.xml");
		Player p = (Player) context.getBean("play");
		System.out.println(p); //get location from match
	}

}

```

Output
```cmd
Player [playerId=100, name=Virat, match=Match [location=Chennai, distance=1000km]]
```


`autowire-candidate=false`
    - If same bean is configured multiple times in xml file, which bean class has to be injected, it is defined using autowire-candidate property
    - So which bean u don't want to use it, we have to provide `autowire-candidate=false`
    
```xml
	<bean id="match1" class="com.pack.Match" autowire-candidate="false"> <!--Type of match class is defined here using class-->
		<constructor-arg name="location" value="Chennai"></constructor-arg>
		<constructor-arg name="distance" value="1000km"></constructor-arg>
	</bean>
	
		<bean id="match2" class="com.pack.Match" > <!--Here we have 2 beans with same Type configured, candidate false-->
		<constructor-arg name="location" value="Mumbai"></constructor-arg>
		<constructor-arg name="distance" value="2000km"></constructor-arg>
	</bean>
	
	<bean id="play" class="com.pack.Player" autowire="constructor">
		<constructor-arg name="playerId" value="100"></constructor-arg>
		<constructor-arg name="name" value="Virat"></constructor-arg>
		 <!-- ref attribute removed -->
	</bean>
```


Output
```cmd
Player [playerId=100, name=Virat, match=Match [location=Mumbai, distance=2000km]]
```


`primary=true`
    - If same bean is configured multiple times in xml file, which bean class has to be injected, it is defined using primary property
    - So which bean u want to use it, we have to provide primary=true

```xml
	<bean id="match1" class="com.pack.Match"> <!--Type of match class is defined here using class-->
		<constructor-arg name="location" value="Chennai"></constructor-arg>
		<constructor-arg name="distance" value="1000km"></constructor-arg>
	</bean>
	
		<bean id="match2" class="com.pack.Match" primary="true"> <!--Here we have 2 beans with same Type configured, candidate false-->
		<constructor-arg name="location" value="Mumbai"></constructor-arg>
		<constructor-arg name="distance" value="2000km"></constructor-arg>
	</bean>
	
	<bean id="play" class="com.pack.Player" autowire="constructor">
		<constructor-arg name="playerId" value="100"></constructor-arg>
		<constructor-arg name="name" value="Virat"></constructor-arg>
		 <!-- ref attribute removed -->
	</bean>
```

Output
```cmd
Player [playerId=100, name=Virat, match=Match [location=Mumbai, distance=2000km]]
```

# Spring using Annotations
- used instead of configuring bean inside xml file

## @Configuration 
- class level annotation, something like xml file, where we configure all bean classes (ie) collection of bean class 

## @Bean 
- used to configure single bean class 

Example1.java
```java
package com.pack;

public class Example1 {
	private String message1;

	public String getMessage1() {
		return message1;
	}

	public void setMessage1(String message1) {
		this.message1 = message1;
	}
	
}

```

Example2.java
```java
package com.pack;

public class Example2 {
	private String message2;

	public String getMessage2() {
		return message2;
	}

	public void setMessage2(String message2) {
		this.message2 = message2;
	}

}

```

ExampleConfiguration.java
```java
package com.pack;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration     // Configation Annotation for the configuration class
public class ExampleConfiguration {

	@Bean //Bean Annotation for bean classes
	public Example1 example1() {
		return new Example1();
	}

	@Bean
	public Example2 example2() {
		return new Example2();

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
		System.out.println(e1.getMessage1());
		
		Example2 e2 = (Example2)context.getBean(Example2.class);
		e2.setMessage2("Hello SPRING!");
		System.out.println(e2.getMessage2());

	}

}

```


Output:
```cmd
Hello world!
Hello SPRING!
```


## @Scope
- By default it is singleton scope, to define lifetime of a bean.
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
		
	
	}

}

```

Output:
```cmd
com.pack.Example1@479d31f3
com.pack.Example1@479d31f3
com.pack.Example1@479d31f3
```


- Prototype Scope 
ExampleConfiguration.java
```java
package com.pack;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;

@Configuration
public class ExampleConfiguration {

	@Bean
	@Scope("prototype")  //Apply prototype scope
	public Example1 example1() {
		return new Example1();
	}

	@Bean
	public Example2 example2() {
		return new Example2();

	}
}

```

Output:
Different references for the same Main.java
```cmd
com.pack.Example1@4d9e68d0
com.pack.Example1@42e99e4a
com.pack.Example1@14dd9eb7
```

> Always prefer Annotations over BeanFactory xml methods. This is most preferred and the easier one.

