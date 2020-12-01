# Implementation View

This page describes general thoughts and design decisions that were used to create the [Component Diagram v2.1](https://miro.com/app/board/o9J_ldsCOKg=/?moveToWidget=3074457352019930466&cot=12).

## **Application Architecture**

In order to enable horizontal scaling for the IT-Rex application, a Microservices Approach was chosen.
The following Diagram shows how the Domain was split up into smaller functional components, the Microservices and their interactions.

![Component-Diagram-v2.2](./Images/Architecture/Component-Diagram-v2.2.png)

For a better understandability, each Microservice will be explained in a section below.
Afterwards, another section covering general information can be found, that is not bound to single Microservices.

## **Client Side**

The Client Side consists of a single Microservice.
As the name suggests, it runs on the client's machine locally.

### **Frontend-Service**
This Service is used for displaying all the relevant information to the user.
It's main tasks are:
 * Manage user Input and forward it to the Backend for Frontend
 * Visualize Data that is received from the Backend for Frontend

With this small set of functionality, the goal was to minimize computational/logical code in order to keep the Frontend-Service as light-weight as possible.
This helps to achieve a smooth User Experience, as well as better performance on the client side.


## **Server Side**

The Server Side consists out of 12 Microservices that together form the Backend of the IT-Rex Application.




### **Backend for Frontend**
The [Backend for Frontend](https://samnewman.io/patterns/architectural/bff/) is an architectural pattern, commonly used for multiplatform scenarios.

It enables different implementations for the same backend that provides data to the Frontend-Service for visualisation.
This can be helpful when functionality changes may occur, depending on parameters like the device used by the client.

Additionally, this Service is used to call the other backend Microservices.
Typically this would happen by receiving requests from the Frontend-Service. The Backend for Frontend's tasks then consist out of:
* Validating the received inputs
* Deciding which Microservices are needed to answer the request
* Retrieving the needed Data



### **Authentication Service**


### **Course Service**

### **LMS Adapter**


### **Document Service**
### **Video Service**
### **Quiz Service**
### **Rex Duell Service**


### **Gamification Service**
### **Scoring Service**
### **Customization Service**
### **Customization Shop**
### **Ranking Service**

## **External Services**

## **General Design & Decisions**

This kind of functionality is distributed and spread across services, that own the Data 