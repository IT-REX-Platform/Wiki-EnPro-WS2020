## Sample Spring Boot Application (for Workshop) with Spring MVC

We want to build a simple todo list that writes new todos to a database and displays them in a web UI.

The code for the finished application can be found here: https://github.com/Well5a/todolist

Prerequisites:
* JDK 11
* Running PostgreSQL Database on Port 5432: https://www.postgresql.org/download/

Create the initial project with https://start.spring.io/

We need the following modules:
* Spring Web: Building web applications with Spring MVC
* Spring Data JPA: Connection to (relational) database
* PostgreSQL Driver: JDBC driver that allows Java applications to connect to PosgreSQL databases
* Thymeleaf: Template engine, allows integration of HTML files.

We will build the app according to the Spring Web MVC framework. This is a framework contained in the Spring Web dependency. From https://www.tutorialspoint.com/spring/spring_web_mvc_framework.htm:

Spring Web MVC provides a Model-View-Controller (MVC) architecture and ready components that can be used to develop flexible and loosely coupled web applications. MVC is an architectural pattern that has the aim to split up an application into the three aspects of data (Model), UI (View) and business (Controller) logic.
* The **Model** encapsulates the application data and in general they will consist of a POJO (Plain Old Java Object).
* The **View** is responsible for rendering the model data and in general it generates HTML output that the client's browser can interpret.
* The **Controller** is responsible for processing user requests and building an appropriate model and passes it to the view for rendering.

According to this we have to split our application into different classes and files. The classes are annotated so that the Spring Framework can interpret them according to their use case and inject the necessary dependencies.

### Model

For the Model we need an Entity and (if we persist the data externally, e.g. in a database) a Repository class:

```
@Entity
public class TodoItem {
    @Id
    @GeneratedValue
    long Id;
    String name;
    boolean isDone;
    public TodoItem(String name, boolean isDone) {
        this.name = name;
        this.isDone = isDone;
    }
}
```

```
@Repository
public interface TodoRepository extends CrudRepository<TodoItem, Long> {}
```

The Entity is a POJO and represents the data in the application that is stored in the database. The Repository is the interface to this database and provides functions for data access. We can extend it with existing super classes by Spring (e.g. CrudRepository) to make use of general predefined functions, like retrieving an entity by its Id.

### View

The view in this example project is handled by the template engine Thymeleaf. In ITRex we will have an external frontend service that is responsible for the UI. Therefore we won't need such template engines and we won't go into further details about this.

### Controller

In the RestController class we specify the HTTP endpoints that our application shall provide and that are later used by the frontend service or other backend services in our system. The Controller should only handle incoming requests and should delegate further processing to Services. Apart from that the Controller should only build up the response, check authorization and do error handling - but never actual business logic.

```
@RestController
public class TodoController {
    @Autowired
    private TodoService service;

    @GetMapping("/")
    Iterable<TodoItem> todo() {
        return service.getTodos();
    }

    @PostMapping("/{todo}")
    String addTodo(@PathVariable String todo) {
        return service.addTodo(todo);
    }

    @DeleteMapping("/{id}")
    String deleteTodo(@PathVariable long id) {
        return service.deleteTodo(id);
    }
}
```

```
@Service
public class TodoService {
    @Autowired
    private TodoRepository repo;

    Iterable<TodoItem> getTodos() {
        return repo.findAll();
    }

    String addTodo(String todo) {
        repo.save(new TodoItem(todo, false));
        return "added todo " + todo;
    }

    String deleteTodo(long id) {
        repo.deleteById(id);
        return "deleted todo with id " + id;
    }
}
```
Here the Controller provides three endpoints to get a list of the todos in the database, add a new todo and delete a todo. With the `@Autowired` annotation it is possible to link to another class and use its functions. In the Service we can see the predefined functions of Spring provided by the `TodoRepository`.

### Configuration

Spring Boot provides extensive default configuration but we still need to configure some things (like database credentials) or change some things (like the server port). This can be done in several ways but the easiest way to do this is in the `application.properties` file:

```
server.port=5555
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=todo
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
```
