
*Date : 06.24.2024*

# Spring boot with Mockito

- spring-boot-starter-test - used to write test cases in Spring boot - comes with Junit5 + Mockito + hamcrest 

```xml
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-test</artifactId>
   <scope>test</scope>
</dependency>
 ```

`@WebMvcTest` - used to write test for `@Controller` or `@RestController`, loads only web layer which includes security, interceptors etc for handling request and response 

`MockMvc` class is a part of Spring MVC framework which helps in testing controller by explicitly starting the server, which will be used along with Spring Boot `@WebMvcTest` to execute JUnit testcase for controller program

`@MockBean` - to add mock object to spring boot application

Builder design pattern - used to build the object using `@Builder` from `lombok` dependency 

```java
import static org.hamcrest.CoreMatchers.is;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.BDDMockito.given;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.post;
import static org.springframework.test.web.servlet.result.MockMvcResultHandlers.print;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
import static org.junit.jupiter.api.Assertions.*;

import java.util.ArrayList;
import java.util.List;

import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.mock.web.MockHttpServletResponse;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.ResultActions;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.pack.SpringBootCRUD.controller.MovieController;
import com.pack.SpringBootCRUD.entity.Movie;
import com.pack.SpringBootCRUD.service.MovieService;


@ExtendWith(MockitoExtension.class)
@WebMvcTest(value=MovieController.class)
public class TestMovieController {

              @Autowired
              MockMvc mockMvc;
              
              @MockBean
              MovieService movieService;
              
              @Autowired
              ObjectMapper mapper;
              
              @Test
              public void testCreateMovie() throws Exception {
                             //Movie movie=new Movie(1000,"Robot","Tamil","action",3);
                             Movie movie=Movie.builder().id(1000).name("Robot").language("Tamil").type("action").rating(3).build();
                             
                        given(movieService.createMovie(any(Movie.class))).willAnswer(inv -> movie);
                             
                             ResultActions response=mockMvc.perform(post("/api/movie")
                                                         .contentType(MediaType.APPLICATION_JSON)
                                                         .content(mapper.writeValueAsString(movie)));
                             
                             response.andDo(print())
                                    .andExpect(status().isCreated())
                                    .andExpect(jsonPath("$.name",is(movie.getName())))
                                    .andExpect(jsonPath("$.language",is(movie.getLanguage())));
                                                          
                             
              }
              
              @Test 
              public void testGetAllMovies() throws Exception {
                             Movie movie1=Movie.builder().id(1000).name("Robot").language("Tamil").type("action").rating(3).build();
                             Movie movie2=Movie.builder().id(1001).name("Friends").language("English").type("comedy").rating(5).build();
                             
                             List<Movie> mlist=new ArrayList<>();
                             mlist.add(movie1);
                             mlist.add(movie2);
                             
                             given(movieService.getAllMovies()).willReturn(mlist);
                             
                             ResultActions response=mockMvc.perform(get("/api/movie"));
                             MockHttpServletResponse res=response.andReturn().getResponse();
                             Movie[] mov=new ObjectMapper().readValue(res.getContentAsString(), Movie[].class);
                             
                             assertEquals(mov[0].getName(),"Robot");
                             assertEquals(mov[1].getName(),"Friends");
              }
              
              @Test
              public void testGetMovieById() throws Exception {
                             Movie movie1=Movie.builder().id(1000).name("Robot").language("Tamil").type("action").rating(3).build();
                             
                            given(movieService.getMovieById(1000)).willReturn(movie1);
                             
                             ResultActions response=mockMvc.perform(get("/api/movie/{movieId}",1000));
                             MockHttpServletResponse res=response.andReturn().getResponse();
                             Movie mov=new ObjectMapper().readValue(res.getContentAsString(), Movie.class);
                             
                             assertEquals("Robot",mov.getName());
                             assertEquals(3,mov.getRating());
              }
}
```


```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.mock.mockito.MockBean;

import com.pack.SpringBootCRUD.entity.Movie;
import com.pack.SpringBootCRUD.entity.MovieRepository;
import com.pack.SpringBootCRUD.service.MovieService;

import static org.mockito.Mockito.when;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

import static org.assertj.core.api.Assertions.*;
import static org.mockito.ArgumentMatchers.anyInt;

@ExtendWith(MockitoExtension.class)
//@SpringBootTest  //load entire appl context 
@DataJpaTest
public class TestMovieService {
              
              @MockBean
              MovieRepository movieRepo;
              
              //@Autowired
              @InjectMocks
              MovieService movieService;
              
              @Test
              public void testCreateMovie() {
                             Movie movie1=Movie.builder().id(1000).name("Robot").language("Tamil").type("action").rating(3).build();
                             when(movieRepo.save(movie1)).thenReturn(movie1);
                             
                       assertThat(movieService.createMovie(movie1)).isEqualTo(movie1);
              }
              
              @Test
              public void testGetAllMovies() {
                             Movie movie1=Movie.builder().id(1000).name("Robot").language("Tamil").type("action").rating(3).build();
                             Movie movie2=Movie.builder().id(1001).name("Friends").language("English").type("comedy").rating(5).build();
                             
                             List<Movie> mlist=new ArrayList<>();
                             mlist.add(movie1);
                             mlist.add(movie2);
                             
                             when(movieRepo.findAll()).thenReturn(mlist);
                             
                            assertThat(movieService.getAllMovies()).isEqualTo(mlist);
              }
              
              @Test
              public void testGetMovieById() {
                             Movie movie1=Movie.builder().id(1000).name("Robot").language("Tamil").type("action").rating(3).build();
                  when(movieRepo.findById(anyInt())).thenReturn(Optional.of(movie1));
                             
                         assertThat(movieService.getMovieById(1000)).isEqualTo(movie1);
              }

}
```

```java
@ExtendWith(MockitoExtension.class)
@SpringBootTest
public class TestMovieRepository {

              @Autowired
              MovieRepository movieRepo;
              
              @Test
              @Disabled
              public void testCreateMovie() {
                             Movie movie1=Movie.builder().id(1000).name("Robot").language("Tamil").type("action").rating(3).build();
                             Movie savedMovie=movieRepo.save(movie1);
                             Movie expectedMovie=movieRepo.findById(savedMovie.getId()).get();
                             assertEquals(savedMovie,expectedMovie);
              }
              
              @Test
              public void testGetAllMovies() {
                             List<Movie> mlist=movieRepo.findAll();
                             List<Movie> list=new ArrayList<>();
                             for(Movie m:mlist)
                                           list.add(m);
                             assertEquals(mlist.size(),list.size());
              }
}
```


---

JUnit and Mockito are both popular tools used in Java testing, but they serve different purposes:

## **JUnit**

- **What it is:** A unit testing framework.
- **What it does:** Provides the foundation for writing and running unit tests. It offers features like:
    - Organizing test cases
    - Running tests
    - Asserting expected behavior

## **Mockito**

- **What it is:** A mocking framework.
- **What it does:** Helps create mock objects for testing. Mock objects simulate the behavior of real objects, allowing you to isolate your code under test from external dependencies. This makes tests faster and more reliable.

Here's a table summarizing the key differences:

|Feature|JUnit|Mockito|
|---|---|---|
|Purpose|Writing and running unit tests|Creating mock objects for testing|
|Scope|Unit-level testing|Isolating dependencies|
|Functionality|Test case organization, execution|Defining mock behavior, verifying interactions|
|Use with JUnit|Not required, but often used together|Can be used independently, but often used with JUnit|

**In essence:**

- JUnit is the **conductor** for your unit testing orchestra.
- Mockito is a specialized **instrument** that helps you play specific notes during the test.

They work well together: JUnit provides the overall testing structure, while Mockito allows you to control dependencies and write more focused tests.

---
Here's a guide to get you started with Mockito:

**1. Setting Up Mockito**

Mockito is a library, so you'll need to add it to your project's dependencies. The dependency configuration depends on your build tool (Maven or Gradle). You can find the specific instructions on the Mockito website ([https://mvnrepository.com/artifact/org.mockito](https://mvnrepository.com/artifact/org.mockito)).

**2. Creating Mock Objects**

Mockito allows you to create mock objects for interfaces and even concrete classes (with limitations). There are two main ways to create mocks:

- **@Mock annotation (JUnit):** This annotation is used with JUnit tests. You declare a field with `@Mock`, and Mockito creates a mock object during test initialization.

Java

```
public class MyTest {

  @Mock
  private MyInterface mockObject;

  // ... rest of your test
}
```

- **Mockito.mock() method:** This static method is a more general way to create mocks. You provide the class you want to mock as an argument.

Java

```
MyInterface mockObject = Mockito.mock(MyInterface.class);
```

**3. Defining Mock Behavior**

Once you have a mock object, you can define its behavior using the `when()` and `thenReturn()` methods.

- **when(object.method(arguments)).thenReturn(returnValue):** This configures the mock object to return a specific value when a particular method is called with certain arguments.

Java

```
when(mockObject.getValue(10)).thenReturn(20);
```

- **Matchers:** You can use matchers instead of exact arguments to make your mocks more flexible. Mockito provides various matchers like `anyInt()`, `eq("value")`, and more.

Java

```
when(mockObject.getValue(anyInt())).thenReturn(42);
```

**4. Verification**

Mockito allows you to verify if your code interacted with the mock object as expected. Use the `verify()` method on the mock object.

- **verify(mockObject).method(arguments):** This verifies that the specific method was called with the given arguments at least once during the test.

Java

```
verify(mockObject).getValue(10);
```

**5. Additional Features**

Mockito offers many other features like:

- **Spies:** Create partial mocks that allow you to mock specific methods while keeping the real behavior for others.
- **Argument Captors:** Capture arguments passed to mock methods for further assertions.
- **Exception Throwing:** Configure mocks to throw specific exceptions.

**Learning Resources:**

- The official Mockito website ([https://site.mockito.org/](https://site.mockito.org/)) has a comprehensive documentation and tutorials.
- Many online resources offer tutorials on using Mockito with JUnit. A quick web search for "Mockito tutorial JUnit" will provide you with detailed examples and explanations.




