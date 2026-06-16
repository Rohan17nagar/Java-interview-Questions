# **Java Interview Questions**

This document serves as a comprehensive guide for Java Spring Boot interview preparation, covering fundamental to advanced topics with structured explanations.

---

# Spring Boot

## Table of Contents

| Sr. No. | Questions                                                                                                                                                                               |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | [What is Spring Boot?](#1-what-is-spring-boot)                                                                                                                                          |
| 2       | [What are the Features of Spring Boot?](#2-what-are-the-features-of-spring-boot)                                                                                                        |
| 3       | [What are the advantages of using Spring Boot?](#3-what-are-the-advantages-of-using-spring-boot)                                                                                        |
| 4       | [Define the Key Components of Spring Boot](#4-define-the-key-components-of-spring-boot)                                                                                                 |
| 5       | [Why do we prefer Spring Boot over Spring?](#5-why-do-we-prefer-spring-boot-over-spring)                                                                                                |
| 6       | [Explain the internal working of Spring Boot](#6-explain-the-internal-working-of-spring-boot)                                                                                           |
| 7       | [What are the Spring Boot Starter Dependencies?](#7-what-are-the-spring-boot-starter-dependencies)                                                                                      |
| 8       | [What are the basic Spring Boot Annotations?](#8-what-are-the-basic-spring-boot-annotations)                                                                                            |
| 9       | [What is Spring Boot dependency management?](#9-what-is-spring-boot-dependency-management)                                                                                              |
| 10      | [Is it possible to change the port of the embedded Tomcat server in Spring Boot?](#10-is-it-possible-to-change-the-port-of-the-embedded-tomcat-server-in-spring-boot)                   |
| 11      | [What is the starter dependency of the Spring boot module?](#11-what-is-the-starter-dependency-of-the-spring-boot-module)                                                               |
| 12      | [How to disable a specific auto-configuration class?](#12-how-to-disable-a-specific-auto-configuration-class)                                                                           |
| 13      | [Describe the flow of HTTPS requests through the Spring Boot application](#13-describe-the-flow-of-https-requests-through-the-spring-boot-application)                                  |
| 14      | [Explain @RestController annotation in Spring Boot](#14-explain-restcontroller-annotation-in-spring-boot)                                                                               |
| 15      | [What are Profiles in Spring?](#15-what-are-profiles-in-spring)                                                                                                                         |
| 16      | [What is Spring Boot Actuator?](#16-what-is-spring-boot-actuator)                                                                                                                       |
| 17      | [What is dependency Injection and its types?](#17-what-is-dependency-injection-and-its-types)                                                                                           |
| 18      | [What is an IOC container?](#18-what-is-an-ioc-container)                                                                                                                               |
| 19      | [How is Hibernate chosen as the default implementation for JPA without any configuration?](#19-how-is-hibernate-chosen-as-the-default-implementation-for-jpa-without-any-configuration) |

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

### 9. What is Spring Boot dependency management?

Spring Boot dependency management makes it easier to manage dependencies in a Spring Boot project. It makes sure that all necessary dependencies are appropriate for the current Spring Boot version and are compatible with it.

> To create a web application, we can add the S pring Boot starter web dependency to our application.

#### **Life cycle of dependency management:**

<img src="../images/di1.png" width="500px"/>
Spring Boot Dependency Management is a feature that simplifies the process of managing project dependencies and their versions. Instead of manually specifying compatible versions for every library, Spring Boot provides predefined dependency configurations through its starter packages and dependency management mechanism.

- Manages all project dependencies from a central location.
- Automatically handles compatible dependency versions.
- Reduces version conflicts between libraries.

#### **Working of Dependency Management in Spring-Boot**

- Dependency is nothing but a 'Library' that provides specific functionality that we can use in our application.
- In Spring-Boot, Dependency Management and Auto-Configuration work simultaneously.
- It is the auto-configuration that makes managing dependencies supremely easy for us.
- We have to add the dependencies in the pom.xml/build.gradle file.
- These added dependencies will then get downloaded from Maven Central.
- The downloaded dependencies will get stored into the '.m2' folder in the local file system.
- The Spring-Boot application can access these dependencies from '.m2' and its sub-directories.
- Example -( .m2 -> repository -> org, etc )

#### **Project Build Systems**

- Spring Boot supports two main build system Maven and Gradle.
- **Maven:** Dependencies are managed in the pom.xml file.
- **Gradle:** Dependencies are managed in the build.gradle file.
- Maven and Gradle use a different syntax for managing dependencies.
- Also, we don't need to mention the version of the dependencies, as Spring-Boot configures them automatically. Though we can mention the version or override as well.
- The curated list published contains all the Spring Modules and third-party libraries that you can use with Spring-Boot.

#### **Spring-Boot Starters**

Spring Boot Starters are a set of convenient dependency descriptors provided by Spring Boot that simplify the setup of your application by grouping commonly used libraries and configurations into a single, reusable module.

> Example: 'spring-boot-starter-jdbc'

#### **Types of Starters**

1. Application Starters
2. Technical Starters
3. Production-Ready Starters

#### **Adding Dependencies in Spring Boot**

1. Using Maven (pom.xml)
2. Using Gradle - 'spring-boot-gradle-plugin'

## 10. Is it possible to change the port of the embedded Tomcat server in Spring Boot?

The default port of Spring boot Tomcat embedded server is : 8080
Yes, it is possible to change the port of the embedded Tomcat server in a Spring Boot application.

> server.port=8081

## 11. What is the starter dependency of the Spring boot module?

Spring Boot Starters are a collection of pre-configured maven dependencies that makes it easier to develop particular types of applications. These starters include,

- Dependencies
- Version control
- Configuration needed to make certain features.

To use a Spring Boot starter dependency , we simply need to add it to our project's pom.xml file. For example, to add the Spring Boot starter web dependency, add the following dependency to the pom.xml file:

```xml
<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

## 12. How to disable a specific auto-configuration class?

To disable a specific auto-configuration class in a Spring Boot application, we can use the @EnableAutoConfiguration annotation with the " exclude" attribute.

> @EnableAutoConfiguration(exclude = {//classname})

## 13. Describe the flow of HTTPS requests through the Spring Boot application.

The flow of HTTPS requests through a Spring Boot application is as follows:

<img src="../images/api_flow.png" width="500px"/>

- First client makes an HTTP request ( GET, POST, PUT, DELETE ) to the browser.
- After that the request will go to the controller, where all the requests will be mapped and handled.
- After this in Service layer, all the **business logic** will be performed. It performs the business logic on the data that is mapped to **JPA (Java Persistence API)** using model classes.
- In repository layer, all the **CRUD** operations are being done for the REST APIs .
- A JSP page is returned to the end users if no errors are there.

## 14. Explain @RestController annotation in Spring Boot.

**@RestController** annotation is like a shortcut to building RESTful services. It combines two annotations:

**@Controller :** Marks the class as a request handler in the Spring MVC framework.
@ResponseBody : Tells Spring to convert method return values (objects, data) directly into HTTP responses instead of rendering views.
It enables us to Define endpoints for different HTTP methods **(GET, POST, PUT, DELETE)**, return data in various formats (JSON, XML, etc.) and map the request parameters to method arguments.

### Controller vs RestController

| Features                         | @Controller                                                             | @RestController                                                 |
| :------------------------------- | :---------------------------------------------------------------------- | :-------------------------------------------------------------- |
| **Usage**                        | It marks a class as a controller class.                                 | It combines two annotations i.e. @Controller and @ResponseBody. |
| **Application**                  | Used for Web applications.                                              | Used for RESTful APIs.                                          |
| **Request handling and Mapping** | Used with @RequestMapping annotation to map HTTP requests with methods. | Used to handle requests like GET, PUT, POST, and DELETE.        |

> Note: Both annotations handle requests, but @RestController prioritizes data responses for building API.

### RequestMapping vs GetMapping

| Features        | @RequestMapping                                                 | @GetMapping                             |
| :-------------- | :-------------------------------------------------------------- | :-------------------------------------- |
| **Annotations** | @RequestMapping                                                 | @GetMapping                             |
| **Purpose**     | Handles various types of HTTP requests (GET, POST, etc.)        | Specifically handles HTTP GET requests. |
| **Example**     | @RequestMapping(value = "/example", method = RequestMethod.GET) | @GetMapping("/example")                 |

## 15. What are Profiles in Spring?

**Spring Profiles** are like different scenarios for the application depending on the environment.

- You define sets of configurations (like database URLs) for different situations (development, testing, production).
- Use the @Profile annotation to clarify which config belongs to where.
- Activate profiles with environment variables or command-line options.

To use Spring Profiles, we simply need to define the spring.profiles.active property to specify which profile we want to use.

## 16. What is Spring Boot Actuator?

Spring Boot Actuator is a component of the Spring Boot framework that provides production-ready operational monitoring and management capabilities. We can manage and monitor your Spring Boot application while it is running.

> Note: To use Spring Boot Actuator, we simply need to add the spring-boot-starter-actuator dependency to our project.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
</dependencies>
```

#### Configuring Actuator in application.properties

Actuator provides several configuration options to customize its behavior. Below are some common configurations:

- We can also change the default endpoint by adding the following in the application.properties file.
  > management.endpoints.web.base-path=/details
- Including IDs/Endpoints
  By default, all IDs are set to false except for 'health'. To include an ID, use the following property in the application.properties file.

      > Example -> management.endpoint.metrics.enabled=true

- List down all IDs that we want to include which are separated by a comma.
  > management.endpoints.web.exposure.include=metrics,info
- Include only metrics and info IDs and will exclude all others ('health' too).
  > management.endpoints.web.exposure.include=\*
- Excluding IDs/Endpoints

  > Example -> management.endpoints.web.exposure.exclude=info

  #### /actuator endpoint

  It's simple just hit the default endpoint '/actuator', ensure that your Application is running.

  #### /actuator/health

  We can click on these above links and see the respective information. Additionally, we can activate other Actuator IDs and use them after '/actuator' to see more information. For example, 'health' ID is activated by default. Therefore we can click the link in the image or directly use 'http://localhost:8080/actuator/health'.

## 17. What is dependency Injection and its types?

Dependency Injection (DI) is a design pattern that enables us to produce loosely coupled components. In DI, an object's ability to complete a task depends on another object. There three types of dependency Injections.

- Constructor injection: This is the most common type of DI in Spring Boot. In constructor injection, the dependency object is injected into the dependent object's constructor.
- Setter injection: In setter injection, the dependency object is injected into the dependent object's setter method.
- Field injection : In field injection, the dependency object is injected into the dependent object's field.

Spring Dependency Injection (DI) is a fundamental concept in the Spring Framework that allows objects to receive their dependencies from an external source rather than creating them internally.

- Eliminates the need for classes to create their own dependencies
- Makes code more reusable and modular
- Supports constructor, setter, and field injection
- Works with XML configuration, annotations, or Java-based configuration.

<img src="../images/di.png" width="500px"/>

In above Diagram:

- The IoC (Inversion of Control) Container is responsible for creating and managing objects (called Beans).
- Bean 1 and Bean 2 are created by the container instead of being manually instantiated.
- If Bean 1 depends on Bean 2, the container automatically injects Bean 2 into Bean 1 (this is Dependency Injection).
- The configuration for this process is defined using XML or Java Annotations.

#### 1. Setter Dependency Injection:

Setter DI involves injecting dependencies via setter methods. To configure SDI, the @Autowiredannotation is used along with setter methods and the property is set through the `property` tag in the bean configuration file.

```java
package com.geeksforgeeks.org;

import com.geeksforgeeks.org.IGeek;
import org.springframework.beans.factory.annotation.Autowired;

public class GFG {

    // The object of the interface IGeek
    private IGeek geek;

    // Setter method for property geek with @Autowired annotation
    @Autowired
    public void setGeek(IGeek geek) {
        this.geek = geek;
    }
}
```

Bean configuration:

```xml
<beans
xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="
          http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans-2.5.xsd">

    <bean id="GFG" class="com.geeksforgeeks.org.GFG">
        <property name="geek"  ref ="CsvGFG" />
    </bean>

<bean id="CsvGFG" class="com.geeksforgeeks.org.impl.CsvGFG" />
<bean id="JsonGFG" class="com.geeksforgeeks.org.impl.JsonGFG" />

</beans>
```

#### 2. Constructor Dependency Injection (CDI):

Constructor DI involves injecting dependencies through constructors. To configure CDI, the `<constructor-arg>` tag is used in the bean configuration file.

```java
package com.geeksforgeeks.org;

import com.geeksforgeeks.org.IGeek;

public class GFG {

    // The object of the interface IGeek
    private IGeek geek;

    // Constructor to set the CDI
    public GFG(IGeek geek) {
        this.geek = geek;
    }
}
```

| Setter DI                                                                    | Constructor DI                                                                   |
| :--------------------------------------------------------------------------- | :------------------------------------------------------------------------------- |
| Creates mutable objects. Dependencies can be modified after creation.        | Creates immutable objects. Dependencies can't be modified after creation.        |
| Dependencies can be injected later.                                          | All dependencies must be provided at creation.                                   |
| Requires addition of @Autowired annotation.                                  | @Autowired annotation is not needed.                                             |
| It results in circular dependencies or partial dependencies.                 | It too can have circular dependencies, it just fails faster and more explicitly. |
| Requires framework or manual setter calls for dependency injection in tests. | Easier unit testing - can create objects directly with mock dependencies.        |

## 18. What is an IOC container?

An IoC (Inversion of Control) Container in Spring Boot is essentially a central manager for the application objects that controls the creation, configuration, and management of dependency injection of objects (often referred to as beans), also referred to as a DI (Dependency Injection) container.

The Spring Inversion of Control (IoC) container is a core component of the Spring Framework, streamlining object creation and management. It promotes flexibility and maintainability by managing dependencies and configurations automatically, allowing developers to concentrate on core business logic.

- Configuration Metadata: Defines how beans should be created, configured, and wired.
- Bean Instantiation: The container creates instances of beans as per the configuration.
- Dependency Injection: Automatically resolves and injects the necessary dependencies into beans.
- Lifecycle Management: Manages bean initialization, destruction, and scope (singleton, prototype, etc.).

The following diagram illustrates how the IoC container manages the creation of beans and injects their dependencies in a Spring application.

<img src="../images/ioc1.png" width="500px"/>

#### **Types of Spring Containers**

#### 1. BeanFactory Container

    The BeanFactory is the simplest and most lightweight container in Spring. It provides basic features for bean creation and management but lacks advanced functionalities such as event handling and AOP.

    - Suitable for simple applications with minimal configuration.
    - Beans are created lazily, meaning they are instantiated only when requested.
    - Typically used for low-memory or resource-constrained environments.

```java
import org.springframework.beans.factory.BeanFactory;
import org.springframework.beans.factory.xml.XmlBeanFactory;
import org.springframework.core.io.ClassPathResource;

public class BeanFactoryExample {
    public static void main(String[] args) {
        // Load the Spring context (XML configuration)
        BeanFactory factory = new XmlBeanFactory(new ClassPathResource("beans.xml"));

        // Access the bean from the factory
        MyBean myBean = (MyBean) factory.getBean("myBean");

        // Use the bean
        myBean.doSomething();
    }
}
```

> BeanFactory Container does not support annotation-based configuration

#### 2. ApplicationContext Container

The ApplicationContext is a more advanced and feature-rich container compared to BeanFactory. It extends BeanFactory and adds additional features such as event propagation, AOP support, and internationalization.

More commonly used in production applications.
In the ApplicationContext container, by default, beans are created eagerly during the container initialization process.
It provides additional services like message resources, event handling, and more.

**Syntax for ApplicationContext Ioc Container**

1. Using XML Configuration

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class ApplicationContextExample {
    public static void main(String[] args) {
        // Load the Spring context (XML configuration)
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");

        // Access the bean from the application context
        MyBean myBean = (MyBean) context.getBean("myBean");

        // Use the bean
        myBean.doSomething();
    }
}
```

2. Using AnnotationBasedConfiguration

```java
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class AnnotationContextExample {
    public static void main(String[] args) {
        // Load the Spring context using annotations
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

        // Access the bean from the application context
        MyBean myBean = context.getBean(MyBean.class);

        // Use the bean
        myBean.doSomething();
    }
}
```

## 15. How is Hibernate chosen as the default implementation for JPA without any configuration?

Spring Boot automatically configures Hibernate as the default JPA implementation when we add the spring-boot-starter-data-jpa dependency to our project. This dependency includes the Hibernate JAR file as well as the Spring Boot auto-configuration for JPA.

# Spring Boot Interview Guide — 30 Questions Answered

> **Format:** Definition → Real-World Analogy → Code Example (where applicable)

---

## 1. How does Spring Boot decide which auto-configuration to apply?

**Definition:**  
Spring Boot uses `@EnableAutoConfiguration` (bundled inside `@SpringBootApplication`) to scan the classpath. It reads entries from `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` (Spring Boot 3.x) or `META-INF/spring.factories` (Spring Boot 2.x) and conditionally applies configurations using `@Conditional*` annotations like `@ConditionalOnClass`, `@ConditionalOnMissingBean`, etc.

**Analogy:**  
Think of it like a hotel check-in. The hotel (Spring Boot) automatically prepares your room based on what you booked (dependencies on classpath). If you booked a suite (added `spring-boot-starter-data-jpa`), they set up a Jacuzzi (DataSource, EntityManager). You don't have to ask for each item individually.

**Code Example:**
```java
// Spring Boot checks: is HikariCP on the classpath? Is there no DataSource bean already?
// If yes → auto-configures one. You don't write this — Spring Boot does it internally.

@ConditionalOnClass(DataSource.class)
@ConditionalOnMissingBean(DataSource.class)
public class DataSourceAutoConfiguration {
    // Sets up a DataSource automatically
}
```

---

## 2. What happens internally when you add `spring-boot-starter-web`?

**Definition:**  
`spring-boot-starter-web` is a dependency aggregator (a POM with no code). It pulls in: Spring MVC, Jackson (JSON), Tomcat (embedded), and Spring Boot auto-configuration. Spring Boot then detects these classes and auto-configures `DispatcherServlet`, `TomcatEmbeddedWebServerFactory`, `HttpMessageConverters`, etc.

**Analogy:**  
It's like ordering a "Full English Breakfast" at a café. You say one thing, but you get eggs, toast, bacon, beans, and tea — all bundled. You didn't order each item separately.

**What gets set up automatically:**
```
spring-boot-starter-web
  ├── spring-webmvc         → DispatcherServlet, @Controller support
  ├── spring-boot-starter-tomcat → Embedded Tomcat server
  ├── jackson-databind      → JSON serialization/deserialization
  └── spring-boot-autoconfigure → Wires everything together
```

---

## 3. Why does Spring Boot prefer convention over configuration?

**Definition:**  
Convention over configuration means Spring Boot provides sensible defaults so developers don't have to write repetitive boilerplate. You only configure what differs from the default. This is enforced through auto-configuration, starter POMs, and opinionated defaults (e.g., port 8080, H2 for in-memory DB).

**Analogy:**  
It's like a pre-furnished apartment. You can move in immediately and use the existing furniture. If you don't like the couch, you replace just that — you don't furnish the entire apartment from scratch.

**Example:**
```yaml
# Without Spring Boot: write 50+ lines of XML for DispatcherServlet, DataSource, etc.
# With Spring Boot — just this in application.yml is enough:
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: secret
```

---

## 4. How does Spring Boot load `application.properties` internally?

**Definition:**  
Spring Boot uses `ConfigDataEnvironmentPostProcessor` during the `Environment` preparation phase of startup. It searches for config files in this order:
1. Classpath root (`src/main/resources/`)
2. Classpath `/config/`
3. Current directory
4. Current directory `/config/`

Properties are loaded into the Spring `Environment` and bound to beans using `@Value` or `@ConfigurationProperties`.

**Analogy:**  
Like a chef reading a recipe card. The card (application.properties) is read at startup before cooking begins. The chef doesn't look at it during cooking — everything is already set up.

**Code Example:**
```java
@Component
@ConfigurationProperties(prefix = "app")
public class AppConfig {
    private String name;
    private int timeout;
    // getters and setters
}
```
```properties
# application.properties
app.name=MyService
app.timeout=5000
```

---

## 5. What is the exact startup flow of a Spring Boot application?

**Definition:**  
The startup flow involves these ordered steps:

```
1. main() called → SpringApplication.run()
2. SpringApplication created → determines application type (SERVLET / REACTIVE / NONE)
3. Loads SpringApplicationRunListeners (from spring.factories)
4. Prepares Environment (loads application.properties, env vars, CLI args)
5. Prints Banner
6. Creates ApplicationContext (AnnotationConfigServletWebServerApplicationContext for web)
7. Prepares ApplicationContext (sets environment, registers BeanDefinitions)
8. Refreshes ApplicationContext → triggers bean creation, auto-configuration
9. Starts Embedded Web Server (Tomcat)
10. Calls ApplicationRunners / CommandLineRunners
11. Application is READY → publishes ApplicationReadyEvent
```

**Analogy:**  
Like launching a rocket. Pre-checks → fuel loading → ignition → lift-off → orbit. Each step must succeed for the next to begin.

---

## 6. Difference between `@ComponentScan` and `@SpringBootApplication`?

**Definition:**

| Annotation | Purpose |
|---|---|
| `@ComponentScan` | Scans specified packages for `@Component`, `@Service`, `@Repository`, `@Controller` |
| `@SpringBootApplication` | Meta-annotation combining `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan` |

`@SpringBootApplication` scans from the package of the class it's placed on, downward.

**Code Example:**
```java
// @SpringBootApplication = all three below combined
@Configuration
@EnableAutoConfiguration
@ComponentScan(basePackages = "com.example")
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

**Tip:** Always place `@SpringBootApplication` in the root package so component scanning covers all sub-packages.

---

## 7. How does Spring Boot detect embedded Tomcat and configure it?

**Definition:**  
`EmbeddedWebServerFactoryCustomizerAutoConfiguration` detects Tomcat on the classpath via `@ConditionalOnClass(Tomcat.class)`. It then creates a `TomcatServletWebServerFactory` bean, registers the `DispatcherServlet`, and starts Tomcat programmatically — no `web.xml` needed.

**Analogy:**  
Like a self-assembling IKEA shelf. The parts (Tomcat JARs) are in the box (classpath), and the instructions (auto-configuration) build it automatically. You don't need to hammer anything.

**Customization Example:**
```java
@Bean
public WebServerFactoryCustomizer<TomcatServletWebServerFactory> tomcatCustomizer() {
    return factory -> {
        factory.setPort(9090);
        factory.addConnectorCustomizers(connector ->
            connector.setMaxPostSize(10 * 1024 * 1024)); // 10MB
    };
}
```

---

## 8. What happens if two beans of same type exist and no `@Qualifier`?

**Definition:**  
Spring throws a `NoUniqueBeanDefinitionException` at startup. It cannot decide which bean to inject when there are multiple candidates and no disambiguation provided.

**Analogy:**  
You ask a waiter "bring me the wine" but there are 20 different wines available. The waiter doesn't know which one and stands confused. You need to specify: "bring me the Merlot" (`@Qualifier("merlot")`).

**Fix Example:**
```java
@Component("fastEngine")
public class FastEngine implements Engine { }

@Component("slowEngine")
public class SlowEngine implements Engine { }

@Service
public class Car {
    @Autowired
    @Qualifier("fastEngine")  // Must specify!
    private Engine engine;
}

// OR use @Primary to set a default:
@Component
@Primary
public class FastEngine implements Engine { }
```

---

## 9. How does Spring Boot handle profile-specific configuration?

**Definition:**  
Spring Boot loads `application-{profile}.properties` or `application-{profile}.yml` in addition to the base `application.properties`. The active profile is set via `spring.profiles.active`. Profile-specific properties override the base ones.

**Analogy:**  
Like a restaurant with a lunch menu and a dinner menu. The base menu (application.properties) has common items. The dinner menu (application-prod.properties) overrides prices and adds specials.

**Code Example:**
```properties
# application.properties (base)
app.name=MyApp
server.port=8080

# application-dev.properties
spring.datasource.url=jdbc:h2:mem:testdb

# application-prod.properties
spring.datasource.url=jdbc:mysql://prod-server/mydb
```
```bash
# Activate profile
java -jar app.jar --spring.profiles.active=prod
```
```java
@Profile("dev")
@Bean
public DataSource devDataSource() { ... }
```

---

## 10. What is the role of `SpringFactoriesLoader`?

**Definition:**  
`SpringFactoriesLoader` reads key-value pairs from `META-INF/spring.factories` files on the classpath. Spring Boot uses it to discover auto-configuration classes, application listeners, initializers, and run listeners — all without explicit registration.

**Analogy:**  
Like a franchise directory. Any new franchise (library/starter) registers itself in the central directory (`spring.factories`). The parent company (Spring Boot) reads the directory and knows all available services automatically.

**Example spring.factories entry:**
```properties
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
  com.example.MyAutoConfiguration,\
  com.example.AnotherAutoConfiguration
```

---

## 11. How does Spring Boot reduce XML configuration completely?

**Definition:**  
Spring Boot eliminates XML by using:
- **Java-based configuration** (`@Configuration`, `@Bean`)
- **Auto-configuration** (reads classpath, applies defaults)
- **Component scanning** (`@ComponentScan`)
- **Annotation-driven** dependency injection (`@Autowired`, `@Value`)

**Analogy:**  
Old Spring = assembling furniture with a 100-page manual. Spring Boot = furniture that assembles itself. You only read the manual if you want to customize.

**Old XML vs Spring Boot:**
```xml
<!-- OLD Spring XML -->
<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
    <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
    <property name="url" value="jdbc:mysql://localhost/test"/>
</bean>
```
```java
// Spring Boot — just add properties file entry, no code needed!
// application.properties:
// spring.datasource.url=jdbc:mysql://localhost/test
```

---

## 12. Difference between `@RestController` and `@Controller` internally?

**Definition:**

| Annotation | Behavior |
|---|---|
| `@Controller` | Returns view names (resolves to HTML templates via ViewResolver) |
| `@RestController` | = `@Controller` + `@ResponseBody`. Writes return value directly to HTTP response body (as JSON/XML) |

**Analogy:**  
`@Controller` is a restaurant waiter who takes your order to the kitchen and brings back a plate (HTML view). `@RestController` is a vending machine — you press a button and data comes out directly (JSON).

**Code Example:**
```java
@Controller
public class WebController {
    @GetMapping("/home")
    public String home(Model model) {
        model.addAttribute("name", "World");
        return "home"; // resolves to home.html (Thymeleaf/FreeMarker)
    }
}

@RestController
public class ApiController {
    @GetMapping("/api/users")
    public List<User> getUsers() {
        return userService.findAll(); // written as JSON directly to response
    }
}
```

---

## 13. How does Spring Boot manage dependency versions automatically?

**Definition:**  
`spring-boot-starter-parent` inherits from `spring-boot-dependencies` BOM (Bill of Materials). The BOM declares tested, compatible versions for hundreds of libraries. When you add a dependency without a version, Maven/Gradle picks it up from the BOM.

**Analogy:**  
Like a pre-approved vendor list in a company. HR (Spring Boot BOM) maintains a list of approved suppliers (libraries) with negotiated prices (versions). You just pick what you need — no price negotiation required.

**pom.xml Example:**
```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.2.0</version>
</parent>

<dependencies>
    <!-- No version needed! BOM handles it -->
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
    </dependency>
</dependencies>
```

---

## 14. What is the lifecycle of a Spring Bean in Spring Boot?

**Definition:**  
Spring Bean lifecycle:

```
1. Instantiation       → Bean object created (constructor called)
2. Dependency Injection → @Autowired fields/setters populated
3. Bean Name Aware     → setBeanName() called (if BeanNameAware)
4. Post Processing     → BeanPostProcessor.postProcessBeforeInitialization()
5. @PostConstruct      → Init method called
6. afterPropertiesSet()→ InitializingBean (if implemented)
7. Custom init-method  → @Bean(initMethod="...")
8. Bean is READY       → BeanPostProcessor.postProcessAfterInitialization()
--- Bean in use ---
9. @PreDestroy         → Called before destruction
10. destroy()          → DisposableBean (if implemented)
11. Custom destroy-method
```

**Code Example:**
```java
@Component
public class MyService {

    @PostConstruct
    public void init() {
        System.out.println("Bean initialized — DB connections, caches set up");
    }

    @PreDestroy
    public void cleanup() {
        System.out.println("Bean destroyed — releasing resources");
    }
}
```

---

## 15. How does Spring Boot handle externalized configuration?

**Definition:**  
Spring Boot supports 17+ property sources with a defined priority order (higher overrides lower):

```
1. Command-line arguments        (--server.port=9090)
2. SPRING_APPLICATION_JSON env var
3. OS environment variables      (SERVER_PORT=9090)
4. application-{profile}.properties
5. application.properties
6. @PropertySource annotations
7. Default properties
```

**Analogy:**  
Like a restaurant's pricing policy. Head office (default properties) sets base prices. Regional manager (profile properties) can override. Local manager (env var) can override that. Customer negotiation (CLI args) wins everything.

**Code Example:**
```java
@Component
public class ServerConfig {
    @Value("${server.port:8080}")  // 8080 is the default fallback
    private int port;
}
```
```bash
# Override at runtime — no code change needed
export SERVER_PORT=9090
java -jar app.jar --server.port=8888   # This wins
```

---

## 16. What happens if `application.yml` and `application.properties` both exist?

**Definition:**  
Both files are loaded. `application.properties` takes **higher priority** than `application.yml` when both exist for the same key. However, it's best practice to use only one format to avoid confusion.

**Analogy:**  
Two people give you directions to the same destination. The one who speaks last (properties file) wins. But having two sources of truth is confusing — just pick one navigator.

**Precedence:**
```
application.properties > application.yml
```

**Best Practice:**  
Stick to one format per project. Use `.yml` for nested configs, `.properties` for simplicity.

---

## 17. How does Spring Boot integrate with Actuator internally?

**Definition:**  
`spring-boot-actuator` auto-configures management endpoints (`/actuator/health`, `/actuator/metrics`, etc.) via `ActuatorAutoConfiguration`. It registers `Endpoint` beans for health, metrics, info, etc. These are exposed over HTTP (or JMX) via `WebMvcEndpointHandlerMapping`.

**Analogy:**  
Like a car dashboard. The engine (your app) runs the car. The dashboard (Actuator) shows you speed, fuel, temperature in real time — without interfering with the engine.

**Setup:**
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
```yaml
management:
  endpoints:
    web:
      exposure:
        include: health, metrics, info, env
```
```bash
curl http://localhost:8080/actuator/health
# {"status":"UP"}
```

---

## 18. Difference between `@Configuration` and a normal class?

**Definition:**

| Aspect | Normal Class | `@Configuration` Class |
|---|---|---|
| Spring awareness | Not managed by Spring | Fully managed by Spring |
| `@Bean` methods | Not intercepted | Proxied via CGLIB — calls are intercepted |
| Singleton guarantee | No | Yes — `@Bean` methods return same instance |

**The Key Difference:** `@Configuration` classes are CGLIB-proxied. When one `@Bean` method calls another inside the same class, Spring intercepts the call and returns the existing singleton instead of creating a new object.

**Code Example:**
```java
@Configuration
public class AppConfig {
    @Bean
    public ServiceA serviceA() {
        return new ServiceA(serviceB()); // serviceB() intercepted — returns singleton
    }

    @Bean
    public ServiceB serviceB() {
        return new ServiceB();
    }
}

// Without @Configuration (just @Component):
// serviceB() would be called as a regular Java method → new object each time → NOT singleton!
```

---

## 19. How does Spring Boot create `DataSource` automatically?

**Definition:**  
`DataSourceAutoConfiguration` triggers when `DataSource.class` and a JDBC driver are on the classpath and no `DataSource` bean exists. It reads `spring.datasource.*` properties and creates a `HikariDataSource` (default connection pool) automatically.

**Analogy:**  
Like a smart coffee machine. You fill water and beans (add driver + properties). The machine (Spring Boot) brews the coffee (DataSource) without any manual steps.

**Example:**
```properties
# application.properties — this is ALL you need
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=secret
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```
```java
// Spring Boot creates this automatically:
// HikariDataSource with connection pool size 10 (default)

// You can inject it directly:
@Autowired
private DataSource dataSource;
```

---

## 20. What is the real use of `CommandLineRunner`?

**Definition:**  
`CommandLineRunner` is a functional interface with `run(String... args)` called after the Spring context is fully initialized but before the app starts serving traffic. Used for: data seeding, cache warming, startup validations, migration scripts.

**Analogy:**  
Like a restaurant's morning prep before opening. The kitchen (Spring context) is set up. Before customers arrive (before serving requests), the chef (CommandLineRunner) preps ingredients, warms the grill, and checks inventory.

**Code Example:**
```java
@Component
public class DataSeeder implements CommandLineRunner {

    @Autowired
    private UserRepository userRepository;

    @Override
    public void run(String... args) throws Exception {
        if (userRepository.count() == 0) {
            userRepository.save(new User("admin", "admin@example.com"));
            System.out.println("✅ Admin user seeded!");
        }
    }
}
```

---

## 21. How does Spring Boot handle exception translation?

**Definition:**  
Spring Boot provides multiple layers of exception handling:
1. `@ExceptionHandler` — method-level, handles exceptions in a single controller
2. `@ControllerAdvice` / `@RestControllerAdvice` — global exception handler across all controllers
3. `BasicErrorController` — default `/error` endpoint for unhandled exceptions
4. `PersistenceExceptionTranslationPostProcessor` — translates JPA/JDBC exceptions to Spring's `DataAccessException` hierarchy

**Analogy:**  
Like airport security levels. First check: gate agent (`@ExceptionHandler`). Second check: terminal security (`@ControllerAdvice`). Final check: airport-wide (BasicErrorController).

**Code Example:**
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND)
            .body(new ErrorResponse("NOT_FOUND", ex.getMessage()));
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneral(Exception ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
            .body(new ErrorResponse("INTERNAL_ERROR", "Something went wrong"));
    }
}
```

---

## 22. Difference between `@EnableAutoConfiguration` and `@Import`?

**Definition:**

| Annotation | Purpose |
|---|---|
| `@EnableAutoConfiguration` | Scans `spring.factories`/`AutoConfiguration.imports` and conditionally applies hundreds of auto-configurations |
| `@Import` | Explicitly imports one or more specific `@Configuration` classes into the Spring context |

`@EnableAutoConfiguration` is broad and conditional. `@Import` is explicit and always applied.

**Code Example:**
```java
// @Import — explicit, always loaded
@Configuration
@Import({SecurityConfig.class, DataSourceConfig.class})
public class AppConfig { }

// @EnableAutoConfiguration — conditional, reads from spring.factories
// Only loads DataSourceAutoConfiguration IF DataSource is on classpath AND no bean exists
@SpringBootApplication  // includes @EnableAutoConfiguration
public class App { }
```

---

## 23. What happens if you exclude an auto-configuration class?

**Definition:**  
When you exclude an auto-configuration class, Spring Boot's `AutoConfigurationImportSelector` removes it from the list before creating beans. No beans from that configuration are created. Useful when you want to provide your own implementation.

**Analogy:**  
Like telling the hotel "I don't need housekeeping today." The service (auto-config) is available but you've opted out for this stay.

**Code Example:**
```java
// Exclude DataSource auto-configuration (e.g., for testing with no DB)
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}

// OR in application.properties:
// spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```

---

## 24. How does Spring Boot support microservices so easily?

**Definition:**  
Spring Boot makes microservices easy through:
- **Embedded server** — each service runs independently, no shared app server
- **Actuator** — built-in health checks for service discovery (Eureka, Kubernetes)
- **Spring Cloud** — complements with circuit breakers (Resilience4j), config server, API gateway
- **Auto-configuration** — minimal setup for REST, messaging, security
- **Fat JAR** — self-contained deployable unit (deploy anywhere: Docker, K8s, VMs)
- **Profiles** — easy environment-specific config (dev/staging/prod)

**Analogy:**  
Like food trucks vs a restaurant chain. Each food truck (microservice) is self-contained, mobile, independently deployable. Spring Boot gives each truck its own kitchen (embedded Tomcat) and menu (configuration).

---

## 25. What is the difference between a Fat JAR and a Normal JAR?

**Definition:**

| | Normal JAR | Fat JAR (Uber JAR) |
|---|---|---|
| Contents | Only compiled classes | Classes + ALL dependencies + embedded server |
| Dependencies | Must be on classpath separately | Bundled inside |
| Deployment | Needs app server / classpath setup | `java -jar app.jar` — runs anywhere |
| Size | Small (KB to few MB) | Large (10-100+ MB) |

**Analogy:**  
Normal JAR = a recipe card (needs ingredients separately). Fat JAR = a meal kit delivery (everything included, just cook and serve).

**Build:**
```xml
<!-- pom.xml — spring-boot-maven-plugin creates the fat jar -->
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
```
```bash
mvn package
java -jar target/myapp-1.0.0.jar   # completely self-contained!
```

---

## 26. How does Spring Boot handle logging by default?

**Definition:**  
Spring Boot uses **SLF4J** as the logging facade and **Logback** as the default implementation (via `spring-boot-starter-logging`). Default log level is `INFO`. Logs go to console by default. Configure via `application.properties`.

**Analogy:**  
SLF4J is like a universal TV remote (works with any TV). Logback is the default TV brand. You can swap to Log4j2 (another TV brand) without changing your remote (SLF4J code).

**Configuration:**
```properties
# application.properties
logging.level.root=INFO
logging.level.com.example=DEBUG
logging.file.name=logs/app.log
logging.pattern.console=%d{HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n
```
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

@Service
public class OrderService {
    private static final Logger log = LoggerFactory.getLogger(OrderService.class);

    public void placeOrder(Order order) {
        log.info("Placing order: {}", order.getId());
        log.debug("Order details: {}", order);
    }
}
```

---

## 27. How does Spring Boot decide server port priority?

**Definition:**  
Port is resolved in this priority order (highest to lowest):

```
1. CLI argument:          --server.port=9090
2. OS environment var:    SERVER_PORT=9090
3. application-{profile}.properties: server.port=9090
4. application.properties: server.port=8080
5. Default:               8080
```

**Special values:**
- `server.port=0` → assigns a random available port (useful for tests)

**Analogy:**  
Like setting a meeting room. Your personal preference (CLI) overrides your manager's suggestion (env var), which overrides the team default (properties file).

**Test Example:**
```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
class MyTest {
    @LocalServerPort
    private int port;  // injects the randomly assigned port
}
```

---

## 28. What happens internally when you hit a REST endpoint?

**Definition:**  
Full request flow:

```
1. HTTP Request arrives → Embedded Tomcat receives it
2. Tomcat → passes to DispatcherServlet (Front Controller)
3. DispatcherServlet → HandlerMapping (finds matching @RequestMapping method)
4. HandlerMapping → returns HandlerExecutionChain (handler + interceptors)
5. DispatcherServlet → HandlerAdapter (adapts and calls the controller method)
6. Interceptors run (preHandle)
7. Controller method executes → returns data
8. @ResponseBody / @RestController → HttpMessageConverter converts to JSON
9. Interceptors run (postHandle)
10. Response written to HttpServletResponse → sent back to client
```

**Analogy:**  
Like a restaurant order. Customer (HTTP request) → Hostess (Tomcat) → Head Waiter (DispatcherServlet) → Menu lookup (HandlerMapping) → Waiter (HandlerAdapter) → Chef (Controller) → Plating (MessageConverter) → Customer gets food (JSON response).

---

## 29. Why is Spring Boot preferred for cloud-native apps?

**Definition:**  
Spring Boot aligns with the **12-Factor App** methodology and cloud-native principles:

| Cloud Requirement | Spring Boot Feature |
|---|---|
| Stateless | Encourages stateless REST services |
| Config externalized | `application.properties`, env vars, Spring Cloud Config |
| Health checks | Actuator `/health` endpoint |
| Self-contained | Fat JAR with embedded Tomcat |
| Fast startup | Minimal config, AOT compilation (Spring Boot 3+) |
| Containerizable | Small Docker image via layered JARs |
| Observability | Actuator + Micrometer + distributed tracing |
| Resilience | Spring Cloud + Resilience4j integration |

**Dockerfile Example:**
```dockerfile
FROM eclipse-temurin:21-jre
COPY target/app.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

---

## 30. What are the most common Spring Boot performance mistakes?

**Definition & Solutions:**

### Mistake 1: N+1 Query Problem
```java
// BAD — fires N+1 queries
List<Order> orders = orderRepo.findAll();
orders.forEach(o -> o.getItems().size()); // lazy load triggers per order

// GOOD — one query with JOIN FETCH
@Query("SELECT o FROM Order o JOIN FETCH o.items")
List<Order> findAllWithItems();
```

### Mistake 2: Not using connection pool tuning
```properties
# Default pool size (10) may be too small/large
spring.datasource.hikari.maximum-pool-size=20
spring.datasource.hikari.minimum-idle=5
spring.datasource.hikari.connection-timeout=30000
```

### Mistake 3: Loading entire dataset into memory
```java
// BAD
List<User> allUsers = userRepo.findAll(); // millions of records → OutOfMemoryError

// GOOD — use pagination
Page<User> users = userRepo.findAll(PageRequest.of(0, 100));
// OR use streams/JPA scrolling for batch processing
```

### Mistake 4: Disabling caching for expensive operations
```java
@Service
public class ProductService {
    @Cacheable("products")  // Cache after first call
    public Product findById(Long id) {
        return productRepo.findById(id).orElseThrow();
    }
}
```
```yaml
spring:
  cache:
    type: redis  # Use Redis for distributed caching
```

### Mistake 5: Enabling all Actuator endpoints in production
```yaml
# BAD — exposes sensitive data
management.endpoints.web.exposure.include=*

# GOOD — only expose what's needed
management.endpoints.web.exposure.include=health,metrics
```

### Mistake 6: Not using async for I/O-bound operations
```java
@Service
public class EmailService {
    @Async  // Runs in separate thread pool
    public CompletableFuture<Void> sendEmail(String to, String body) {
        // non-blocking email send
        return CompletableFuture.completedFuture(null);
    }
}
```

---

## Quick Reference Summary

| # | Topic | Key Takeaway |
|---|---|---|
| 1 | Auto-configuration | `@Conditional*` + `spring.factories` |
| 2 | starter-web | Aggregator POM → pulls Tomcat, MVC, Jackson |
| 3 | Convention over config | Sensible defaults, override only what you need |
| 4 | Properties loading | ConfigDataEnvironmentPostProcessor, 4 locations |
| 5 | Startup flow | 11 ordered steps from main() to READY |
| 6 | ComponentScan | Part of @SpringBootApplication |
| 7 | Embedded Tomcat | ConditionalOnClass + TomcatServletWebServerFactory |
| 8 | Duplicate beans | NoUniqueBeanDefinitionException → use @Qualifier/@Primary |
| 9 | Profiles | application-{profile}.properties + @Profile |
| 10 | SpringFactoriesLoader | Reads META-INF/spring.factories |
| 11 | No XML | @Configuration + auto-config replaces all XML |
| 12 | @RestController | = @Controller + @ResponseBody |
| 13 | Dependency versions | spring-boot-dependencies BOM |
| 14 | Bean lifecycle | Instantiate → Inject → @PostConstruct → Use → @PreDestroy |
| 15 | Externalized config | 17 property sources, CLI args win |
| 16 | yml vs properties | Both loaded; .properties takes higher priority |
| 17 | Actuator | Auto-configured management endpoints |
| 18 | @Configuration | CGLIB-proxied for singleton guarantee |
| 19 | DataSource | DataSourceAutoConfiguration → HikariCP |
| 20 | CommandLineRunner | Post-startup init: seeding, warming caches |
| 21 | Exception handling | @ExceptionHandler → @ControllerAdvice → BasicErrorController |
| 22 | @EnableAutoConfiguration | Conditional + broad vs @Import (explicit) |
| 23 | Exclude auto-config | Removed before bean creation |
| 24 | Microservices | Embedded server + fat JAR + actuator + Spring Cloud |
| 25 | Fat JAR | Self-contained: classes + deps + server |
| 26 | Logging | SLF4J + Logback default, INFO level |
| 27 | Port priority | CLI > env var > profile props > props > default 8080 |
| 28 | REST request flow | Tomcat → DispatcherServlet → HandlerMapping → Controller |
| 29 | Cloud-native | 12-factor alignment, actuator, layered JARs |
| 30 | Performance mistakes | N+1, pool tuning, pagination, caching, async |

---