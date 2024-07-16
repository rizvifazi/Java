
## Implementing Spring Boot Actuator

Spring Boot Actuator provides production-ready features to help you monitor and manage your application. This guide will walk you through the steps to implement Spring Boot Actuator in your application.

### Table of Contents

1. [Setup Spring Boot Project](#setup-spring-boot-project)
2. [Add Spring Boot Actuator Dependency](#add-spring-boot-actuator-dependency)
3. [Configure Actuator Endpoints](#configure-actuator-endpoints)
4. [Accessing Actuator Endpoints](#accessing-actuator-endpoints)
5. [Customizing Actuator Endpoints](#customizing-actuator-endpoints)
6. [Securing Actuator Endpoints](#securing-actuator-endpoints)
7. [Monitoring and Management with Actuator](#monitoring-and-management-with-actuator)
8. [Conclusion](#conclusion)

### 1. Setup Spring Boot Project

Create a new Spring Boot project using Spring Initializr (https://start.spring.io/) or your favorite IDE. Include the following dependencies:

- Spring Web
- Spring Boot Actuator

### 2. Add Spring Boot Actuator Dependency

If you haven't included the Spring Boot Actuator dependency, add it to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

### 3. Configure Actuator Endpoints

By default, Actuator provides a variety of endpoints that can be used to monitor and manage your application. To configure these endpoints, update your `application.properties` or `application.yml` file.

#### application.properties

```properties
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
management.endpoint.info.enabled=true
```

#### application.yml

```yaml
management:
  endpoints:
    web:
      exposure:
        include: "*"
  endpoint:
    health:
      show-details: "always"
    info:
      enabled: true
```

### 4. Accessing Actuator Endpoints

After configuring Actuator, you can access the endpoints via HTTP. The default base path for Actuator endpoints is `/actuator`.

- `/actuator/health`: Provides application health information.
- `/actuator/info`: Provides application information.
- `/actuator/metrics`: Provides various metrics related to the application.
- `/actuator/httptrace`: Provides HTTP request trace information.

### 5. Customizing Actuator Endpoints

You can customize the information returned by some Actuator endpoints. For example, to add custom information to the `/actuator/info` endpoint, create a new `InfoContributor` bean.

```java
import org.springframework.boot.actuate.info.Info;
import org.springframework.boot.actuate.info.InfoContributor;
import org.springframework.stereotype.Component;

import java.util.HashMap;
import java.util.Map;

@Component
public class CustomInfoContributor implements InfoContributor {

    @Override
    public void contribute(Info.Builder builder) {
        Map<String, Object> customInfo = new HashMap<>();
        customInfo.put("app-version", "1.0.0");
        customInfo.put("description", "Spring Boot Actuator Example");
        builder.withDetail("customInfo", customInfo);
    }
}
```

### 6. Securing Actuator Endpoints

You can secure Actuator endpoints by configuring Spring Security. Add the Spring Security dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

Then, create a security configuration class to restrict access to Actuator endpoints.

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;

@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/actuator/**").hasRole("ADMIN")
                .anyRequest().authenticated()
                .and()
            .httpBasic();
    }

    @Bean
    @Override
    protected UserDetailsService userDetailsService() {
        UserDetails user = User.withDefaultPasswordEncoder()
            .username("admin")
            .password("password")
            .roles("ADMIN")
            .build();

        return new InMemoryUserDetailsManager(user);
    }
}
```

### 7. Monitoring and Management with Actuator

Spring Boot Actuator can be integrated with external monitoring systems. Some popular integrations include:

- **Prometheus**: For monitoring metrics.
- **Micrometer**: For collecting application metrics.
- **Spring Boot Admin**: For managing and monitoring Spring Boot applications.

To integrate with Prometheus, add the following dependencies to your `pom.xml` file:

```xml
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-registry-prometheus</artifactId>
</dependency>
```

Then, configure Prometheus in your `application.properties` or `application.yml` file.

#### application.properties

```properties
management.metrics.export.prometheus.enabled=true
```

#### application.yml

```yaml
management:
  metrics:
    export:
      prometheus:
        enabled: true
```

### 8. Conclusion

In this guide, we have covered the basics of implementing Spring Boot Actuator in a Spring Boot application. We configured and accessed Actuator endpoints, customized the information returned by the endpoints, secured the endpoints, and explored monitoring and management options. This should provide a solid foundation for adding Actuator to your Spring Boot applications.