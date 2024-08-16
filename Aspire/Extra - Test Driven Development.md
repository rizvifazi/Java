# Java and Spring Boot Testing Guide

## 1. How to Create Unit Tests with Spring Boot

### Overview
Unit tests are designed to test individual components of a software application in isolation. In a Spring Boot application, you can create unit tests using frameworks like **JUnit 5** and **Mockito**. Spring Boot also provides specialized annotations to facilitate testing.

### Setting Up Dependencies
Ensure that you have the necessary dependencies in your `pom.xml` or `build.gradle` file.

For Maven (`pom.xml`):
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

For Gradle (`build.gradle`):
```groovy
dependencies {
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
    testImplementation 'org.mockito:mockito-core'
}
```

### Writing a Unit Test

Here’s an example of writing a unit test for a simple service class in Spring Boot.

**Service Class:**
```java
@Service
public class CalculatorService {

    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }
}
```

**Unit Test:**
```java
@SpringBootTest
public class CalculatorServiceTest {

    @Autowired
    private CalculatorService calculatorService;

    @Test
    public void testAdd() {
        int result = calculatorService.add(10, 20);
        assertEquals(30, result);
    }

    @Test
    public void testSubtract() {
        int result = calculatorService.subtract(20, 10);
        assertEquals(10, result);
    }
}
```

### Using Mockito to Mock Dependencies

If your service depends on other components (like a repository), you can mock them using Mockito.

**Service Class with Dependency:**
```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public User getUserById(Long id) {
        return userRepository.findById(id).orElse(null);
    }
}
```

**Unit Test with Mockito:**
```java
@RunWith(MockitoJUnitRunner.class)
public class UserServiceTest {

    @InjectMocks
    private UserService userService;

    @Mock
    private UserRepository userRepository;

    @Test
    public void testGetUserById() {
        User mockUser = new User(1L, "John Doe");
        when(userRepository.findById(1L)).thenReturn(Optional.of(mockUser));

        User user = userService.getUserById(1L);

        assertNotNull(user);
        assertEquals("John Doe", user.getName());
    }
}
```

## 2. Difference Between Unit and Integration Tests

### Unit Tests
- **Scope:** Test individual units (methods, classes) in isolation.
- **Dependencies:** Use mocks to simulate dependencies.
- **Execution Time:** Fast, as they don't interact with external systems.
- **Example:** Testing a single service method.

### Integration Tests
- **Scope:** Test how different parts of the application work together (e.g., service, repository, and database).
- **Dependencies:** Often require real or in-memory databases, messaging queues, or external APIs.
- **Execution Time:** Slower, as they involve real systems.
- **Example:** Testing a service method that saves data to a database and retrieves it.

**Integration Test Example:**
```java
@SpringBootTest
@AutoConfigureTestDatabase
public class UserServiceIntegrationTest {

    @Autowired
    private UserService userService;

    @Autowired
    private UserRepository userRepository;

    @Test
    public void testGetUserById() {
        User savedUser = userRepository.save(new User(1L, "John Doe"));

        User user = userService.getUserById(savedUser.getId());

        assertNotNull(user);
        assertEquals("John Doe", user.getName());
    }
}
```

## 3. How to Run and Check the Results of Unit Tests

### Running Unit Tests

**1. Using Your IDE:**
   - Most IDEs like IntelliJ IDEA, Eclipse, or Visual Studio Code allow you to run tests directly from the IDE.
   - Right-click on the test class or method and select "Run".

**2. Using Maven:**
   - You can run tests from the command line using Maven.
   ```sh
   mvn test
   ```

**3. Using Gradle:**
   - Similarly, you can run tests using Gradle.
   ```sh
   ./gradlew test
   ```

### Checking the Results

- **Console Output:** The results of the tests (passed, failed, errors) will be printed to the console.
- **HTML Reports:** Maven and Gradle can generate HTML reports that provide a more detailed summary of the test results.
  - For Maven: Check `target/surefire-reports`.
  - For Gradle: Check `build/reports/tests/test/index.html`.

### Handling Test Failures

- **Assertions:** When an assertion fails, it will show in the test output with details about the expected and actual values.
- **Stack Trace:** If an exception is thrown during the test, the stack trace will be shown to help debug the issue.

## 4. What is Test-Driven Development (TDD)?

### Overview
Test-Driven Development (TDD) is a software development approach where tests are written before the actual code. The process is iterative and involves three main steps:

1. **Red:** Write a test that fails because the functionality doesn’t exist yet.
2. **Green:** Write the minimal code necessary to make the test pass.
3. **Refactor:** Improve the code while ensuring that all tests still pass.

### Example of TDD Workflow

**Step 1: Write a Failing Test (Red)**
```java
@Test
public void testMultiply() {
    int result = calculatorService.multiply(10, 20);
    assertEquals(200, result);
}
```
This test will fail because the `multiply` method doesn’t exist.

**Step 2: Write the Minimal Code (Green)**
```java
@Service
public class CalculatorService {

    public int multiply(int a, int b) {
        return a * b;
    }
}
```
The test should now pass.

**Step 3: Refactor the Code**
Refactor the `CalculatorService` class if necessary, without changing the test outcome.

### Advantages of TDD
- **Improved Code Quality:** By writing tests first, developers are encouraged to think about the design and edge cases.
- **Immediate Feedback:** Tests provide immediate feedback on code changes.
- **Confidence in Refactoring:** With a suite of tests in place, developers can refactor code with confidence, knowing that the tests will catch regressions.
