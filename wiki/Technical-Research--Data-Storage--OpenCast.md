# OpenCast

## What is OpenCast

OpenCast is a video capture, management and distribution solution for academic institutions.
At the University of Stuttgart it is used for:
  - archive and transcode videos
  - distribute videos (incl. two-stream recordings)
  - push videos to ILIAS courses
  - record videos in lecture halls
  
What it can't do:
  - live-streaming
  - complex video editing
  
## Technical Opportunities

OpenCast itself offers a REST API:

https://stable.opencast.org/rest_docs.html

The University of Stuttgart can offer Tenants on the OpenCast-Server.


## Organisational Opportunities

**Opportunity 1:** The University of Stuttgart can offer Tenants on the OpenCast-Server.

Consequence: The video store for ILIAS and IT-Rex would be seperate.

**Opportunity 2:** Get access to the same OpenCast-Tenant used by ILIAS via external API.

Consequence: Content uploaded via IT-REX could be (automatically?) reusable via ILIAS.

To be clarified: who authorizes access and implements the access. How can auth with OpenCast be handled?

## Technical Assumption

Workflow for video upload to ILIAS (as far as we understand it):

1. Lecturer authenticates and records / uploads a recording to OpenCast
2. Lecturer creates an OpenCast-Object in ILIAS
3. Lecturer links OpenCast-Recording to the according OpenCast-Object in ILIAS

Same authentication information is used for starting and accessing the recording.

All user rights are stored in ILIAS.

Consequence: if we use the same authentication, uniform access to OpenCast should be feasible


# Implementation Attempt

As documented in the [Implementation View](Application-Architecture--Implementation-View.md#media-service), the idea was to define an interface for media storage and streaming that could be implemented by adapters for the respective data store in use, i.e., an adapter for OpenCast in specific.

During the development project, in January 2020, the connection to OpenCast as video store was going to be implemented. The according JIRA-issue was: https://it-rex.atlassian.net/browse/ITREX-377

During this task, the following was achieved:
* Setting up and OpenCast instance on the [vServer](vServer.md), see: https://github.com/IT-REX-Platform/Opencast
* General exploration and feasibility of video upload to OpenCast via the external API was proven, see: https://github.com/IT-REX-Platform/prototypes/blob/upload-download-opencast/upload-download-opencast/src/test/resources/postman/opencast.postman_collection.json 

However, there are some challenges with OpenCast:
* Asynchronous processing model: how long does it take, until a video is actually processed by OpenCast? OpenCast uses messaging internally, so the MediaService / the MediaAdapter for OpenCast would have to abstract from that.
* There is only a HTTP-API for OpenCast, so a Java-wrapper API would still have to be produced.

Due to the rather slow project progress and high uncertainty regarding OpenCast, the implementation was stopped in February 2020. A protoype inlcuding the achievements mentioned above is available here:
https://github.com/IT-REX-Platform/prototypes/tree/main/upload-download-opencast.
