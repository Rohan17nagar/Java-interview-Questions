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

