# Static Code Analysis
"Static code analysis is a method of debugging by examining source code before a program is run. 
It’s done by analyzing a set of code against a set (or multiple sets) of coding rules."[1](https://www.perforce.com/blog/sca/what-static-analysis)

## Quality Metrics and Heuristics
Some metrics for good code that should be covered by a static analysis tool.  Can be changed / completed by the team.
- **Maintability:** (see Microsoft's Maintainability Index). Often done on method-level
- **Cyclomatic complexity:** indicates complexity of a program by quantitatively measureing the number of linearly independent paths through a program's source code. A complex control flow requires more tests to achieve good code coverage and will be less maintainable. Can be done module or program-wise Includes:
    - Depth of Nested IF/ELSE statements
    - multiple SWITCH/CASE statements
- **Lines of code:** measured on different levels: project / class / method. A very high count might indicate that a type or method is trying to do too much work and should be split up. It might also indicate that the type or method might be hard to maintain.
- **Coupling:** Measure in two directions - How many components are using the measured component and on how many components it relies on. A high number indicates that any change to the current component risks breaking those others, if many components depend on the measured one and vice versa.
- **Churn:** amount of edits (number of commits) to a source code file. A high churn indicates specific areas of the system that undergo a lot of updates. Exept for exceptions, this is normally an indicator that there are quality problems within a file.
- **Clones**
- **Compliance with Coding Conventions**

# Quick Overview
## Backend 

|Metric| Goal | Measures | Tools | 
| :--- | :--- | :--- | :--- |
|Coding Conventions| More readable, consistent coding style to simplify teamwork | Sun Code Conventions | Checkstyle Plug-In for Intellij IDEA & Jenkins | 
|Testing coverage| Avoid bugs early and create the most qualitative code base as possible | Make sure that the code base is well covered by JUnit tests. | Local: Intellij/Jacoco CI-Environment: Jacoco  |
|Potential bugs| Reduce the number of possible bugs to get an error-free code base |Search for error patterns to avoid actual errors. | Local: pmd/Intellij? CI-Environment: findbugs/pmd?| 
|Nesting depth|Avoid too deep nesting, as the readability and complexity of the code may suffer.| Define rules for the nesting depth. | Local: Intellij/Checkstyle CI-Environment: Checkstyle |
|Path complexity| -|-|pmd?|
|(Code Smells) Lines of code|Files with no more than 2000 lines to ensure understandability and manageability|Sun Code Conventions|Local: Intellij/Checkstyle CI-Environment: Checkstyle|
|(Code Smells) Duplicates|Avoid duplicated code to simplify the structure of the code base, make it shorter and easier to support|Detect and eliminate duplicate codes.|Local: Intellij/Checkstyle/Pmd CI-Environment: Checkstyle/Pmd|










## Sources
- [1] [Static Code Analysis](https://www.perforce.com/blog/sca/what-static-analysis)
- [2] [Checkstyle](https://checkstyle.sourceforge.io/index.html)
- [List of Tools for static code analysis](https://en.wikipedia.org/wiki/List_of_tools_for_static_code_analysis)
