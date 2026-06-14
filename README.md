# Java Interview Questions

This document serves as a comprehensive guide for Java interview preparation, covering fundamental to advanced topics with structured explanations.

---

## Table of Contents

1. [What is JVM, JRE, and JDK?](#1-what-is-jvm-jre-and-jdk)
2. [What are the main features of Java?](#2-what-are-the-main-features-of-java)
3. [What is the difference between OOP and SOP?](#3-what-is-the-difference-between-oop-and-sop)
4. [Why is Java not a pure object-oriented language?](#4-why-is-java-not-a-pure-object-oriented-language)
5. [What is a classloader and what are its types?](#5-what-is-a-classloader-and-what-are-its-types)
6. [What is the difference between an Instance variable and a Local variable?](#6-what-is-the-difference-between-an-instance-variable-and-a-local-variable)
7. [What are memory allocations available in Java?](#7-what-are-memory-allocations-available-in-java)
8. [Why are Java Strings immutable?](#8-why-are-java-strings-immutable)
9. [What is the difference between String, StringBuffer, and StringBuilder?](#9-what-is-the-difference-between-string-stringbuffer-and-stringbuilder)
10. [What is Garbage Collection in Java and how does it work?](#10-what-is-garbage-collection-in-java-and-how-does-it-work)

---

## Questions and Answers

### 1. What is JVM, JRE, and JDK?

- **JVM (Java Virtual Machine):** It is an abstract machine that provides the runtime environment in which Java bytecode can be executed. JVM is platform-dependent (different for Windows, Mac, Linux), but it is what makes Java bytecode platform-independent.
- **JRE (Java Runtime Environment):** It is a software package that provides the minimum requirements for executing a Java application. It contains the JVM, core libraries, and other supporting files. It does not contain development tools like compilers or debuggers.
- **JDK (Java Development Kit):** It is a full-featured software development kit required to develop and execute Java applications. It contains everything that JRE has, plus development tools such as the Java compiler (`javac`), debugger, and javadoc tool.

**Relationship:** `JDK = JRE + Development Tools` and `JRE = JVM + Core Libraries`.

---

### 2. What are the main features of Java?

- **Simple:** Easy to learn, and its syntax is clean and concise. Removes complex features like explicit pointers and operator overloading.
- **Object-Oriented:** Everything in Java is an Object (except primitive types), following concepts like Inheritance, Polymorphism, Abstraction, and Encapsulation.
- **Platform Independent:** Follows the "Write Once, Run Anywhere" (WORA) philosophy. Code is compiled into bytecode, which runs on any machine with a JVM.
- **Secure:** Java runs inside a virtual machine sandbox, lacks explicit pointers, and offers automated memory management.
- **Robust:** Emphasizes early checking for possible errors, with strong compile-time and runtime error-checking, plus a robust Exception Handling framework.
- **Multithreaded:** Java has built-in support for writing programs that can perform many tasks concurrently.

---

### 3. What is the difference between OOP and SOP?

- **OOP (Object-Oriented Programming):** Focuses on data and objects rather than logic and actions. Programs are organized around objects and data binding. Examples: Java, C++, Python.
- **SOP (Structural / Procedural Oriented Programming):** Focuses on writing code in a sequence of steps, procedures, or functions to solve a problem. It treats data and code as separate entities. Examples: C, Pascal.

---

### 4. Why is Java not a pure object-oriented language?

Java is not considered a pure object-oriented language because it supports **primitive data types** (such as `int`, `char`, `float`, `double`, `boolean`, etc.) which are not objects. In a pure object-oriented language, everything must be an object. While Java provides wrapper classes (`Integer`, `Character`, etc.) and autoboxing, the baseline existence of primitives prevents it from being 100% pure.

---

### 5. What is a classloader and what are its types?

A **Classloader** is a part of the JRE that dynamically loads Java classes into the JVM during runtime when they are referenced for the first time.

There are three main types of built-in classloaders in Java:

1.  **Bootstrap Classloader:** Loads core Java platform classes from the JDK internal packages (like `java.lang.*`, `java.util.*` via `rt.jar` or module systems).
2.  **Extension / Platform Classloader:** Loads classes from the extension directories or platform-specific extensions.
3.  **Application / System Classloader:** Loads the application-specific classes from the environment paths specified by the system `CLASSPATH` variable or `-classpath` option.

---

### 6. What is the difference between an Instance variable and a Local variable?

- **Instance Variable:** Declared inside a class but outside any method, constructor, or block. They are created when an object is instantiated and are accessible to all methods of the class. They take default values if uninitialized.
- **Local Variable:** Declared inside a method, constructor, or block. They are created when the block is entered and destroyed upon exit. They do not have default values and must be initialized before use.

---

### 7. What are memory allocations available in Java?

Java separates runtime memory primarily into two sectors:

- **Heap Memory:** Used for allocating memory to objects and instance variables dynamically during runtime. All objects created via the `new` keyword reside here. It is shared across all threads.
- **Stack Memory:** Used for execution threads. It holds short-lived local variables, references to objects in the heap, and method invocation frames. Each thread has its own private stack memory.

---

### 8. Why are Java Strings immutable?

Strings are immutable (cannot be changed once created) for several design reasons:

- **String Pool:** Java optimizes memory by storing string literals in a common "String Constant Pool". Multiple references can point to the same literal. If strings were mutable, changing one reference would unintentionally alter the values for other references.
- **Security:** Strings are widely used as parameters for network connections, database URLs, file paths, and username/password entries. Immutability ensures these vital parameters cannot be altered mid-execution.
- **Thread Safety:** Since they cannot be modified, strings are inherently thread-safe and can be shared among multiple threads without synchronization.
- **Caching HashCode:** The hashcode of a string is cached during its creation. This makes it highly efficient when used as keys in HashMaps or HashSets.

---

### 9. What is the difference between String, StringBuffer, and StringBuilder?

- **String:** Immutable sequence of characters. Modifications create new objects in memory. Slowest performance under frequent manipulations.
- **StringBuffer:** Mutable sequence of characters. It is **synchronized** (thread-safe), meaning multiple threads cannot access it simultaneously. Slightly slower than StringBuilder due to synchronization overhead.
- **StringBuilder:** Mutable sequence of characters. It is **non-synchronized** (not thread-safe). It provides faster performance than StringBuffer and is preferred for single-threaded operations.

---

### 10. What is Garbage Collection in Java and how does it work?

**Garbage Collection (GC)** is an automatic memory management process in Java that tracks allocations and deletes objects that are no longer reachable or referenced by any active part of the program.

- It runs as a background daemon thread managed by the JVM.
- Developers can request garbage collection using `System.gc()`, but execution is never guaranteed immediately.
- The heap is typically divided into **Young Generation** (Eden, Survivor spaces) where new objects are born, and **Old/Tenured Generation** where long-lived objects are promoted. GC algorithms (like G1, ZGC, or CMS) selectively scan these regions to free memory.
