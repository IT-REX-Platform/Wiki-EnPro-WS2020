# Architecture Constraints

In the requirements elicitation with our customers, we identified a couple of requirements/constraints for IT-REX on system level, that limit our architectural options.
* Resource-heavy deployment is unrealisitic: Storage as well as network bandwith that are required to store lots of videos are expensive. Affording hardware to set-up such a system from scratch is unrealistic for the Univerisity of Stuttgart and likely for other schools/universities as well.
* In an ideal scenario, the system should work well for a quite low number of users as well as theoretically scale up to serving an entire university (e.g. University of Stuttgart with roughly 25k students and about 3.5k academic personnel).
* Only authenticated users may interact with the system. 
* IT-REX might achieve higher student acceptance, if existing log-in credentials, that their organisation provides, can be reused.
* IT-REX will achieve higher lecturer acceptance if contents uploaded to IT-REX are somehow made available via an existing system as well (e.g. replicated to ILIAS or Moodle). [Background: When setting-up IT-REX it will typically not be the primary/official platform, so there might be students unwilling to use it. Replicating the contents to an official platform manually is an overhead for lecturers which might keep lecturers from using IT-REX.]

# High-level Architectural Design Decisions

* Individual application components require independent horizontal scaling. This is especially applicable if many videos are streamed at the same time, as many open connections have to be served efficiently. Therefore, a microservice-based approach was chosen to encapsulate media streaming functionality in an independent microservice. Consequently, other functionality was split into such microservices as well, see [Implementation View](Application-Architecture--Implementation-View) for more details.
* In order to make use of existing computing resources when setting-up IT-REX, the goal for IT-REX is to use OpenCast to store videos. OpenCast is often used by universities for recording lectures and hence already equipped with quite some hardware resources. Reusing such hardware with IT-REX might make setting-up the system more realistic. See more at: [Deployment View](Application-Architecture--Deployment-View)

Design decisions on a lower level with some more details can be found in the description of different architectural viewpoints listed below.

# Architecture Views and Topics

[Implementation View](Application-Architecture--Implementation-View)

[Deployment View](Application-Architecture--Deployment-View)

[Runtime View](Application-Architecture--Runtime-View)

[Data Model](Application-Architecture--Data-Model)

[User Access Management](Application-Architecture--User-Access-Management)