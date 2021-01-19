
## Backend: Java/Spring Boot 


In order to find out which metrics in the area of Static Code Analysis are considered necessary and useful by the developers of the team, a survey was launched using Mentimeter.  

These are the results: 

![SurveyResults](./Images/StaticCodeAnalysis_Survey.png)

**Ranking**:

1. Code conventions
2. Nesting depth
3. Testing coverage 
3. Path complexity 
4. Potential bugs
5. Code Smells
    1. Lines of code (per class)
    2. Duplicates (Clones)
    3. Code vs comment lines


## Code Conventions

**Goal:** More readable, consistent coding style to simplify teamwork. 

**Measures:** [Sun Code Conventions](https://introcs.cs.princeton.edu/java/11style/codeconventions-150003.pdf) (Oracle)

**Tool:**  To check if the written source code in the backend conforms to the [Sun Code Conventions](https://introcs.cs.princeton.edu/java/11style/codeconventions-150003.pdf), 
 Intellij is used locally with the Checkstyle plugin. Checkstyle is also used to check the coding conventions during continuous integration.

### Checkstyle
"Checkstyle is a development tool to help programmers write Java code that adheres to a coding standard. It automates the 
process of checking Java code to spare humans of this boring (but important) task. This makes it ideal for projects that 
want to enforce a coding standard." [2](https://checkstyle.sourceforge.io/index.html)

Intellij is a leading Java IDE with built-in code inspection and analysis. With the additional help of the Checkstyle Plugin,
Intellij takes care of the correct formatting, e.g. with regard to indentation (In relation to the Sun Code Conventions), 
and marks violations of the Google Java Code Guidelines. A list of what conventions Checkstyle checks can be found [here](https://checkstyle.sourceforge.io/google_style.html). 

#### Plugin installation and configuration Checkstyle

**Precondition:** Intellij is already installed and opened 
 
1. Navigate to: File &rarr; Settings &rarr; Plugins
2. Search for **CheckStyle-IDEA** and install the plugin
3. Navigate to: File &rarr; Settings &rarr; Tools &rarr; Checkstyle 
4. Select **Sun Checks** as Configuration File
5. Adjust the scan scope if necessary 

Adding the code style schema to the editor:
5. Download the sun_style.xml 
6. Navigate to:  File &rarr; Settings &rarr; Editor &rarr; Code Style
7. Import the sun_style.xml scheme as follows: ![CodeStyleSchema](./Images/CodeStyleSchama.png)

 **&rarr; Restart Intellij**
 
 After the restart the CheckStyle Plugin automatically checks the Sun Code Conventions in the Background and marks the violations in the editor.  

#### Code Style Reporting

1. Open build.gradle file located in project base directory. Gradle functionalities are organized into tasks.
Gradle Plug-Ins provide new functionalities to a build.

2. add the checkstyle plugin via "apply plugin: 'checkstyle' ".

3.  configure checkstyle plugin:
"checkstyle{ toolVersion = '6.16.1'
}"

4. create a subdirectoriy in the project named "config/checkstyle".

5. create a file in the created directory with the name "checkstyle.xml".

6. Paste in the rules included in the "sun_checks.xml" in here. 

7. Run "gradlew clean build" in the terminal to initiate the build process.

8. In the project you should now find the report in the path "build/reports/checkstyle" 

9. Checkstyle generates separate reports for each source set.  A list of classes and violations will be shown. 
Under that list, the violations of the code conventions are described in more detail. 



## Nesting depth
**Goal:** Avoid too deep nesting, as the readability and complexity of the code may suffer.

**Measure:** Define rules for the nesting depth.

**Tool:** The allowed nesting depth can be regulated with the help of additional Checkstyle rules in for, try, if and switch. These rules must be included in the sun_checks.xml.  

## Testing coverage 

**Goal:** Avoid bugs early and create the most qualitative code base as possible.	

**Measure:**  Make sure that the code base is well covered by JUnit tests.

**Tool:** Local: Jacoco/Intellij CI-Environment: Jacoco  

### Jacoco
Jacoco is a widely used well tested test coverage tool and has good documentation. The integration with gradle projecte is very easy. Reports are provided in .html, .csv and .xml format.

### Test Coverage Reporting
1. Open build.gradle file located in project base directory. Gradle functionalities are organized into tasks.
Gradle Plug-Ins provide new functionalities to a build.

2. add the checkstyle plugin via "apply plugin: 'jacoco' ".

3.  configure checkstyle plugin:
"jacoco {
     toolVersion = "0.8.5"
 }"

7. Run "gradlew clean build jacocoTestReport" in the terminal to initiate the build process.

8. In the project you should now find the reports in the path "build/reports/jacoco/test" 


## Path complexity 

## Potential bugs
**Goal:** Reduce the number of possible bugs to get an error-free code base.

**Measure:** Search for error patterns to avoid actual errors.

**Tool:** PMD? 

### PMD 

For PMD there is a ruleset in .xml format that can be customized as required.
 
**Features:**
- Possible Bugs
- Dead Code
- Suboptimal Code (Wasteful String/ String Buffer usage)
- Overcomplicated Expressions (Unnecessary if statements, for loops that could be while loops)
- Cyclomatic Complexity
- Duplicated code  
- ...

### Reporting

1. Open build.gradle file located in project base directory. Gradle functionalities are organized into tasks.
Gradle Plug-Ins provide new functionalities to a build.

2. add the checkstyle plugin via "apply plugin: 'pmd' ".

3.  configure the pmd plugin:
"pmd {
     toolVersion = '5.4.1'
     ruleSetConfig = rootProject.resources.text.fromFile('config/pmd/ruleset.xml')
     ignoreFailures = true
 }"
 <br>
  With the configuration "ignoreFailures = true", allows the build to continue if there are warnings. 
  There is a whole [list of configurations](https://docs.gradle.org/current/dsl/org.gradle.api.plugins.quality.Pmd.html) that can be made.

4. create a subdirectoriy in the project named "config/pmd".

5. create a file in the created directory with the name "ruleset.xml".

6. Paste in the rules included in the "pmd_ruleset.xml" in here. 

7. Run "gradlew clean build" in the terminal to initiate the build process.

8. In the project you should now find the reports in the path "build/reports/pmd" in .xml and .html format.  

9. Pmd generates separate reports for each source set.  A list of classes and violations will be shown. 
An explanation of the problem found is provided in the link under "Problem".   



## Code Smells
#### Lines of code (per class)
**Goals:** Files with no more than 2000 lines to ensure understandability and manageability.

**Measure:** Sun Code Conventions	

**Tool:** Local: Intellij/Checkstyle (Sun Code Conventions) CI-Environment: Checkstyle (Sun Code Conventions)



The Sun conventions that are used for coding conventions define: Files longer than 2000 lines are cumbersome and should be avoided.

How Checkstyle can be integrated with the Sun Code Conventions, can be found above. 
#### Duplicates (Clones)

Intellij/Checkstyle/PMD 

Checkstyle rule: \<module name="StrictDuplicateCode"/>


 



## Sources
- [1] [Static Code Analysis](https://www.perforce.com/blog/sca/what-static-analysis)
- [2] [Checkstyle](https://checkstyle.sourceforge.io/index.html)
- [List of Tools for static code analysis](https://en.wikipedia.org/wiki/List_of_tools_for_static_code_analysis)
- [Using the Gradle Checkstyle Plugin for Code Style Reporting](https://www.youtube.com/watch?v=zo3zyyo7Vkw)
