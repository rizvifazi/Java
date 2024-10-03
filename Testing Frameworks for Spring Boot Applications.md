
# Testing Frameworks for Spring Boot Applications

## 1. JUnit 5

- **Key Features:**
	- Standard testing framework for Java applications
	- Annotations for test lifecycle management (@BeforeEach, @AfterAll, etc.)
	- Parameterized tests
	- Conditional test execution
	- Parallel test execution

- **Differentiators:**
	- Widely adopted and well-integrated with Spring Boot
	- Extensible architecture
	- Support for Java 8 lambda expressions

## 2. Mockito

- **Key Features:**
	- Mocking framework for unit tests
	- Stubbing method calls
	- Verifying method invocations
	- Argument matchers

- **Differentiators:**
	- Intuitive API
	- Integration with JUnit
	- Support for both stubbing and verification

## 3. Spring Test

- **Key Features:**
	- Integration testing support for Spring applications
	- MockMvc for testing web controllers
	- TestRestTemplate for testing REST APIs
	- @SpringBootTest for full application context loading

- **Differentiators:**
	- Tightly integrated with Spring Boot
	- Supports testing with sliced application context
	- Provides utilities for working with Spring Security

## 4. TestContainers

- **Key Features:**
	- Provides lightweight, throwaway instances of databases, message brokers, etc.
	- Supports various databases (MySQL, PostgreSQL, MongoDB, etc.)
	- Integration with JUnit 5

- **Differentiators:**
	- Enables testing with real dependencies
	- Supports Docker-based testing environments
	- Improves test reliability and reproducibility

## 5. AssertJ

- **Key Features:**
	- Fluent assertions library
	- Rich set of assertions for various types
	- Custom assertion creation

- **Differentiators:**
	- More readable and expressive assertions compared to JUnit assertions
	- Supports both object and primitive assertions
	- IDE-friendly due to its fluent interface

## 6. Cucumber

- **Key Features:**
	- Behavior-Driven Development (BDD) framework
	- Gherkin syntax for writing test scenarios
	- Step definitions in Java

- **Differentiators:**
	- Bridges communication gap between technical and non-technical team members
	- Supports living documentation
	- Can be used for acceptance testing

## 7. Spock

- **Key Features:**
	- Testing framework for Java and Groovy applications
	- Built-in mocking capabilities
	- Data-driven testing

- **Differentiators:**
	- Groovy-based, allowing for more expressive tests
	- Combines unit testing, mocking, and BDD in one framework
	- Powerful and concise syntax for test cases

## 8. REST Assured

- **Key Features:**
	- Testing framework for RESTful APIs
	- Supports various HTTP methods
	- Response validation

- **Differentiators:**
	- Designed specifically for testing RESTful services
	- Fluent API for request building and response validation
	- Integrates well with existing Java-based test frameworks

## 9. Gatling

- **Key Features:**
	- Load and performance testing tool
	- Scenario recording and scripting
	- Real-time test results

- **Differentiators:**
	- Focuses on performance testing rather than functional testing
	- Provides detailed performance reports
	- Can simulate complex user behaviors

## 10. Wiremock

- **Key Features:**
	- Mock HTTP services
	- Stubbing and verification
	- Fault simulation

- **Differentiators:**
	- Useful for testing microservices and external API dependencies
	- Can be used as a standalone mock server or embedded in JUnit tests
	- Supports various response templating options