This page will present the findings from our kickoff meeting on the 15th December.
There we discussed and agreed upon some basic decisions like IDE, Git-Workflow and Technology.
These are going to be presented in the following.

# DevOps Motivation

! not yet finished !



# IDE

In order to bring peace and harmony to our code base, developers will be enforced to use certain styling guidelines.
The easiest way for ensuring the same stylings and to prevent technical difficulties, we decided on using the same IDE for every developer.

For frontend development this is: [Visual Studio Code](https://code.visualstudio.com/). <br>
For backend development this is: [IntelliJ IDEA](https://www.jetbrains.com/de-de/idea/). <br>

Furthermore, this will enable us to easily help other developers when facing problems through remote screen sharing or similar things.


# Git-Workflow

! not yet finished !

In order to work on different topics in parallel we also decided on a workflow.
For this, we chose the [Git-flow workflow](https://www.atlassian.com/de/git/tutorials/comparing-workflows/gitflow-workflow).
This approach works as follows:

Development is done in **Feature-Branches**. A possibility for a naming convention would be to use the jira issue number as a name here.
When the Feature is implemented and tested a pull request is created.
After the pull-request is reviewed and accepted, the code then gets merged into the **develop** branch.
The **develop** branch then contains the latest version of software.
In addition, we want a **main** branch. Nobody pushes directly to the main branch. This step is only done through our CI environment.
With this approach, we want to guarantee for a stable production environment (the codebase on **main**). Whereas the pre-production code from the **develop** branch is deployed and released for testing-purposes. This helps to see the latest changes in a production-like environment before pushing them to the production environment.


# CI-Environment

! not yet finished !



Is currently being evaluated. Most knowledge is available in Jenkins.

[Frontend Travis](https://travis-ci.com/github/IT-REX-Platform/Frontend)

[Problems with Travis](https://travis-ci.community/t/builds-hang-in-queued-state/10250) are not only that the current pricing model doesn't allow infinite usage, but that builds can idle 

~33 mins.
