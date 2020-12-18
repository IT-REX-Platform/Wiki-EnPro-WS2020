# Server Layer

## **Framework**: Spring and Spring Boot

Spring is a Framework for JVM languages like Java that expands their functionality and has the aim to make programming "quicker, easier, and safer" (https://spring.io/why-spring). For that purpose it offers a comprehensive programming and configuration model. It also provides a set of modules for different use cases like Spring Data or Spring Cloud that follow this general model. Those modules offer libraries for implementing functionality for their specific use case.

For example [Spring Data](https://spring.io/projects/spring-data) has the aim to provide a consistent programming model for data access. To also retain special traits and advantages of different data store technologies it is composed out of several sub modules like Spring Data JDBC, JPA, Redis, MongoDB or REST.

[Spring Boot](https://spring.io/projects/spring-boot) is another (yet special) module that makes it easier to create Spring applications. It helps to combine different modules in one project and offers meaningful but minimal standard configuration for the integrated libraries. Furthermore it follows the idea to just setup a Spring Boot application and being able to run it immediately. For that it automatically includes an application server (e.g. with Tomcat).

Quickstart guide with Spring Boot: https://spring.io/quickstart


## **Language**: Java

We can only use JVM languages with Spring. Java is the language most of the developers know and wished to use. I suggest to use Java 11 as it is the standard version today.

Download of OpenJDK 11: https://adoptopenjdk.net/


## Sample Spring Boot Application (for Workshop)

We want to build a simple todo list that writes new todos to a database and displays them in a web UI.

Prerequisites:
* JDK 11
* Running PostgreSQL Database on Port 5432: https://www.postgresql.org/download/

Create the initial project with https://start.spring.io/

We need the following modules:
* Spring Web: Building web applications with Spring MVC
* Spring Data JPA: Connection to (relational) database
* Spring Boot Actuator: Provides additional endpoints for health checks or metrics, always useful
* Thymeleaf: Template engine, allows integration of HTML files.
* PostgreSQL Driver: JDBC driver that allows Java applications to connect to PosgreSQL databases

We will build the app according to the MVC pattern: Model, View, Controller. The model is the data of the application and the view is handled by a template engine (thymeleaf). We only need to specify Controllers that provide interfaces for the view and Repositories that handle the data access to the database. Additionally we need an Entity, which represents data objects in our system.
