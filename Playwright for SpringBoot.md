
# Playwright End-to-End Testing Guide for Spring Boot Web Applications

## Table of Contents
1. [Introduction](#introduction)
2. [Setup](#setup)
3. [Basic Test Structure](#basic-test-structure)
4. [Writing Tests](#writing-tests)
   - [Navigation and Assertions](#navigation-and-assertions)
   - [Form Interactions](#form-interactions)
   - [API Testing](#api-testing)
5. [Page Object Model](#page-object-model)
6. [Handling Authentication](#handling-authentication)
7. [Testing in Different Browsers](#testing-in-different-browsers)
8. [Continuous Integration](#continuous-integration)
9. [Best Practices](#best-practices)

## Introduction

This guide demonstrates how to implement Playwright for end-to-end testing of a Spring Boot web application. Playwright allows you to write tests that interact with your web application just like a user would, providing confidence in your application's functionality from a user's perspective.

## Setup

1. Add Playwright dependency to your `pom.xml`:

```xml
<dependency>
  <groupId>com.microsoft.playwright</groupId>
  <artifactId>playwright</artifactId>
  <version>1.34.0</version>
  <scope>test</scope>
</dependency>
```

2. Install Playwright browsers:

After adding the dependency, run the following command to install the necessary browsers:

```bash
mvn exec:java -e -D exec.mainClass=com.microsoft.playwright.CLI -D exec.args="install"
```

## Basic Test Structure

Create a new test class in your `src/test/java` directory:

```java
import com.microsoft.playwright.*;
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

@TestInstance(TestInstance.Lifecycle.PER_CLASS)
public class PlaywrightE2ETest {

    private Playwright playwright;
    private Browser browser;
    private BrowserContext context;
    private Page page;

    @BeforeAll
    void launchBrowser() {
        playwright = Playwright.create();
        browser = playwright.chromium().launch();
    }

    @BeforeEach
    void createContextAndPage() {
        context = browser.newContext();
        page = context.newPage();
    }

    @AfterEach
    void closeContext() {
        context.close();
    }

    @AfterAll
    void closeBrowser() {
        playwright.close();
    }

    @Test
    void shouldLoadHomePage() {
        page.navigate("http://localhost:8080");
        assertEquals("Home", page.title());
    }
}
```

This structure sets up and tears down the Playwright resources for each test.

## Writing Tests

### Navigation and Assertions

```java
@Test
void shouldNavigateToAboutPage() {
    page.navigate("http://localhost:8080");
    page.click("text=About");
    assertTrue(page.url().contains("/about"));
    assertTrue(page.textContent("h1").contains("About Us"));
}
```

### Form Interactions

```java
@Test
void shouldSubmitContactForm() {
    page.navigate("http://localhost:8080/contact");
    page.fill("#name", "John Doe");
    page.fill("#email", "john@example.com");
    page.fill("#message", "Hello, this is a test message.");
    page.click("button[type=submit]");
    
    // Wait for the success message to appear
    page.waitForSelector("#success-message");
    
    assertTrue(page.isVisible("#success-message"));
    assertEquals("Message sent successfully!", page.textContent("#success-message"));
}
```

### API Testing

You can also use Playwright to test your REST APIs:

```java
@Test
void shouldReturnUserData() {
    Response response = page.navigate("http://localhost:8080/api/users/1");
    assertEquals(200, response.status());
    
    String responseBody = response.text();
    assertTrue(responseBody.contains("\"id\":1"));
    assertTrue(responseBody.contains("\"name\":\"John Doe\""));
}
```

## Page Object Model

For larger applications, consider using the Page Object Model pattern to organize your tests:

```java
public class HomePage {
    private final Page page;

    public HomePage(Page page) {
        this.page = page;
    }

    public void navigate() {
        page.navigate("http://localhost:8080");
    }

    public String getTitle() {
        return page.title();
    }

    public void clickAboutLink() {
        page.click("text=About");
    }
}

public class AboutPage {
    private final Page page;

    public AboutPage(Page page) {
        this.page = page;
    }

    public String getHeadingText() {
        return page.textContent("h1");
    }
}

@Test
void shouldNavigateToAboutPage() {
    HomePage homePage = new HomePage(page);
    AboutPage aboutPage = new AboutPage(page);

    homePage.navigate();
    homePage.clickAboutLink();
    
    assertTrue(page.url().contains("/about"));
    assertTrue(aboutPage.getHeadingText().contains("About Us"));
}
```

## Handling Authentication

If your application requires authentication, you can set it up in the `@BeforeEach` method:

```java
@BeforeEach
void createContextAndPage() {
    context = browser.newContext();
    page = context.newPage();
    
    // Perform login
    page.navigate("http://localhost:8080/login");
    page.fill("#username", "testuser");
    page.fill("#password", "testpassword");
    page.click("button[type=submit]");
    
    // Wait for navigation to complete
    page.waitForNavigation();
}
```

## Testing in Different Browsers

Playwright supports testing in Chromium, Firefox, and WebKit. You can parameterize your tests to run in different browsers:

```java
@ParameterizedTest
@ValueSource(strings = {"chromium", "firefox", "webkit"})
void shouldWorkInAllBrowsers(String browserType) {
    Browser browser = null;
    switch (browserType) {
        case "chromium":
            browser = playwright.chromium().launch();
            break;
        case "firefox":
            browser = playwright.firefox().launch();
            break;
        case "webkit":
            browser = playwright.webkit().launch();
            break;
    }
    
    Page page = browser.newPage();
    page.navigate("http://localhost:8080");
    assertEquals("Home", page.title());
    
    browser.close();
}
```

## Continuous Integration

For CI environments, you'll want to run Playwright in headless mode. You can set this up in your test configuration:

```java
@BeforeAll
void launchBrowser() {
    playwright = Playwright.create();
    browser = playwright.chromium().launch(new BrowserType.LaunchOptions().setHeadless(true));
}
```

You may need to install additional dependencies in your CI environment. For Ubuntu, you can use:

```bash
sudo apt-get update
sudo apt-get install -y libgbm-dev
sudo apt-get install -y libatk-bridge2.0-0
```

## Best Practices

1. **Use explicit waits**: Instead of using `Thread.sleep()`, use Playwright's built-in waiting mechanisms like `waitForSelector()` or `waitForNavigation()`.

2. **Keep tests independent**: Each test should be able to run independently of others. Use `@BeforeEach` to set up the required state for each test.

3. **Use descriptive test names**: Make your test names descriptive of the behavior they're testing.

4. **Handle dynamic content**: If your application has dynamic content, use appropriate selectors and waits to handle it.

5. **Take screenshots on failure**: You can set up a test watcher to take screenshots when tests fail:

```java
@ExtendWith(ScreenshotOnFailureExtension.class)
public class PlaywrightE2ETest {
    // ...
}

public class ScreenshotOnFailureExtension implements TestWatcher {
    @Override
    public void testFailed(ExtensionContext context, Throwable cause) {
        if (context.getTestInstance().isPresent() && context.getTestInstance().get() instanceof PlaywrightE2ETest) {
            PlaywrightE2ETest test = (PlaywrightE2ETest) context.getTestInstance().get();
            test.takeScreenshot("failure-" + context.getTestMethod().get().getName() + ".png");
        }
    }
}
```

6. **Use data-testid attributes**: For more stable selectors, consider adding `data-testid` attributes to your HTML elements and use these in your tests.

7. **Group related tests**: Use JUnit 5's `@Nested` annotation to group related tests together.

8. **Parallelize tests**: Playwright supports running tests in parallel. You can configure this in your test runner settings.

By following these practices and examples, you can create robust end-to-end tests for your Spring Boot web application using Playwright, ensuring that your application works correctly from a user's perspective across different browsers and scenarios.