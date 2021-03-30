# Bugs that could not be fixed so far

See also JIRA for open bug tickets: [IT-REX@Jira](https://it-rex.atlassian.net/jira/software/c/projects/ITREX/issues/ITREX-677?jql=project%20%3D%20%22ITREX%22%20AND%20type%20%3D%20%22Bug%22%20ORDER%20BY%20created%20DESC)

# Known Problems and Limitations that could not be improved yet

## Content Data Model Implementation

In the design phase, a baseline for the content data model was created in order to get an overview about the respective entities and their relationships, see: [Content Data Model](Application-Architecture--Data-Model--Content.md).

In the current implementation state, IT-REX supports only videos, no PDFs, audio files, etc. Additionally, as described in the [Implentation View](./Application-Architecture--Implementation-View.md#Document-Service), the service cut between the existing Media Service (handles videos) and a potential future Document Service is not fix. During the implemenation of the Media Service, the entire Content Data Model was implemented on entity-level. It demonstrates a potential solution for implementing the entire model in one service including inheritence, therefore this implementation was not removed from the code-base as a reference implementation. When decision about other media types is made, this implementation may be used, remove, or altered.

## Media Adapter

The definition of a Media Interface and implementation of an according adapter for OpenCast was started, but not finished during the project. See details here: [OpenCast in our Wiki](Technical-Research--Data-Storage--OpenCast.md#implementation-attempt).