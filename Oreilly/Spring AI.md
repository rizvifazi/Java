
![[Pasted image 20240909181301.png]]



Reference Link : https://docs.spring.io/spring-ai/reference/index.html
GitHub Link : https://github.com/spring-projects/spring-ai
Azure Workshop : https://github.com/Azure-Samples/spring-ai-azure-workshop
OpenAI Platform : https://platform.openai.com/docs/overview
Ken Kousen : https://github.com/kousen/OpenAIClient
Solutions : https://github.com/kousen/springaiexamples


---

# Introduction to Spring AI

**Spring AI** is an extension to the **Spring Framework** that facilitates the integration of artificial intelligence (AI) capabilities within Spring-based applications. It simplifies the process of interacting with AI services, leveraging the robustness and modularity of the Spring ecosystem. While it is still in its early stages, Spring AI focuses on abstracting away the complexities of using AI/ML models and services like OpenAI, Hugging Face, and others.

Spring AI allows developers to easily embed AI-related operations such as text generation, image analysis, and more, into their enterprise applications. This empowers businesses to integrate AI functionalities into their workflows in a way that is consistent with the well-known Spring programming model.

## Key Features of Spring AI

1. **Seamless Integration**: Spring AI integrates AI services like OpenAI, Hugging Face, and others into Spring applications without requiring extensive code.
   
2. **Declarative and Modular Approach**: With Spring’s modular architecture, Spring AI provides a declarative way to define AI workflows, making it simple to configure and extend.

3. **Reusable Components**: Like the rest of the Spring framework, Spring AI allows you to reuse components and leverage dependency injection to manage AI service connections efficiently.

4. **Cloud-Ready**: Spring AI is built with cloud-native applications in mind, enabling easy integration with cloud services offering AI models.

5. **Extensible**: You can extend Spring AI to work with different AI services, whether it's for natural language processing (NLP), computer vision, or other AI-related use cases.

## How to Get Started with Spring AI

### 1. **Set Up Your Spring Boot Project**
Start by creating a **Spring Boot** project using **Spring Initializr** or your preferred method. You can create the project via:
- [Spring Initializr](https://start.spring.io/)
- Integrated development environments (IDEs) like **IntelliJ IDEA** or **Eclipse**

Make sure to include the following dependencies:
- `Spring Web`
- `Spring AI` (Once available as a dependency)

Here’s an example of a `pom.xml` with the relevant dependencies (assuming Spring AI is available):

```xml
<dependencies>
    <!-- Spring Web for building REST APIs -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Spring AI for integrating AI services -->
    <dependency>
        <groupId>org.springframework.ai</groupId>
        <artifactId>spring-ai-starter</artifactId>
        <version>1.0.0</version>
    </dependency>
</dependencies>
```

### 2. **Configure AI Services**

Depending on which AI service you want to integrate (e.g., OpenAI, Hugging Face, etc.), you need to provide the appropriate API keys and configuration in your application properties. For example, if using OpenAI:

```yaml
spring:
  ai:
    openai:
      api-key: YOUR_API_KEY_HERE
```

This setup allows Spring AI to handle API requests for you without the need for direct integration code.

### 3. **Writing a Simple AI Service**

Let’s say you want to build a simple text-generation service using OpenAI’s GPT model. With Spring AI, you can define this service in a typical Spring style.

```java
import org.springframework.ai.openai.OpenAiClient;
import org.springframework.ai.openai.models.CompletionRequest;
import org.springframework.ai.openai.models.CompletionResponse;
import org.springframework.stereotype.Service;

@Service
public class TextGenerationService {

    private final OpenAiClient openAiClient;

    public TextGenerationService(OpenAiClient openAiClient) {
        this.openAiClient = openAiClient;
    }

    public String generateText(String prompt) {
        CompletionRequest request = CompletionRequest.builder()
                .prompt(prompt)
                .maxTokens(100)
                .build();

        CompletionResponse response = openAiClient.complete(request);
        return response.getChoices().get(0).getText();
    }
}
```

### 4. **Exposing AI Functionality via REST API**

Next, expose the AI functionality through a REST controller, allowing clients to send prompts and get AI-generated responses.

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/ai")
public class AiController {

    private final TextGenerationService textGenerationService;

    public AiController(TextGenerationService textGenerationService) {
        this.textGenerationService = textGenerationService;
    }

    @PostMapping("/generate")
    public String generateText(@RequestParam String prompt) {
        return textGenerationService.generateText(prompt);
    }
}
```

### 5. **Run the Application**

Once your Spring Boot application is set up with the necessary AI services and controllers, you can run it using your IDE or by executing the following command:

```bash
mvn spring-boot:run
```

Then, you can send requests to your API (e.g., via Postman or curl):

```bash
curl -X POST "http://localhost:8080/api/ai/generate?prompt=Hello AI"
```

This will trigger the AI model (OpenAI in this case) to generate text based on the prompt provided.

## Further Steps

### Testing
Spring AI integrates smoothly with Spring's testing framework. You can test your AI services using `MockMvc` or other testing utilities.

### Cloud Deployment
Once your AI-powered Spring application is ready, you can deploy it to the cloud. Spring Boot applications are well-suited for deployment on platforms like:
- **Heroku**
- **AWS (Amazon Web Services)**
- **Google Cloud**
- **Azure**

You can containerize the application using Docker, then deploy it to Kubernetes or other container orchestration platforms.

### Advanced Use Cases
Explore more advanced use cases such as:
- **Fine-tuning models** for specific tasks.
- **Integrating with multiple AI providers**.
- **Streaming AI responses** for real-time applications like chatbots.

## Resources

- [Spring Official Documentation](https://spring.io/projects/spring-framework)
- [OpenAI API Documentation](https://beta.openai.com/docs/)
- [Hugging Face Transformers](https://huggingface.co/docs/transformers/index)

## Conclusion

Spring AI offers a robust and modular way to integrate AI capabilities into your Spring Boot applications. It reduces the complexity of AI integration by providing a declarative and cloud-ready solution. With the power of Spring and modern AI services, you can quickly create AI-powered applications that are scalable, maintainable, and production-ready.
```

This guide provides an overview of **Spring AI**, how to configure it, and how to build AI-based features within a Spring Boot application.