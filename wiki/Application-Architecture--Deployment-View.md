# Deployment View

This page describes general thoughts and design decisions that were used to create the [Deployment Diagram](https://miro.com/app/board/o9J_ldsCOKg=/?moveToWidget=3074457352127621741&cot=12) (concept on Miro). ( :warning: The diagram is far outdated by now! The concepts are however still the same.)

The [Component Model](./Application-Architecture--Implementation-View) was already designed with the thoughts of smaller scalable entities as components following a Microservices approach. These components are reused in the Deployment diagram. Because of that most components and especially databases are just deployed on their own logical node.

Currently, the system is deployed using docker compose. See: 
* [CD Environment](./DevOps--Production-Environment-(CD))
* [Local Deployment for Devs](./Development--How-to-start-a-backend-service)
* GitHub Repositories:
  * https://github.com/IT-REX-Platform/IT-Rex-deployment
  * https://github.com/IT-REX-Platform/IT-Rex-dev

In response to the challenge of hardware resources stated in the [Architecture Docs Main Page](./Architecture-Documentation), we aim to support OpenCast as storage solution for videos. See also the [implementation prototype of an OpenCast connection](./Technical-Research--Data-Storage--OpenCast#implementation-attempt).
