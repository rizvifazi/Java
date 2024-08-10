
### Introduction to Thymeleaf with Spring Boot

Thymeleaf is a modern server-side Java template engine for web and standalone environments. It provides a way to create dynamic web pages with server-side logic embedded in the HTML. When integrated with Spring Boot, Thymeleaf is used to render views by combining the data returned from controllers with the HTML templates.

### Step-by-Step Guide

#### 1. **Setting Up the Project**

1. **Create a Spring Boot project:**
   - You can create a Spring Boot project using [Spring Initializr](https://start.spring.io/), your IDE (e.g., IntelliJ IDEA), or manually via Maven/Gradle.
   - Select **Spring Web** and **Thymeleaf** dependencies.

2. **Maven/Gradle Dependency:**
   - If you're setting up the project manually, add the following dependency to your `pom.xml` (for Maven):

     ```xml
     <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-thymeleaf</artifactId>
     </dependency>
     ```

   - Or for Gradle, add this to `build.gradle`:

     ```groovy
     implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
     ```

#### 2. **Creating Thymeleaf Templates**

Thymeleaf templates are HTML files with embedded Thymeleaf-specific attributes. These templates are typically placed in the `src/main/resources/templates` directory.

1. **Basic Structure of a Thymeleaf Template:**

   ```html
   <!DOCTYPE html>
   <html xmlns:th="http://www.thymeleaf.org">
   <head>
       <title>Thymeleaf with Spring Boot</title>
   </head>
   <body>
       <h1>Welcome to Thymeleaf!</h1>
       <p th:text="${message}">Placeholder for the message</p>
   </body>
   </html>
   ```

   - The `xmlns:th` attribute defines the namespace for Thymeleaf.
   - `th:text` is a Thymeleaf attribute that replaces the content of the element with the value of the `${message}` variable passed from the controller.

#### 3. **Creating a Controller**

In Spring Boot, a controller handles the requests and prepares the data for rendering by the Thymeleaf template.

1. **Example of a simple controller:**

   ```java
   import org.springframework.stereotype.Controller;
   import org.springframework.ui.Model;
   import org.springframework.web.bind.annotation.GetMapping;

   @Controller
   public class GreetingController {

       @GetMapping("/greeting")
       public String greeting(Model model) {
           model.addAttribute("message", "Hello, Thymeleaf!");
           return "greeting";
       }
   }
   ```

   - The `@Controller` annotation indicates that this class is a Spring MVC controller.
   - `@GetMapping("/greeting")` maps HTTP GET requests to the `/greeting` URL.
   - `Model` is used to pass data from the controller to the view.
   - `return "greeting";` indicates that the `greeting.html` template (located in `src/main/resources/templates`) should be rendered.

#### 4. **Running the Application**

1. **Run the Spring Boot application:**
   - You can run the application via your IDE or by executing the `mvn spring-boot:run` or `./gradlew bootRun` command in the terminal.

2. **Access the Thymeleaf page:**
   - Open your browser and navigate to `http://localhost:8080/greeting`.
   - You should see the rendered HTML page with the message "Hello, Thymeleaf!".

#### 5. **Thymeleaf Features**

1. **Text and Attribute Insertion:**
   - Use `th:text` to insert text:
     ```html
     <p th:text="${message}">Default text</p>
     ```

   - Use `th:href` or `th:src` to set the value of attributes:
     ```html
     <a th:href="@{/home}">Home</a>
     ```

2. **Conditionals:**
   - You can conditionally display content using `th:if` and `th:unless`:
     ```html
     <p th:if="${userLoggedIn}">Welcome, User!</p>
     <p th:unless="${userLoggedIn}">Please log in.</p>
     ```

3. **Loops:**
   - To iterate over collections, use `th:each`:
     ```html
     <ul>
         <li th:each="item : ${items}" th:text="${item.name}"></li>
     </ul>
     ```

4. **Fragments:**
   - You can define reusable components in Thymeleaf using fragments:
     ```html
     <!-- In fragment.html -->
     <div th:fragment="header">
         <h1>Site Header</h1>
     </div>

     <!-- In another template -->
     <div th:replace="fragment :: header"></div>
     ```

#### 6. **Internationalization (i18n) Support**

1. **Create Message Properties Files:**
   - Add `messages.properties` (default) and `messages_fr.properties` (for French) in `src/main/resources`.

2. **Using Message Codes in Thymeleaf:**
   - Use the `#{} ` syntax to access messages:
     ```html
     <p th:text="#{welcome.message}"></p>
     ```

3. **Controller to Set Locale:**
   - You can configure Spring Boot to support different locales based on user preferences.

#### 7. **Form Handling**

1. **Creating a Form in Thymeleaf:**
   - Create a form with `th:action` and `th:object` attributes:
     ```html
     <form th:action="@{/submit}" th:object="${formObject}" method="post">
         <input type="text" th:field="*{name}" />
         <button type="submit">Submit</button>
     </form>
     ```

2. **Handling Form Submission:**
   - In the controller, bind the form data to an object and process it:
     ```java
     @PostMapping("/submit")
     public String submitForm(@ModelAttribute("formObject") FormObject formObject) {
         // Process the form data
         return "result";
     }
     ```

### Conclusion

Thymeleaf is a powerful templating engine that integrates seamlessly with Spring Boot, allowing for dynamic and maintainable web applications. This guide covers the basics, but Thymeleaf also offers advanced features such as expression language, security integration, and template inheritance. As you become more familiar with it, you'll find it to be an essential tool in your Spring Boot toolkit.