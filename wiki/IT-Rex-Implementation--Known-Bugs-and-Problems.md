# Open Bugs

See also JIRA for open bug tickets: [IT-REX@Jira](https://it-rex.atlassian.net/jira/software/c/projects/ITREX/issues/?jql=project%20%3D%20%22ITREX%22%20AND%20type%20%3D%20%22Bug%22%20ORDER%20BY%20created%20DESC)

## Missing video player feature - result: currently unprotected API routes in Media Service

(Relevant commit: MediaService/[f24830d4e17e20b57f745df94b56ad831412dde5](https://github.com/IT-REX-Platform/MediaService/blob/f24830d4e17e20b57f745df94b56ad831412dde5/src/main/java/de/uni_stuttgart/it_rex/media/config/SecurityConfiguration.java#L75))  
IT-REX hosts videos, which can be streamed from a MinIO backend through the Media Service.
The Frontend uses an HTML5 videoplayer (wrapped in expo-av) for video playback.
Our authorization model, which relies on a JWT passed in a header with every request, is incompatible with this approach as the HTML5 video player does not support defining custom headers to be sent with the video file request. While expo-av does in fact appear to offer such a property to be defined, this only works with the iOS and Android targets.

To mitigate the impact of this limitation, we chose to go with UUIDs to identify valid videos. These are at the very least hard to guess and can only be obtained through properly protected endpoints.

Possible workarounds include:

1. XMLHttpRequest (CORS) -> buffer / blob -> try to play this; may cause issues with Range functionality.
2. Pass token as URL parameter and catch this in Media Service (generally not a good idea due to browser caching / history)
3. Pass token as cookie

Options 2 & 3 require additional research into the Spring Security Configuration as retrieving and processing the JWT on these levels is being handled by generated code and dependencies exclusively, so this is not a trivial change to make (or at least not to our knowledge).


## Zuul Exceptions in Gateway when watching a video

When watching a video in the Frontend there are errors with Zuul (“Error during filtering - Filter threw Exception”) in the Gateway. They are not visible in the Frontend and the watching of videos is working correctly.

The exceptions occur every time the watching of a video is started and continuously come up while watching the video.

Perhaps this is a version incompatibility of two components that are used by Jhipster.

A logfile of the thrown exception can be found [here](https://github.com/IT-REX-Platform/Wiki/blob/main/wiki/resource/logs/zuulException.md).

See also JIRA for open bug tickets: [IT-REX@Jira](https://it-rex.atlassian.net/jira/software/c/projects/ITREX/issues/ITREX-696?jql=project%20%3D%20%22ITREX%22%20ORDER%20BY%20created%20DESC)

# Known Problems and Limitations

This is a list of limitations with the current implementation and specific design decisions. For overall architectural limitations, refer to the Architecture Documentation, e.g., [the Implementation View](https://github.com/IT-REX-Platform/Wiki/wiki/Application-Architecture--Implementation-View#known-limitations).

## Content Data Model Implementation

In the design phase, a baseline for the content data model was created in order to get an overview about the respective entities and their relationships, see: [Content Data Model](Application-Architecture--Data-Model--Content).

In the current implementation state, IT-REX supports only videos, no PDFs, audio files, etc. Additionally, as described in the [Implementation View](Application-Architecture--Implementation-View#Document-Service), the service cut between the existing Media Service (handles videos) and a potential future Document Service is not fix. During the implementation of the Media Service, the entire Content Data Model was implemented on entity-level. It demonstrates a potential solution for implementing the entire model in one service including inheritence, therefore this implementation was not removed from the code-base as a reference implementation. When decision about other media types is made, this implementation may be used, remove, or altered.

## Media Adapter

The definition of a Media Interface and implementation of an according adapter for OpenCast was started, but not finished during the project. See details here: [OpenCast in our Wiki](Technical-Research--Data-Storage--OpenCast#implementation-attempt).

## Video Upload Size

Currently the upper limit of the size of videos to upload is ~70MB. This is because of a problem with the Gateway service, which JVM Heap Memory gets over utilized with larger video files. This leads to an exception in the Gateway and an internal server error.

Screenshot from Grafana:
![JVM Memory](./Images/heapOutOfMemory.PNG)

A logfile of the thrown exception can be found [here](https://github.com/IT-REX-Platform/Wiki/blob/main/wiki/resource/logs/heapOutOfMemory.md).

## Amount of joined Courses per User

In the current approach the id of the assinged courses of an Student/Lecturer are stored in the jwt which is located in the header of each http-request to the backend (see [User Access Management](./Application-Architecture--User-Access-Management)).
So each time a User join a course, the jwt and therefore the http-header gets bigger and bigger.
The default max header size which is accepted by spring is 8kb.
So a user can join a max of ~40 Courses with this configuration.

Current state:
* At the moment, the application.yml of the microservices was modified to let the server accept bigger headers.

```yml
server:
  max-http-header-size: 48000
```
* The Frontend checks the amount of joined Courses and displays a message if the "maximum" number is exeeded (See MaxCoursesAllowed.ts). Currently, this is limited to 50, so there is a very optimistic gap between the max token size to be expected at the moment, and the allowed header size.

Still, there are open to dos:
* Currently, due to the token creation config in keycloak, there are two redundant lists of roles in the token. This should be fixed and will already cut the token size in half, enabling nearly double the amout of courses per user without increasing the header size. See: https://it-rex.atlassian.net/browse/ITREX-685. 
* The amount of courses per user should be a property to be set in the application influencing the required values in the frontend, as well as the header size config in the backend services. With the introduction of an [Admin UI](./IT-Rex-Implementation--Feature-Progress#admin-user-interface), it would be possible to make this an application property to be adjusted to the needs of an admin, including the advice that more courses per user will impact request size (and consequently affect resource consumption). 
* For "normal" users, such a course limit as listed above should be no problem - they would just have to leave/delete old courses, which also results in the system not being cluttered with old, unused data. However, some users (admin, study program manager) might require to access far more courses than normal users.
  * As the admin user is not very established in the application yet, (see [Admin UI](./IT-Rex-Implementation--Feature-Progress#admin-user-interface)), it must also be ensured that an admin can access any course with full priviledges **wihtout** requiring specific right in the JWT. (Consequently, it must be ensured that for admin users, such rights are also not created in the first place to not bloat the JWT).
  * In case a special role for a study program manager (like an admin, but access only to a subset of courses that belong to a study program) is required, this would have to be newly introduced. See [User Access Management](./Application-Architecture--User-Access-Management). With the JWT and the current approach, it appears to be feasible to introduce study program entities and handle authorization via study programs courses belong to, equivalently to the way that course access is handled at the moment.

