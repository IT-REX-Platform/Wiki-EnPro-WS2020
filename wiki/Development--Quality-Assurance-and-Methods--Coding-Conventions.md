# Coding Conventions 

## What are Coding Conventions?
Code conventions are guidelines on the structural quality of software  for each aspect of a program written in a specific language. 
Typically, code conventions include the following areas: 

- File organization
- Indentation
- Commenting 
- Declarations
- Statements
- Whitespace
- Naming conventions
- Programming standards
- Programming principles
- Architectural best practices

## Why do we need Coding Conventions?
Coding conventions are necessary for readability, understandability, and to support teamwork. 
In addition, the later maintenance, which is probably not performed by the original developer team itself, is eased.

**Important:** Every developer of the team must conform to the code conventions to make this work.

## How are Coding Conventions defined? 

For our chosen Programming Languages/Frameworks for Frontend and Backend (Java/Spring Boot; Expo/React) there are a lot of 
already existing Coding Conventions. Commonly one of these is selected and only adaptations/extensions are recorded.    

## Coding Conventions Java/Spring Boot

As documented in the topic Static Code Style Analysis, the plugin [Checkstyle](https://checkstyle.sourceforge.io/index.html) 
is used for checking the Code Conventions. 
Checkstyle supports the [Sun Code Conventions](https://checkstyle.org/styleguides/sun-code-conventions-19990420/CodeConvTOC.doc.html) 
as well as [Google Java Style Guide](https://checkstyle.sourceforge.io/styleguides/google-java-style-20180523/javaguide.html).


A detailed list, which conventions Checkstyle checks can be found [here]((https://checkstyle.sourceforge.io/google_style.html)) for the Google Java Style  the documentation for Sun Code Conventions are here in contrast incomplete. 
Google Conventions as well as the Sun Code Conventions were also tested via the Checksytle tool. Here it was noticed that the style check with the Sun Code Conventions makes stricter restrictions than Google Java Style Guide,  
which are completely suitable for the project.

It was therefore decided to use the [Google Java Style Guide](https://checkstyle.sourceforge.io/styleguides/google-java-style-20180523/javaguide.html).

    


Spring Boot Best Practices für die Projekt Struktur und Beans/Annotations. Ansonsten aud Java Code Conventions zurückgreifen 

--> Google conventions vs sun style conventions betrachten 




Checkstyle is a development tool to help programmers write Java code that adheres to a coding standard. It automates the process of checking Java code to spare humans of this boring (but important) task. This makes it ideal for projects that want to enforce a coding standard.

Projekt struktur und Beans von Spring Beachten 




## Sources

- [Code Conventions](https://www.triology.de/blog/code-conventions)
