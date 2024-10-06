# Mockito Testing Guide for Spring Boot REST API

## Table of Contents
1. [Introduction](#introduction)
2. [Setup](#setup)
3. [Mocking Dependencies](#mocking-dependencies)
4. [Testing Controllers](#testing-controllers)
5. [Testing Service Layer](#testing-service-layer)
6. [Testing with MockMvc](#testing-with-mockmvc)
7. [Advanced Mockito Features](#advanced-mockito-features)
8. [Best Practices](#best-practices)

## Introduction

This guide demonstrates how to implement Mockito for testing a Spring Boot REST API. Mockito is a popular mocking framework that allows you to create and configure mock objects. When used with Spring Boot and JUnit, it provides a powerful way to unit test your application.

## Setup

First, ensure you have the necessary dependencies in your `pom.xml` file:

```xml
<dependencies>
    <!-- Spring Boot Starter Web -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    
    <!-- Spring Boot Starter Test (includes Mockito) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

The `spring-boot-starter-test` includes Mockito, so you don't need to add it separately.

## Mocking Dependencies

Let's start with a basic example of how to mock a dependency:

```java
import org.junit.jupiter.api.Test;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import org.junit.jupiter.api.extension.ExtendWith;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)
class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @Test
    void testGetUserById() {
        UserService userService = new UserService(userRepository);
        User mockUser = new User(1L, "John Doe", "john@example.com");
        
        when(userRepository.findById(1L)).thenReturn(Optional.of(mockUser));
        
        User result = userService.getUserById(1L);
        
        assertNotNull(result);
        assertEquals("John Doe", result.getName());
        verify(userRepository).findById(1L);
    }
}
```

In this example:
- We use `@ExtendWith(MockitoExtension.class)` to enable Mockito annotations.
- `@Mock` creates a mock `UserRepository`.
- `when(...).thenReturn(...)` sets up the behavior of the mock.
- `verify(...)` ensures that the mock was called as expected.

## Testing Controllers

When testing controllers, you often need to mock the service layer:

```java
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import org.junit.jupiter.api.extension.ExtendWith;
import org.springframework.http.ResponseEntity;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)
class UserControllerTest {

    @Mock
    private UserService userService;

    @InjectMocks
    private UserController userController;

    @Test
    void testGetUser() {
        User mockUser = new User(1L, "John Doe", "john@example.com");
        when(userService.getUserById(1L)).thenReturn(mockUser);

        ResponseEntity<User> response = userController.getUser(1L);

        assertEquals(200, response.getStatusCodeValue());
        assertEquals("John Doe", response.getBody().getName());
        verify(userService).getUserById(1L);
    }
}
```

Here:
- `@InjectMocks` creates an instance of `UserController` and injects the mocked `UserService`.
- We set up the mock behavior and then call the controller method.
- We assert on the response and verify the service method was called.

## Testing Service Layer

Testing the service layer often involves mocking the repository:

```java
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import org.junit.jupiter.api.extension.ExtendWith;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)
class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    void testCreateUser() {
        User inputUser = new User(null, "Jane Doe", "jane@example.com");
        User savedUser = new User(1L, "Jane Doe", "jane@example.com");
        
        when(userRepository.save(any(User.class))).thenReturn(savedUser);

        User result = userService.createUser(inputUser);

        assertNotNull(result);
        assertEquals(1L, result.getId());
        assertEquals("Jane Doe", result.getName());
        verify(userRepository).save(any(User.class));
    }
}
```

In this example:
- We mock the `save` method of the repository to return a user with an ID.
- We use `any(User.class)` to match any `User` object passed to `save`.
- We verify that the `save` method was called with any `User` object.

## Testing with MockMvc

For testing REST endpoints, you can combine Mockito with MockMvc:

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
    void testGetUser() throws Exception {
        User mockUser = new User(1L, "John Doe", "john@example.com");
        given(userService.getUserById(1L)).willReturn(mockUser);

        mockMvc.perform(get("/api/users/1")
                .contentType(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.id").value(1))
                .andExpect(jsonPath("$.name").value("John Doe"))
                .andExpect(jsonPath("$.email").value("john@example.com"));

        verify(userService).getUserById(1L);
    }
}
```

Here:
- `@WebMvcTest` sets up MockMvc for testing the web layer.
- `@MockBean` creates and injects a mock of `UserService` into the application context.
- We use `given(...).willReturn(...)` to set up the mock behavior.
- MockMvc is used to perform a GET request and assert on the response.

## Advanced Mockito Features

### Argument Captors

Argument captors allow you to capture arguments passed to mocks:

```java
@Test
void testCreateUser() {
    User inputUser = new User(null, "Jane Doe", "jane@example.com");
    
    userService.createUser(inputUser);

    ArgumentCaptor<User> userCaptor = ArgumentCaptor.forClass(User.class);
    verify(userRepository).save(userCaptor.capture());
    
    User capturedUser = userCaptor.getValue();
    assertEquals("Jane Doe", capturedUser.getName());
    assertEquals("jane@example.com", capturedUser.getEmail());
}
```

### Mocking Void Methods

For void methods, you can use `doNothing()` or `doThrow()`:

```java
@Test
void testDeleteUser() {
    doNothing().when(userRepository).deleteById(1L);
    
    userService.deleteUser(1L);
    
    verify(userRepository).deleteById(1L);
}

@Test
void testDeleteUserNotFound() {
    doThrow(new UserNotFoundException("User not found")).when(userRepository).deleteById(999L);
    
    assertThrows(UserNotFoundException.class, () -> userService.deleteUser(999L));
}
```

## Best Practices

1. **Don't mock types you don't own**: Avoid mocking classes from external libraries or frameworks.

2. **Use `@Mock` instead of `mock()`**: It's more readable and less error-prone.

3. **Verify interactions**: Use `verify()` to ensure that mock methods are called as expected.

4. **Don't overuse mocking**: If you find yourself mocking too much, it might indicate a design problem.

5. **Keep tests focused**: Each test should verify a specific behavior.

6. **Use meaningful names**: Name your tests clearly to describe what they're testing.

7. **Be careful with static methods**: Mockito doesn't mock static methods by default. Consider using MockedStatic for this.

8. **Reset mocks in teardown**: If you're reusing mocks across tests, reset them in a `@AfterEach` method.

9. **Use BDDMockito for better readability**: Consider using BDDMockito's `given()` instead of `when()` for a more natural language in your tests.

By following these practices and examples, you can effectively use Mockito to test your Spring Boot REST API, ensuring that your components work correctly in isolation and integration.