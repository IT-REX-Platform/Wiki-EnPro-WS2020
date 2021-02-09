# Deployment View

This page describes general thoughts and design decisions that were used to create the [Deployment Diagram](https://miro.com/app/board/o9J_ldsCOKg=/?moveToWidget=3074457352127621741&cot=12) (concept on Miro).

The [Component Model](./Application-Architecture--Implementation-View) was already designed with the thoughts of smaller scalable entities as components following a Microservices approach. These components are reused in the Deployment diagram. Because of that most components and especially databases are just deployed on their own logical node. Only the gamification services are deployed together on one node for now. This is subject to change because we haven't finally decided on how to split up these services (or if we want to split them up at all).

Currently, the system is deployed using docker compose. See: 
* [CD Environment](./DevOps--Production-Environment-(CD))
* [Deployment Files GitHub Repo](https://github.com/IT-REX-Platform/Backend-Deploy)
* [Local Deployment for Devs](./Development--How-to-start-a-backend-service)

In response to the challenge of hardware resources stated in the [Architecture Docs Main Page](./Architecture-Documentation), we seek to support OpenCast as storage solution for videos. In a production deployment, setting-up and own OpenCast instance could be ommitted - in our current set-up however, we use our own instances to verify deployablitiy without having to adhere to organizational constraints. For reference, see the current state of the CD environment (link above).
