<img align="left" width="200" src="../graphix/rexlogo.png"/>
<br/>
<br/>

# IT-REX Newsletter #2

<p align="right">Published: Dec 23, 2020</p>
<br/>

## Roadmap

We are currently setting up the toolchain to implement first basic functionality, while further refining the architecture to adhere to requirements regarding deployment and operation. See our roadmap below:

![Roadmap](../graphix/roadmap02.png)

## Sprint Goal Overview:
* **Last sprint** (finished Dec 22, 2020): Bring IT-REX to life with first basic functionality!
* **Current sprint** -- No current sprint due to Christmas break --

## Latest Decisions

In order to implement first functionality and get a feeling for the system, own storage solutions will be used for all data. In parallel, alternative solutions using existing large-scale systems focusing on the available systems at the University of Stuttgart will be explored (ILIAS, OpenCast). 

## Latest Achievements

* Set-up of a **Continuous Integration and Deployment Toolchain**: A Jenkins was set up including a pipeline for building the client application. The pipeline for the backend, i.e. single microserivces, is still in progress. 
* Designed a **Strategy for Implementing the UI** - see details in the [Wiki](https://github.com/IT-REX-Platform/Wiki/wiki/Development--UI-Design-and-Implementation-Strategy-and-Tools).
* Defined the remaining parts of the **Technology Stack**: In addition to the previous decision of using Expo for the Frontend, we decided to implement microservices with Java 11 using Spring Boot. In addition, the adoption of JHipster for the microservices environment is currently under exploration.
* Definition of **Quality Assurance Methods and Tools** is in progress: The focus is on Testing, Static Code Analysis and Coding Conventions. Plugins and Tools are currently being explored and defined. 

## Next Steps

* Finish remaining tasks from Sprint#2
* Enjoy the Christmas Break :-)

## [Newsletter-Archive](https://github.com/IT-REX-Platform/Wiki/tree/main/newsletter/archive)