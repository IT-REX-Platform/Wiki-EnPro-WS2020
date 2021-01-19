<!-- omit in toc -->
# Setup dev environment

This page is about setting up the the tools that are needed for the local static code analysis. This is necessary because SonarQube is only triggered when a commit is merged onto the dev branch. 

 ![DevelopmentCycle](./Images/DevEnvironment/dev-cycle.png)
 
 [Image Source](https://docs.sonarqube.org/latest/)

- [Frontend](#frontend)
  - [ESLint and Prettier](#eslint-and-prettier)
- [Backend](#backend)
  - [SonarQube](#sonarqube)
  - [Checkstyle](#checkstyle)
  - [SonarLint](#sonarlint)

## Frontend

### ESLint and Prettier

Read [ESLint and Prettier](./Development--Quality-Assurance-and-Methods--Coding-Conventions--ESLint-and-Prettier##VSCode)

## Backend

### SonarQube

With SonarQube is a tool to automatically review Code to detect bugs, code smells and vulnerabilities. It can integrate with the existing workflow to enable continuous code inspection across the project branches and pull requests. [1](https://docs.sonarqube.org/latest/)

Everyone of us needs an account (except David maybe🤪)
1. Go to [SonarQube](http://129.69.217.173:9001)
2. Login with the username "admin" and the password "ContactChristianForThat42"
3. Got to [Users](http://129.69.217.173:9001/admin/users) ![SonarQubeUsers](./Images/SonarQubeUser.png)
4. Click on "Create User" and fill in that stuff. You can ignore the SCM stuff ![SonarQubeUsers](./Images/SonarQubeCreateUser.png)
5. Congratulations:)

### Checkstyle

This is already documented [here](./Development--Quality-Assurance-and-Methods--Static-Code-Analysis--Backend###Checkstyle).

### SonarLint

After the SonarQube scanner has analysed the code, the results are sent to the SonarQube server and to the SonarLint plugin integrated in Intellij. With this feedback you can catch and fix issues before they get to the repository. [1](https://docs.sonarqube.org/latest/)

1. Navigate to: File → Settings → Plugins
2. Search for SonarLint and install the plugin
3. Navigate to: File → Settings → Tools → SonarLint
4. Add a new SonarQube connection by clicking on the "+"
5. Adjust the scan scope if necessary
6. Choose "SonarQube" and enter the url to our instance ![6](./Images/DevEnvironment/6.png)
7. Generate your token [here](http://129.69.217.173:9001/account/security) or use your username and password ![7](./Images/DevEnvironment/7.png)
8. Thats it (almost) ![8](./Images/DevEnvironment/8.png)
9.  Now click on "Update binding"![9](./Images/DevEnvironment/9.png)

 
## Sources
- [SonarQube](https://docs.sonarqube.org/latest/)
