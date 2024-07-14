
## Implementing Spring Security in a Spring Boot Application

Spring Security is a powerful and highly customizable authentication and access-control framework for Java applications. In this guide, we will walk through the steps to implement Spring Security in a Spring Boot application.

### Table of Contents

1. [Setup Spring Boot Project](#setup-spring-boot-project)
2. [Add Spring Security Dependency](#add-spring-security-dependency)
3. [Create Security Configuration Class](#create-security-configuration-class)
4. [Define User Roles and Authorities](#define-user-roles-and-authorities)
5. [Configure Authentication Manager](#configure-authentication-manager)
6. [Create Custom Login Page](#create-custom-login-page)
7. [Add Security to REST Endpoints](#add-security-to-rest-endpoints)
8. [Testing the Security Configuration](#testing-the-security-configuration)
9. [Conclusion](#conclusion)

### 1. Setup Spring Boot Project

First, create a new Spring Boot project using Spring Initializr (https://start.spring.io/) or your favorite IDE. Make sure to include the following dependencies:

- Spring Web
- Spring Security
- Thymeleaf (optional, for custom login page)

### 2. Add Spring Security Dependency

If you haven't included the Spring Security dependency, add it to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

### 3. Create Security Configuration Class

Create a configuration class to define your security settings. This class should extend `WebSecurityConfigurerAdapter`.

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/public/**").permitAll()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .loginPage("/login")
                .permitAll()
                .and()
            .logout()
                .permitAll();
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication()
            .withUser("user").password(passwordEncoder().encode("password")).roles("USER")
            .and()
            .withUser("admin").password(passwordEncoder().encode("admin")).roles("ADMIN");
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

### 4. Define User Roles and Authorities

In the above configuration, we have defined two users with different roles: `USER` and `ADMIN`. You can modify these roles as needed for your application.

### 5. Configure Authentication Manager

The `configure(AuthenticationManagerBuilder auth)` method is used to set up in-memory authentication with hard-coded users. In a real-world application, you would likely use a user details service that loads user data from a database.

### 6. Create Custom Login Page

Create a custom login page using Thymeleaf or any other templating engine. Place the `login.html` file in the `src/main/resources/templates` directory.

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Login</title>
</head>
<body>
    <h1>Login</h1>
    <form th:action="@{/login}" method="post">
        <div>
            <label>Username:</label>
            <input type="text" name="username"/>
        </div>
        <div>
            <label>Password:</label>
            <input type="password" name="password"/>
        </div>
        <div>
            <button type="submit">Login</button>
        </div>
    </form>
</body>
</html>
```

### 7. Add Security to REST Endpoints

To secure REST endpoints, you can use the `@PreAuthorize` annotation or configure it in the `HttpSecurity` configuration.

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {

    @GetMapping("/public")
    public String publicEndpoint() {
        return "This is a public endpoint.";
    }

    @GetMapping("/private")
    public String privateEndpoint() {
        return "This is a private endpoint.";
    }
}
```

Update the security configuration to restrict access to the private endpoint:

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .authorizeRequests()
            .antMatchers("/public/**").permitAll()
            .antMatchers("/private/**").hasRole("USER")
            .anyRequest().authenticated()
            .and()
        .formLogin()
            .loginPage("/login")
            .permitAll()
            .and()
        .logout()
            .permitAll();
}
```

### 8. Testing the Security Configuration

Run your Spring Boot application and access the following URLs to test the security configuration:

- `http://localhost:8080/public` (should be accessible without authentication)
- `http://localhost:8080/private` (should require authentication)

Attempt to access the private endpoint without logging in; you should be redirected to the custom login page.

### 9. Conclusion

In this guide, we have covered the basics of implementing Spring Security in a Spring Boot application. We configured security settings, created a custom login page, and secured REST endpoints. This should provide a solid foundation for adding security to your Spring Boot applications.

Feel free to extend this guide by integrating a database for user authentication, adding JWT support, or customizing access rules based on your application's requirements.


---
## Integrating a Database for User Authentication, Adding JWT Support, and Customizing Access Rules in a Spring Boot Application

In this guide, we'll extend our previous Spring Security configuration to include:

1. Integrating a database for user authentication
2. Adding JWT support
3. Customizing access rules

### Table of Contents

1. [Setup Spring Boot Project](#setup-spring-boot-project)
2. [Add Dependencies](#add-dependencies)
3. [Configure the Database](#configure-the-database)
4. [Create JPA Entities and Repositories](#create-jpa-entities-and-repositories)
5. [Implement UserDetailsService](#implement-userdetailsservice)
6. [Configure JWT](#configure-jwt)
7. [Update Security Configuration](#update-security-configuration)
8. [Create REST Controllers for Authentication](#create-rest-controllers-for-authentication)
9. [Testing the Configuration](#testing-the-configuration)
10. [Conclusion](#conclusion)

### 1. Setup Spring Boot Project

Create a new Spring Boot project using Spring Initializr (https://start.spring.io/) or your favorite IDE with the following dependencies:

- Spring Web
- Spring Security
- Spring Data JPA
- Spring Boot Starter Data JPA
- H2 Database (for simplicity, you can use any database)
- jjwt (Java JWT)

### 2. Add Dependencies

Add the following dependencies to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.9.1</version>
</dependency>
```

### 3. Configure the Database

Add the H2 database configuration to your `application.properties` file:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=password
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
```

### 4. Create JPA Entities and Repositories

Create the `User` entity and `UserRepository`:

```java
import javax.persistence.*;
import java.util.Set;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String username;
    private String password;
    @ElementCollection(fetch = FetchType.EAGER)
    private Set<String> roles;

    // Getters and setters
}
```

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
    User findByUsername(String username);
}
```

### 5. Implement UserDetailsService

Create a `CustomUserDetailsService` to load user details from the database:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.security.core.userdetails.User;

import java.util.stream.Collectors;

public class CustomUserDetailsService implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username);
        if (user == null) {
            throw new UsernameNotFoundException("User not found");
        }
        return new org.springframework.security.core.userdetails.User(user.getUsername(), user.getPassword(),
                user.getRoles().stream().map(SimpleGrantedAuthority::new).collect(Collectors.toList()));
    }
}
```

### 6. Configure JWT

Create a utility class for generating and validating JWTs:

```java
import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import org.springframework.stereotype.Component;

import java.util.Date;
import java.util.HashMap;
import java.util.Map;
import java.util.function.Function;

@Component
public class JwtUtil {

    private String SECRET_KEY = "secret";

    public String extractUsername(String token) {
        return extractClaim(token, Claims::getSubject);
    }

    public Date extractExpiration(String token) {
        return extractClaim(token, Claims::getExpiration);
    }

    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver) {
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }

    private Claims extractAllClaims(String token) {
        return Jwts.parser().setSigningKey(SECRET_KEY).parseClaimsJws(token).getBody();
    }

    private Boolean isTokenExpired(String token) {
        return extractExpiration(token).before(new Date());
    }

    public String generateToken(UserDetails userDetails) {
        Map<String, Object> claims = new HashMap<>();
        return createToken(claims, userDetails.getUsername());
    }

    private String createToken(Map<String, Object> claims, String subject) {
        return Jwts.builder().setClaims(claims).setSubject(subject).setIssuedAt(new Date(System.currentTimeMillis()))
                .setExpiration(new Date(System.currentTimeMillis() + 1000 * 60 * 60 * 10))
                .signWith(SignatureAlgorithm.HS256, SECRET_KEY).compact();
    }

    public Boolean validateToken(String token, UserDetails userDetails) {
        final String username = extractUsername(token);
        return (username.equals(userDetails.getUsername()) && !isTokenExpired(token));
    }
}
```

### 7. Update Security Configuration

Update the `SecurityConfig` to include JWT authentication:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private UserDetailsService userDetailsService;

    @Autowired
    private JwtRequestFilter jwtRequestFilter;

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(userDetailsService).passwordEncoder(passwordEncoder());
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    @Override
    public AuthenticationManager authenticationManagerBean() throws Exception {
        return super.authenticationManagerBean();
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable()
            .authorizeRequests().ant

```


---

