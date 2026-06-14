# **Java Interview Questions**

This document serves as a comprehensive guide for Java Spring Boot interview preparation, covering fundamental to advanced topics with structured explanations.

---

# Spring Boot

## Table of Contents

| Sr. No. | Questions                                                                                                                                                |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | [What is JVM, JRE, and JDK?](#1-what-is-jvm-jre-and-jdk)                                                                                                 |
| 2       | [What are the main features of Java?](#2-what-are-the-main-features-of-java)                                                                             |
| 3       | [Why is Java not a pure object-oriented language?](#3-why-is-java-not-a-pure-object-oriented-language)                                                   |
| 4       | [What is a classloader and what are its types?](#4-what-is-a-classloader-and-what-are-its-types)                                                         |
| 5       | [What is the difference between an Instance variable and a Local variable?](#5-what-is-the-difference-between-an-instance-variable-and-a-local-variable) |
| 6       | [What are memory allocations available in Java?](#6-what-are-memory-allocations-available-in-java)                                                       |
| 7       | [Why are Java Strings immutable?](#7-why-are-java-strings-immutable)                                                                                     |

### 1. What is Spring Boot?

Spring Boot is built on top of the Spring framework to create stand-alone RESTful web applications with very minimal configuration and there is no need of external servers to run the application because it has embedded servers like Tomcat.

Spring Boot framework is independent.
It creates executable spring applications that are production-grade.

### 2. What are the Features of Spring Boot?

There are many useful features of Spring Boot:

**Auto-configuration** - Spring Boot automatically configures dependencies by using @EnableAutoconfiguration annotation and reduces boilerplate code.

**Spring Boot Starter POM** - These Starter POMs are pre-configured dependencies for functions like database, security, maven configuration etc.

**Spring Boot CLI (Command Line Interface)** - This command line tool is generally for managing dependencies, creating projects and running the applications.

**Actuator** - Spring Boot Actuator provides health check, metrics and monitors the endpoints of the application. It also simplifies the troubleshooting management.

**Embedded Servers** - Spring Boot contains embedded servers like Tomcat and Jetty for quick application run. No need of external servers.

### 3. What are the advantages of using Spring Boot?

Spring Boot is a framework that creates stand-alone, production grade Spring based applications. So, this framework has so many advantages.

1. **Easy to use:** The majority of the boilerplate code required to create a Spring application is reduced by Spring Boot.
2. **Rapid Development:** auto-configuration enable developers to quickly develop apps without the need for time-consuming setup.
3. **Scalable:** Spring Boot apps are intended to be scalable.
4. **Production-ready:** Metrics, health checks, and externalized configuration

### 4. Define the Key Components of Spring Boot.

The key components of Spring Boot are listed below:

- Spring Boot starters
- Auto-configuration
- Spring Boot Actuator
- Spring Boot CLI
- Embedded Servers

### 5. Why do we prefer Spring Boot over Spring?

Here is a table that summarizes why we use Spring Boot over Spring framework.

| Feature              | Spring                | Spring Boot           |
| :------------------- | :-------------------- | :-------------------- |
| Ease of use          | More complex          | Easier                |
| Production readiness | Less production-ready | More production-ready |
| Scalability          | Less scalable         | More scalable         |
| Speed                | Slower                | Faster                |
| Customization        | Less Customizable     | More Customizable     |

### 6. Explain the internal working of Spring Boot.

**Here are the main steps involved in how Spring Boot works:**

- Start by creating a new Spring Boot project.
- Add the necessary dependencies to your project.
- Annotate the application with the appropriate annotations.
- Run the application.

#### 1. Spring boot internal working:

- Spring Boot applications start with SpringApplication.run().
- The IoC Container manages beans and dependency injection.
- Auto-configuration and component scanning reduce manual configuration.

#### 2. Spring Boot Layered Architecture

Spring Boot follows a layered architecture in which each layer communicates with the other layer directly in a hierarchical structure.

<img src="../images/spring_boot_arc.png" width="400"/>

#### 3. Explanation:

1. Client makes an HTTP request(GET, POST, PUT, DELETE) to the browser.
   Then the request will go to the controller where all the requests will be mapped and handled.
2. After mapping done, in Service layer all the business logic will be performed. It performs the logic on the data that is mapped to JPA(Java Persistence API) using model classes.
3. In repository layer, all the CRUD operations is done for the rest APIs.
   A JSP page is returned to the user if no errors are there.

#### 4. How Spring Boot Application Starts?

Spring Boot applications start with a main class containing the main() method and the @SpringBootApplication annotation.

- JVM executes the main() method.
- SpringApplication.run() is invoked.
- Spring creates the Application Context.
- Component scanning identifies beans and components.
- Auto-configuration configures required dependencies.
- Beans are created and stored inside the IoC Container.
- Embedded server (Tomcat, Jetty, etc.) starts.
- Application becomes ready to handle requests.

#### 5. Basic Annotations to Start a Spring Boot Application

Spring Boot Application is the class which contains @SpringBootApplication annotation along with the main method. The main method should contain SpringApplication.run method.

```java
import org.springframework.boot.SpringApplication

@SprinBootApplication
 public class GFG {
    public static void main (String[] args) {
        SpringApplication.run(GFG.class, args);
         // Data
    }
}
```

> @SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan

#### 6. @Configuration Annotation

- This annotation configures the application context such as transaction, resource handler, view resolver, security etc.
- It is used in class level and it specifically indicates that a class declare one or more than one @Bean methods.

```java
// Annotation
@Configuration
public class GFG {
    @Bean(name = gfg)
      public demoClass demo(){
        // Data
    }
}
```

@EnableAutoConfiguration Annotation:

- This annotation will automatically configures our application we don't need to configure manually.
- It enables the auto-configuration feature of Spring Boot.

```java
// Annotaion
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;

// Annotaion used
@EnableAutoConfiguration
public class GFG {
    public static void main (String[] args) {
        SpringApplication(&quot;GFG.class, args&quot;);
         // Data
    }
}
```

> Here we have used @EnableAutoConfiguration annotation along with the class name to perform the automatic configuration over an application.

#### 7. @ComponentScan Annotation:

- This annotation will automatically scans all the beans and package declaration when the application initializes inside the class path.
- It will automatically scan all the components added to our project.

```java
// @ComponentScan Annotation
@ComponentScan(&quot;com.geeksforgeeks.springboot&quot;)
@SpringBootApplication
public class GFG {
      // Data
}
```

> Automatically discovers components annotated with @Component, @Service, @Repository, or @RestController within its package tree.

### 7. What are the Spring Boot Starter Dependencies?

Spring Boot provides many starter dependencies. Some of them which are used the most in the Spring Boot application are listed below:

- Data JPA starter
- Web starter
- Security starter
- Test Starter
- Thymeleaf starter

### 8. What are the basic Spring Boot Annotations?

#### 1. Common Spring boot annotations:

- **@SpringBootApplication:** This is the main annotation used to bootstrap a Spring Boot application. It combines three annotations: @Configuration , @EnableAutoConfiguration , and @ComponentScan . It is typically placed on the main class of the application.
- **@Configuration:** This annotation is used to indicate that a class contains configuration methods for the application context. It is typically used in combination with @Bean annotations to define beans and their dependencies.
- **@Component:** This annotation is the most generic annotation for any Spring-managed component. It is used to mark a class as a Spring bean that will be managed by the Spring container.
- **@RestController:** This annotation is used to define a RESTful web service controller. It is a specialized version of the @Controller annotation that includes the @ResponseBody annotation by default.
- **@RequestMapping:** This annotation is used to map HTTP requests to a specific method in a controller. It can be applied at the class level to define a base URL for all methods in the class, or at the method level to specify a specific URL mapping.
- **@Bean:** Used to define a Spring bean explicitly inside a configuration class. Gives full control over bean creation and lifecycle.

  ```java
  @Configuration
  public class AppConfig {
  @Bean
  public RestTemplate restTemplate() {
  return new RestTemplate();
  }
  }
  ```

#### 2. Dependency Injection Annotations

@Autowired: Automatically injects required dependencies into a class. Eliminates the need for manual object creation.

```java
@Autowired
private UserService userService;
```

@Qualifier
Specifies which bean to inject when multiple beans of the same type exist.

```java
@Autowired
@Qualifier("emailService")
private NotificationService service;
```

@Primary
Marks a bean as the default choice among multiple candidates. Used when no @Qualifier is explicitly specified.

```java
@Primary
@Component
public class SmsService implements NotificationService {
}
```

#### 3. Web and REST API Annotations

@RestController
Used to create RESTful web services and automatically returns data in JSON or XML format.

```java
@RestController
public class HelloController {
}
```

@RequestMapping
Maps HTTP requests to controller classes or methods. Defines the base URL path for request handling.

```java
@RequestMapping("/api")
public class ApiController {
}
```

#### 4. HTTP Method Annotations

| Annotation     | HTTP Method | Explanation                    |
| :------------- | :---------- | :----------------------------- |
| @GetMapping    | GET         | Retrieves data from the server |
| @PostMapping   | POST        | Sends data to the server       |
| @PutMapping    | PUT         | Updates existing data          |
| @DeleteMapping | DELETE      | Deletes data                   |

**Example:**

```java
@GetMapping("/users")
public List<User> getUsers() {
return userService.getAllUsers();
}
```

@PathVariable
Extracts values from the URI path and binds them to method parameters.

```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable int id) {
return userService.getUser(id);
}
```

@RequestParam
Reads query parameters from the request URL. Used for optional or filtering inputs.

```java
@GetMapping("/search")
public String search(@RequestParam String keyword) {
return keyword;
}
```

@RequestBody
Binds the HTTP request body to a Java object. Commonly used with POST and PUT requests.

```java
@PostMapping("/users")
public User saveUser(@RequestBody User user) {
return userService.save(user);
}
```

#### 5. Configuration and Properties Annotations

@Value
Injects individual property values from application.properties or application.yml.

```java
@Value("${server.port}")
private String port;
```

@ConfigurationProperties
Binds a group of related configuration properties to a POJO in a type-safe manner.

```java
@ConfigurationProperties(prefix = "app")
public class AppConfig {
private String name;
}
```

#### 6. Validation Annotations

Validation annotations ensure input data correctness.

- @NotNull - Field value must not be null
- @NotBlank - String must contain at least one non-whitespace character
- @Email - Validates email format
- @Size - Restricts field length or size.

  ```java
  public class User {
  @NotBlank
  private String username;
  @Email
  private String email;
  }
  ```

#### 7. Exception Handling Annotations

@ExceptionHandler
Handles specific exceptions within a controller. Allows custom error responses for exceptions.

```java
@ExceptionHandler(Exception.class)
public String handleException() {
return "Error occurred";
}
```

@ControllerAdvice
Provides global exception handling across all controllers. Centralizes error-handling logic.

```java
@ControllerAdvice
public class GlobalExceptionHandler {
}
```

#### 8. JPA and Database Annotations

| Annotation      | Purpose                           |
| :-------------- | :-------------------------------- |
| @Entity         | Marks a class as a JPA entity     |
| @Table          | Specifies table mapping           |
| @Id             | Defines primary key               |
| @GeneratedValue | Auto-generates primary key values |
| @Column         | Maps class field to table column  |
