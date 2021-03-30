# Preliminary

This page aims to provide an overview about the implementation progress that was already achieved in each individual feature. A high-level description of features is available in the [IT-REX Scope and Roadmap](IT-Rex-Scope-and-Roadmap.md). 

- [Preliminary](#preliminary)
- [High-level Progress Visualization](#high-level-progress-visualization)
- [Detailed Progress Description](#detailed-progress-description)
  - [Course Data Management :large_blue_circle:](#course-data-management-large_blue_circle)
  - [Course Content Publishing :large_blue_circle:](#course-content-publishing-large_blue_circle)
  - [User Access Management :large_blue_circle:](#user-access-management-large_blue_circle)
  - [Course Structuring :white_circle:](#course-structuring-white_circle)
  - [Study Progress :large_blue_circle:](#study-progress-large_blue_circle)
  - [Course Quizzes _large_blue_circle:](#course-quizzes-_large_blue_circle)
  - [Gamification: Quizzes :black_circle:](#gamification-quizzes-black_circle)
  - [Gamification: Progress Incentivization :black_circle:](#gamification-progress-incentivization-black_circle)
  - [Notifications :black_circle:](#notifications-black_circle)
  - [User Identity Integration :black_circle:](#user-identity-integration-black_circle)
  - [ILIAS Integration :black_circle:](#ilias-integration-black_circle)
  - [Social Media Interaction :black_circle:](#social-media-interaction-black_circle)
  - [Moodle Integration :black_circle:](#moodle-integration-black_circle)
  - [Mobile Offline Behaviour :black_circle:](#mobile-offline-behaviour-black_circle)
  - [Desktop Client Offline Behaviour :black_circle:](#desktop-client-offline-behaviour-black_circle)
- [Cross-cutting / non-feature Progress](#cross-cutting--non-feature-progress)
  - [Mobile Application](#mobile-application)
  - [Admin User Interface](#admin-user-interface)

# High-level Progress Visualization

| Symbol | Meaning |
| --- | --- |
| :black_circle: | No implementation: The implementation of this feature was not started yet. |
| :large_blue_circle: | Basic implementation: The basics of this feature are implemented, but there are still many things that can be added. |
| :white_circle: | Complete implementation: This feature is mainly or nearly completely implemented, with only few things to add. |

# Detailed Progress Description

Each feature description covers:
* Related Backlog Entries => Epics that contain the user stories representing this high-level feature.
* What has been implemented? => Description of the implemented functionality.
* What's left to do in the backlog? => Links to the Jira-Backlog and a short summary of the functionality left to be implemented.
* Anything foreseeable to do that's not in the backlog yet? => Overview about concepts and ideas that were established, but not yet represented in the backlog because they are still abstract/future thoughts.

## Course Data Management :large_blue_circle:
* Related Backlog Entries:
  * https://it-rex.atlassian.net/browse/ITREX-17
  * https://it-rex.atlassian.net/browse/ITREX-45
* What has been implemented?
  * Courses can be created and unpublished courses can be deleted.
  * Courses have a description and a term.
  * Users can join courses via their id.
* What's left to do in the backlog?
  * Published courses can be archived and deleted. 
  * Courses can be created based on templates or existing courses.
  * Course joining can be restricted by password or listed/unlisted courses and can be affected via invitation links or a public course list.
  * [Course settings depending on other features.]
* Anything foreseeable to do that's not in the backlog yet?
  * Nope :smiley:

## Course Content Publishing :large_blue_circle:
* Related Backlog Entries:
  * https://it-rex.atlassian.net/browse/ITREX-46
  * https://it-rex.atlassian.net/browse/ITREX-86
* What has been implemented?
  * Videos and Quizzes can be added to courses.
  * Videos can be accessed and watched.
  * Quizzes can be accessed and solved.
* What's left to do in the backlog?
  * Implement publishing and updating of contents.
  * Upload, Download PDFs or even view them in-app.
  * Chain content items (e.g., a video is only accessible after completing the video before) and enable autoplay.
* Anything foreseeable to do that's not in the backlog yet?
  * Nope :smiley:

## User Access Management :large_blue_circle:
* Related Backlog Entries
  * https://it-rex.atlassian.net/browse/ITREX-41
  * https://it-rex.atlassian.net/browse/ITREX-45
* What has been implemented?
  * Users can authenticate, and authentication is enforced to see any contents.
  * Users are students, lecturers or admins. In contrast to lecturers, student users cannot create courses.
  * All users can be participants, managers or owners of a course with specific rights which leads to certain priviledges within a course.
* What's left to do in the backlog?
  * Manage user roles of a course (e.g., make someone a course manager).
  * Implement either self-registering or usage of external identities for authentication.
* Anything foreseeable to do that's not in the backlog yet?
  * Related: Admin User Interface, specifically for the admin

## Course Structuring :white_circle:
* Related Backlog Entries
  * https://it-rex.atlassian.net/browse/ITREX-17
  * https://it-rex.atlassian.net/browse/ITREX-46
  * https://it-rex.atlassian.net/browse/ITREX-75
* What has been implemented?
  * A course can be structured by chapters, and chapters can be filled with contents.
  * A course has a timeline, and course contents can be scheduled within this timeline.
  * Course participants as well as managers or owners have distinct views to work with the course structure.
* What's left to do in the backlog?
  * Support custom timeline creation and scheduling of course contents and improve user friendlyness. 
* Anything foreseeable to do that's not in the backlog yet?
  * Nope :smiley:

## Study Progress :large_blue_circle:
* Related Backlog Entries
  * https://it-rex.atlassian.net/browse/ITREX-61
* What has been implemented?
  * User progress is tracked on course content level storing which content item was started or completed.
  * The last accessed content of a user is stored per course for quick access.
  * The progress of a user in a video is stored.
  * All progress is visualized for the user.
* What's left to do in the backlog?
  * Track the progress of quizzes, including marking them as completed only when a quiz is passed.
  * Visualize the study progress in comparison to the recommended course timeline for a course participant.
  * Visualize the student's study progress for a course owner or manager. 
* Anything foreseeable to do that's not in the backlog yet?
  * Nope :smiley:

## Course Quizzes _large_blue_circle:
* Related Backlog Entries
  * https://it-rex.atlassian.net/browse/ITREX-30
* What has been implemented?
  * Quizzes can be created and linked to the course structure.
  * Quizzes can be accessed and solved.
* What's left to do in the backlog?
  * Advanced quiz settings like fail/pass criteria, time limits, ...
  * Store user's quiz results.
* Anything foreseeable to do that's not in the backlog yet?
  * Graded quizzes for examination purposes
  * Question points or difficulty for different weight of individual questions.
  * Different answer types, see also [Quizzes](Quizzes.md)

## Gamification: Quizzes :black_circle:
* Related Backlog Entries
  * https://it-rex.atlassian.net/browse/ITREX-30
* What has been implemented?
  * Nothing yet.
* What's left to do in the backlog?
  * Use questions from Course Quizzes for Gamification Quizzes
  * Answer questions in Turbo Mode
* Anything foreseeable to do that's not in the backlog yet?
  * Alternative quiz modes like RexDuell, see [Quizzes](Quizzes.md) and [Gamification Ideas](Gamification--The-Story-of-IT-Rex.md).
  * Jokers, difficulty, scores

## Gamification: Progress Incentivization :black_circle:
* Related Backlog Entries
  * https://it-rex.atlassian.net/browse/ITREX-50
* What has been implemented?
  * Nothing yet.
* What's left to do in the backlog?
  * Store food to earn per content item.
  * Design an IT-REX icon per course indicating if it is hungry or not.
  * Visualize progess with IT-REX feeding state.
  * User ranking.
* Anything foreseeable to do that's not in the backlog yet?
  * See all Gamificaiton ideas in [The Story of IT-REX](Gamification--The-Story-of-IT-Rex.md) and [Ranking and Scoring](Gamification--Ranking-and-Scoring-System.md).


## Notifications :black_circle:
* Related Backlog Entries
  * https://it-rex.atlassian.net/browse/ITREX-59
  * https://it-rex.atlassian.net/browse/ITREX-84
* What has been implemented?
  * Nothing yet.
* What's left to do in the backlog?
  * Create an inbox for notifications.
  * Notify about quizzes, comments and course announcements.
* Anything foreseeable to do that's not in the backlog yet?
  * Define more notifyable events in the course, e.g., update of a content item.
  * Enable to (de)activate notifications for a certain course.
  * Enable to (de)activate certain kinds of notifications.

## User Identity Integration :black_circle:
* Related Backlog Entries
  * https://it-rex.atlassian.net/browse/ITREX-578
* What has been implemented?
  * Nothing yet.
* What's left to do in the backlog?
  * Register a third-party identity provider with IT-REX.
* Anything foreseeable to do that's not in the backlog yet?
  * Nope :smiley:

## ILIAS Integration :black_circle:
This feature was not closely considered for implementation yet, so no backlog entries are available at all. See [general thoughts on integrating external systems on application level](Application-Architecture--Implementation-View.md#application-level). Some technical research was done and documented:
* [ILIAS API](Technical-Research--LMS--ILIAS-API.md)
* [ILIAS Plugin Development](Technical-Research--LMS--ILIAS-Plugin-Development.md)
* [ILIAS as Storage Solution](Technical-Research--LMS--ILIAS-Storage-Solution.md)

## Social Media Interaction :black_circle:
* Related Backlog Entries
  * https://it-rex.atlassian.net/browse/ITREX-66
  * https://it-rex.atlassian.net/browse/ITREX-57
* What has been implemented?
  * Nothing yet.
* What's left to do in the backlog?
  * Publish and view course announcements.
  * Comment on course contents, respond to comments and watch comment threads.
* Anything foreseeable to do that's not in the backlog yet?
  * like/dislike functionality
  * watchlist/watch later functionality

## Moodle Integration :black_circle:
This feature was not closely considered for implementation yet, so no backlog entries are available at all. See [general thoughts on integrating external systems on application level](Application-Architecture--Implementation-View.md#application-level).
Some technical research was done and documented:
* [Moodle API](Technical-Research--LMS--Moodle-API.md)
* [Moodle Misc](Technical-Research--LMS--Moodle-Misc..md)
* [Moodle Setup](Technical-Research--LMS--Moodle-Setup.md)

## Mobile Offline Behaviour :black_circle:
This feature was not closely considered for implementation yet, so no backlog entries are available at all. 


## Desktop Client Offline Behaviour :black_circle:
This feature was not closely considered for implementation yet, so no backlog entries are available at all. Some technical research was done regarding client frameworks that allow creating desktop apps. See [Cross Platform Frameworks](Technical-Research--Cross-Platform-Framework.md) and subpages.

# Cross-cutting / non-feature Progress

Some remarks should be made about the implementation progress regarding parts of IT-REX that do not directly map to one single feature.

## Mobile Application

The Frontend is build with ReactNative. Expo is used to generate the web-archive, and may as well be used to create mobile apps for Android and iOS. This was also done in the beginning of the project, but in order to speed up the implementation progress, specific styling and testing on mobile platforms was ommitted. Consequently, this would have to be done in order to make the frontend ready for mobile apps. See also[Cross Platform Frameworks](Technical-Research--Cross-Platform-Framework.md) and subpages.

## Admin User Interface

While an admin user was considered from the very beginning, no specific functionality and user interface was created for the admin user. See [User Access Management](Application-Architecture--User-Access-Management.md) for more information. Specific admin functionality may be that an admin can access a list of all courses, contents, etc and can modify, delete, ... anything that's in the applicatoin. A specific user interface for such application administration topics may be useful in the far future. Additionally, it might mnight make sense to add a system admin section that includes links to the JHipster Registry etc in order to provide an easy entry into the system for a system admin.