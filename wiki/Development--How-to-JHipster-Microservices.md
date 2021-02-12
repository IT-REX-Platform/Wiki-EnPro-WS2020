- [Preliminary](#preliminary)
- [Working with JHipster Microservices](#working-with-jhipster-microservices)
  - [Preconditions](#preconditions)
  - [```written```-Packages](#written-packages)
  - [Implementing Business Logic](#implementing-business-logic)
  - [Running Microservices](#running-microservices)
- [Creating new Microservices with JHipster](#creating-new-microservices-with-jhipster)
  - [Preconditions](#preconditions-1)
  - [JDL](#jdl)
    - [IT-REX JDL Files](#it-rex-jdl-files)
    - [JDL Options in Use](#jdl-options-in-use)
  - [Steps to create a new Microservice](#steps-to-create-a-new-microservice)
  - [Updating existing microservices with JHipster](#updating-existing-microservices-with-jhipster)
    - [Changing entities](#changing-entities)

# Preliminary 

We decided on Feb 12, 2021 to stop using the DSL provided by jHipster, the JDL, for the development of our application. **We will only use the JDL in order to set-up the application structure.** So we specifically use the JDL to persist the set-up of each backend-component, namely the Gateway and each single Microservice.

Reasoning: The JDL allows the specification of entities, which results in the automatic creation of a full-blown CRUD-Application based on Spring Boot. The generated code works well, but does not provide all options we need. Adapting the generated code to specific needs however is impossible due to overriding behaviour and non-working flags in the jHipster generator.

Consequently, using the JDL is only relevant for you, dear reader, if you want to create a new microservice! [Or if you, if it so happens, want to adapt the existing set-up which you should consider carefully.]

We version the JDL-files in our central [JDL Git-Repository](https://github.com/IT-REX-Platform/JDL).

# Working with JHipster Microservices

This chapter describes how we work with the project structure created with the JHipster generator. I.e., we describe how we put our code in an existing JHipster microservice.

If you want to set-up a nem microservice, continue reading [Creating a new Microservice with JHipster](#creating-new-microservices-with-jhipster).

## Preconditions

1. Follow the [Enviornment Setup](Development--Environment-Setup.md).

2. Clone repositories from GitHub.

- Backend (Recommendation: Create new directory 'Backend' and clone all repositories in there):
  - git@github.com:IT-REX-Platform/Gateway.git
  - git@github.com:IT-REX-Platform/["AllMicroservices"] (e.g.IT-REX-Platform/CourseService.git)
- [optional] Frontend: git@github.com:IT-REX-Platform/Frontend.git

## ```written```-Packages

Unfortunately, as the JHipster generator does not properly respond to all flags and configuration options, we cannot avoid generated code at all times. In ordert to not interfer with generated code and the JHipster generator, we decided to move **all custom java code to subpackages named ```written```**. Accordingly, this is the resulting procject structure: 

TODO

## Implementing Business Logic

After the decision to stop using the JDL for the creation of custom domain entities, we decided to add the required Java-Classes manually, as we will also need manual implementation in order to fullfill our requirements. All classes should therefore be added in the ```written```-Packages described above.

Follow the structure introduced in the [Spring Boot Workshop (see docs)](Technical-Research--Server-Layer-Technologies--Spring-Boot-and-MVC.md): Entities, Repositories, Services and RestControllers.

## Running Microservices

Follow the [documentation for starting the backend consisting of multiple microserivces](Development--How-to-start-a-backend-service.md). If want to implement backend logic, the partial set-up is for you :wink:. 

| :information_source: **Encountered errors while executing and how to resolve them**|
|---|

- OS: Windows - While running the main class - :openApiGenerate is failing<br/>
  `javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed` <br/>
  When you see this error, check which Java version your IntelliJ is using - we need Java 11. You can do this under **File** - **Project Structure** - **Project Settings**

- OS: Windows - While running the main class <br/>
  `Command line is too long. Shorten command line for GatewayApp or also for Spring Boot default configuration?`<br/>
  Go Into your **run configuration** - open the sub-menu **Environment** - In the select fiel **Shorten Command Line** change the value to: **@argfile (Java 9+)** instead of **user-local default:none**

# Creating new Microservices with JHipster

This chapter describes how to create a new microservice with JHipster.

## Preconditions

What needs to be installed and how?

1. Follow the [Enviornment Setup](Development--Environment-Setup.md).

2. jHipster generator
  - Via NPM:
    ```bash
    npm install -g generator-jhipster
    ```
    This will install the most up-to-date version. Currently, this is ```6.10.5``` which is also the version we are using.
    To install this specific version, use
    ```bash
    npm install -g generator-jhipster@6.10.5
    ```
  - Alternatively with Docker:
    ```
    docker container run --name jhpster_generator -v $(pwd):/home/jhipster/app -v ~/.m2:/home/jhipster/.m2 -p 8080:8080 -p 9000:9000 -p 3001:3001 -it --rm jhipster/jhipster:v6.10.5 bash
    ```

## JDL

The JDL documentation can be found here: https://www.jhipster.tech/jdl/. Be careful, as most flags do not work as indicated in the documentation! We list all flags we use in [JDL Options in Use](#JDL-Options-in-Use). 

### IT-REX JDL Files

We store all JDL-files in our central [JDL Git-Repository](https://github.com/IT-REX-Platform/JDL). Consequently, the single project repositiries for each microservice do not contain JDL-files, so do not bother searching for them :wink:. Each microservice is specified in an individual JDL-file however, but the files are still stored centrally.

JDL-Files can be edited with [JDL-Studio](https://start.jhipster.tech/jdl-studio/) or [VS-Code](https://www.jhipster.tech/configuring-ide-visual-studio-code/).

### JDL Options in Use

TODO

important fields for us
- we don't use dtos anymore because they only serve a purpose when changing them and we don't wnat to do this with generated code. If we need to change the representation of the domain entity in the client we need to define our own dto.
- use UUID in entities??

## Steps to create a new Microservice

1. Clone the JDL-Repository (Recommendation: inside the Backend-dir containing all exising microserices): 
    ```git
    git clone https://github.com/IT-REX-Platform/JDL.git
    ```

2. Create a new JDL file based on the template available in the JDL-Repository (we will call the new service ```MyNewRexService``` and the JDL-File ```myNewRexService.jdl```). Use existing Microservices as Orientation and consider the list of [JDL Options in Use](#jdl-options-in-use)

3. Go to the Backend-dir in and create a new directory called ```MyNewRexService```
   - navgiate inside the new directory
   - execute the jdl to generate the service with: 
    ```bash
    jhipster import-jdl path-to-JDL-repository/myNewRexService.jdl
    ```
   - discard changes in every project except for the newly generated one and the Gateway (to avoid overriding important changes done by others). Discard Changes: Git command (git reset o.ä.)
4. In the new service add the ```written```-packages [as described earlier](#written-packages).
5. Add the defined sonar exclusions in sonar-project.properties
   TODO - link!?
6. [Needs to be discussed] Add roles of usermanagement and secure routes TODO: specify which files and what needs to be added
7. Create GitHub repository and push initial commit 

:clap: Congrats! You created a new microservice!

You might want to consider integrating it into the CI/CD as well.

TODO - link!?

TODO - clarify if anything in the gateway has to be changed if new microservices are created.

## Updating existing microservices with JHipster

TODO

changes to jdl and how to integrate them in existing microservice
--ignore-application

### Changing entities

1. Create new Entity in the it-rex.jdl
2. Assign the Entity to the according microservice in the application section
3. Create a serviceClass, append the new Entity to the `service-line`
4. Append the new Entity to the according `microservice-line`
5. Execute `jhipster import-jdl it-rex.jdl --ignore-application` (Don't regenerate the whole application, like SecurityConfig.java and sonar-project.properties)

Was wird von JDL generiert und wie wird die REST-Schnittstelle davon beeinflusst? (e.g. )
Wie wird REST-Schnittstelle für Frontend implementiert?
