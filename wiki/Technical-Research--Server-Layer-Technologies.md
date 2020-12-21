# Server Layer

## **Language**: Java

We can only use JVM languages with Spring. Java is the language most of the developers know and wished to use. I suggest to use Java 11 as it is the standard version today.

Download of OpenJDK 11: https://adoptopenjdk.net/


## **BuildTool**:

Article comparing Ant, Maven and Gradle: https://www.baeldung.com/ant-maven-gradle


## **Framework**: Spring and Spring Boot

Spring is a Framework for JVM languages like Java that expands their functionality and has the aim to make programming "quicker, easier, and safer" (https://spring.io/why-spring). For that purpose it offers a comprehensive programming and configuration model. It also provides a set of modules for different use cases like Spring Data or Spring Cloud that follow this general model. Those modules offer libraries for implementing functionality for their specific use case.

For example [Spring Data](https://spring.io/projects/spring-data) has the aim to provide a consistent programming model for data access. To also retain special traits and advantages of different data store technologies it is composed out of several sub modules like Spring Data JDBC, JPA, Redis, MongoDB or REST.

[Spring Boot](https://spring.io/projects/spring-boot) is another (yet special) module that makes it easier to create Spring applications. It helps to combine different modules in one project and offers meaningful but minimal standard configuration for the integrated libraries. Furthermore it follows the idea to just setup a Spring Boot application and being able to run it immediately. For that it automatically includes an application server (e.g. with Tomcat).

Quickstart guide with Spring Boot: https://spring.io/quickstart
