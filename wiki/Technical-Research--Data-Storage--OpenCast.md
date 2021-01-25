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


