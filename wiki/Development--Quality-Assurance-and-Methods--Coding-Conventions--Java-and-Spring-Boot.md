## Coding Conventions Java/Spring Boot

As documented in the topic Static Code Style Analysis, the plugin [Checkstyle](https://checkstyle.sourceforge.io/index.html) 
is used for checking the Code Conventions. 
Checkstyle supports the [Sun Code Conventions](https://introcs.cs.princeton.edu/java/11style/codeconventions-150003.pdf) 
as well as [Google Java Style Guide](https://checkstyle.sourceforge.io/styleguides/google-java-style-20180523/javaguide.html).

It was decided to use the [Sun Code Conventions](https://introcs.cs.princeton.edu/java/11style/codeconventions-150003.pdf).

#### Basic Sun Code COnventions 
* **Naming Conventions**:
    * All names should be formulated in a expressive way apart from e.g. counters in loops
    * **File names**: case-sensitive name of the top-level class
    * **Class names**: 
        * UpperCamelCase
        * Nouns or noun phrases
    * **Method names**:
        * lowerCamelCase
        * verbs or verb phrases 
    * **Constant names**: 
        * UPPERCASE_LETTERS
    * **Parameter/Local variable names**:
        * lowerCamelCase        
* **Formatting**:
    * **Braces** are used with if, else, for, do and while statements, even when the body is empty or contains only a single statement. 
        * No line break before the opening brace.
        * Line break after the opening brace.
        * Line break before the closing brace.
        * Line break after the closing brace, only if that brace terminates a statement or terminates the body of a method, constructor, or named class. For example, there is no line break after the brace if it is followed by else or a comma.
    * **Line Length**: max length 100 characters 
    * ...
    * Intellij automatically formats the code according to the Google Java Code Guidelines if the google_style.xml is imported.
* **Comments**:
    * **Javadoc Comments:**  A doc comment must precede a class, field, constructor or method declaration. Used to to define the overall purpose or behavior of a class or member/method.  
        * It is made up of two parts: A description followed by block tags.
        * The block tags used for our purposes should be: (@author)? @param, @return, @throws, @deprecated in this order 
    * **Implementation Comments**: Use Multi-line or Single-line Comments
                 

#### [Best Practises Spring Boot](https://www.e4developer.com/2018/08/06/spring-boot-best-practices/) 
* 'Correct' Project structure
    * keep entry Class in top-level source directory
    * well-named packages
    * keep all controllers together 
* Keep **@Controller’s** clean and focused
    * Controllers should be stateless 
    * Controllers should not execute business logic but rely on delegation
* Build your **@Service’s** around business capabilities
* ...


## Sources

- [Code Conventions](https://www.triology.de/blog/code-conventions)
- [Spring Boot best practices](https://www.e4developer.com/2018/08/06/spring-boot-best-practices/)
