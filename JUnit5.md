# JUnit 5 Testing Guide for Spring Boot REST API

## Table of Contents
1. [Introduction](#introduction)
2. [Setup](#setup)
3. [Unit Testing](#unit-testing)
4. [Integration Testing](#integration-testing)
5. [Testing REST Controllers](#testing-rest-controllers)
6. [Testing Service Layer](#testing-service-layer)
7. [Testing Repository Layer](#testing-repository-layer)
8. [Best Practices](#best-practices)

## Introduction

This guide demonstrates how to implement JUnit 5 tests for a Spring Boot REST API. We'll cover unit testing, integration testing, and testing different layers of the application.

## Setup

First, ensure you have the necessary dependencies in your `pom.xml` file:

```xml
<dependencies>
    <!-- Spring Boot Starter Web -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    
    <!-- Spring Boot Starter Test -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

The `spring-boot-starter-test` includes JUnit 5, Mockito, and other testing libraries.

## Unit Testing

Let's start with a simple unit test for a service class.

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class UserServiceTest {

    @Test
    void testGetUserById() {
        UserService userService = new UserService();
        User user = userService.getUserById(1L);
        assertNotNull(user);
        assertEquals(1L, user.getId());
    }

    @Test
    void testGetUserByIdNotFound() {
        UserService userService = new UserService();
        assertThrows(UserNotFoundException.class, () -> {
            userService.getUserById(999L);
        });
    }
}
```

In these tests, we're using JUnit 5 annotations and assertions. The `@Test` annotation marks a method as a test method. We're using `assertNotNull`, `assertEquals`, and `assertThrows` to validate the behavior of our `UserService` class.

## Integration Testing

For integration tests, we'll use the `@SpringBootTest` annotation to load the entire application context.

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import static org.junit.jupiter.api.Assertions.*;

@SpringBootTest
class UserIntegrationTest {

    @Autowired
    private UserService userService;

    @Autowired
    private UserRepository userRepository;

    @Test
    void testCreateUser() {
        User user = new User("John Doe", "john@example.com");
        User savedUser = userService.createUser(user);
        assertNotNull(savedUser.getId());
        
        User retrievedUser = userRepository.findById(savedUser.getId()).orElse(null);
        assertNotNull(retrievedUser);
        assertEquals("John Doe", retrievedUser.getName());
    }
}
```

This test creates a user through the service layer and then verifies that it was correctly saved in the database using the repository.

## Testing REST Controllers

To test REST controllers, we'll use `@WebMvcTest` which loads only the web layer of your application.

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;

import static org.mockito.BDDMockito.*;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void testGetUserById() throws Exception {
        User user = new User(1L, "John Doe", "john@example.com");
        given(userService.getUserById(1L)).willReturn(user);

        mockMvc.perform(get("/api/users/1")
                .contentType(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.id").value(1))
                .andExpect(jsonPath("$.name").value("John Doe"))
                .andExpect(jsonPath("$.email").value("john@example.com"));
    }

    @Test
    void testCreateUser() throws Exception {
        User user = new User("Jane Doe", "jane@example.com");
        User savedUser = new User(1L, "Jane Doe", "jane@example.com");
        given(userService.createUser(any(User.class))).willReturn(savedUser);

        mockMvc.perform(post("/api/users")
                .contentType(MediaType.APPLICATION_JSON)
                .content("{\"name\":\"Jane Doe\",\"email\":\"jane@example.com\"}"))
                .andExpect(status().isCreated())
                .andExpect(jsonPath("$.id").value(1))
                .andExpect(jsonPath("$.name").value("Jane Doe"))
                .andExpect(jsonPath("$.email").value("jane@example.com"));
    }
}
```

Here, we're using `MockMvc` to simulate HTTP requests and verify the responses. We're also using `@MockBean` to mock the `UserService` and control its behavior in our tests.

## Testing Service Layer

For the service layer, we typically want to unit test the business logic while mocking any dependencies.

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;

import static org.mockito.BDDMockito.*;
import static org.junit.jupiter.api.Assertions.*;

class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @BeforeEach
    void setUp() {
        MockitoAnnotations.openMocks(this);
    }

    @Test
    void testGetUserById() {
        User user = new User(1L, "John Doe", "john@example.com");
        given(userRepository.findById(1L)).willReturn(Optional.of(user));

        User result = userService.getUserById(1L);
        assertNotNull(result);
        assertEquals("John Doe", result.getName());
    }

    @Test
    void testCreateUser() {
        User user = new User("Jane Doe", "jane@example.com");
        User savedUser = new User(1L, "Jane Doe", "jane@example.com");
        given(userRepository.save(user)).willReturn(savedUser);

        User result = userService.createUser(user);
        assertNotNull(result);
        assertEquals(1L, result.getId());
        assertEquals("Jane Doe", result.getName());
    }
}
```

In these tests, we're using Mockito to mock the `UserRepository` and control its behavior. This allows us to test the `UserService` in isolation.

## Testing Repository Layer

For testing the repository layer, we can use `@DataJpaTest` which sets up an in-memory database and configures Spring Data JPA.

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.boot.test.autoconfigure.orm.jpa.TestEntityManager;

import static org.junit.jupiter.api.Assertions.*;

@DataJpaTest
class UserRepositoryTest {

    @Autowired
    private TestEntityManager entityManager;

    @Autowired
    private UserRepository userRepository;

    @Test
    void testFindByEmail() {
        User user = new User("John Doe", "john@example.com");
        entityManager.persist(user);
        entityManager.flush();

        User found = userRepository.findByEmail("john@example.com");
        assertNotNull(found);
        assertEquals("John Doe", found.getName());
    }
}
```

This test uses `TestEntityManager` to set up test data and then verifies that our custom repository method works correctly.

## Best Practices

1. **Use descriptive test names**: Write test names that describe the scenario being tested.
2. **Follow the AAA pattern**: Arrange, Act, Assert. This helps in organizing your test code.
3. **Test edge cases**: Don't just test the happy path. Include tests for error scenarios and edge cases.
4. **Use test fixtures**: For complex objects or setups, use `@BeforeEach` to set up test fixtures.
5. **Leverage parameterized tests**: Use `@ParameterizedTest` for testing multiple scenarios with different inputs.
6. **Keep tests independent**: Each test should be able to run independently of others.
7. **Use appropriate assertions**: JUnit 5 provides a rich set of assertions. Use the most appropriate one for your scenario.
8. **Mock external dependencies**: Use Mockito to mock external services or dependencies that are not the focus of your test.

By following these practices and examples, you can create a comprehensive test suite for your Spring Boot REST API using JUnit 5.