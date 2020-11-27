# General Information
For researching purposes, our [vServer](vServer) is hosting an instance of Moodle for the devs to experiment on.
This instance can be found at [http://129.69.217.173:8081/](http://129.69.217.173:8081/) from within the University network (use VPN!).

# Platform Account Credentials
The following common user accounts are available (more to follow):
| User ID | Account name | Password | Informal Role / Capacity |
| :--- | :--- | :--- | :--- |
| 2 | admin | password | Platform administrator (please don't mess up, there is no backup :P) |
| 3 | user | password | Generic student |
| 4 | usertwo | password | Generic student |

# Moodle API
As of the time of this edit, we're planning on using Moodle's REST API to retrieve relevant data from a linked Moodle platform.

### Mandatory preliminary setup
Most of the services and features of Moodle's API that we're going to use are ***not*** enabled by default on a fresh instance.
To prepare your instance for testing and potentially later on for integration with our IT-Rex platform, these configuration steps are necessary (edit and improve as required):

* Advanced Features
	* Enable 'Web services'
* Plugins -> Web Services
	* Enable 'REST' protocol
	* Create external service called "IT-Rex Integration", abbreviated "itrex"
		* Set 'Users' to 'All Users' for example, if all platform users should be allowed to make use of the service; otherwise set 'Authorized users only' and define users
		* Associate Web Service Functions (permitted API calls; see WIP table below)
			* e.g. core_enrol_get_users_courses
* Create platform Role "IT-Rex User"
	- Context: System
	- Capabilities (just an example; Web Service Functions will tell you which capabilities they require to work):
		- moodle/webservice:createtoken
		- webservices/rest:use

### Sample requests
---
**Generate a token** for user `user` with password `password` for use with external service `itrex`:
```
http://129.69.217.173:8081/login/token.php?username=user&password=password&service=itrex
```
---
**Sample REST request** using my service token `wstoken=903..e9` to retrieve a list of all courses via `wsfunction=core_enrol_get_users_courses` that a given user `userid=4` is enrolled in:
```
http://129.69.217.173:8081/webservice/rest/server.php?wstoken=903c8eabf7c64852901e80680bdd2de9&wsfunction=core_enrol_get_users_courses&userid=4
```

Note that `userid` denotes which user I am interested in receiving data about. This does not have to be *me*, i.e. the user the given token was generated for. In this instance, depending on the roles and capabilities of the user associated with the token, certain information might not be visible.

---

### Integration
As part of our efforts to integrate IT-Rex with Moodle, we agreed on coming up with solutions for common problems in e-learning using the Moodle API.
These solutions are meant to help facilitate better understanding of the Moodle API's strengths and weaknesses, and ultimately lead to a recommendation and a final decision on whether we are moving forward with the integration or going to have to shoot for alternatives instead.

As per issue [ITREX-235](https://it-rex.atlassian.net/browse/ITREX-235), the main tasks are as follows:

1. Retrieve meta information on a user's courses
2. Retrieve slide sets from a course
3. Retrieve lecture recordings / videos from a course
4. Check / retrieve course membership (i.e. which courses is a given user a member of / who are the members of a given course)

Furthermore, there are the following two low-priority tasks:

5. Retrieve course appointments / dates
6. Retrieve quizzes (content)

#### Proposed Solutions

**1. Retrieve meta information on a user's courses**

REST call: http://129.69.217.173:8081/webservice/rest/server.php?wstoken=9d03213a36ba2475cb90a557c1a10e0b&wsfunction=core_enrol_get_users_courses&userid=

REST call parameters:
| Parameters | Example value | Description |
| :--- | :--- | :--- |
| wstoken | 9d03213a36ba2475cb90a557c1a10e0b | The token belongs to the user, it defines which content is displayed. E.g. a request with wstoken of role "Generic student" doesn't show invisible content, but a request with wstoken of role "Platform administrator" does. |
| wsfunction | core_enrol_get_users_courses | Response is a list of courses where the user is enrolled. |
| userid | 2 | Determines which courses are shown in the response. |

Response keys:
| KEY | Example value | Description |
| :--- | :--- | :--- |
| id | 2 | Course ID. |
| displayname | Entwicklungsprojekt IT-REX | Course name. |
| enrolledusercount | 3 | Number of enrolled users in a course. |
| visible | 1 | This setting determines whether the course appears in the list of courses and whether students can access it. Always "1" for students, because invisible courses are always hidden for them, even if they are members. Can be "0" for teachers and managers. |
| summary | \&lt;p\&gt;course summary bla bla bla | Text with course summary. Affected by KEY summaryformat. |
| summaryformat | 1 | Summary formats: 1 = HTML, 0 = MOODLE, 2 = PLAIN or 4 = MARKDOWN. |
| format | weeks | Possible course formats are: weeks, topics, social, site. |
| lang | en | Course language. This value can be empty if course and website language are identical. |
| startdate | 1605225600 | This setting determines the start of the first week for a course in weekly format. It also determines the earliest date that logs of course activities are available for. If the course is reset and the course start date changed, all dates in the course will be moved in relation to the new start date. |
| enddate | 1608256800 | The course end date is used for determining whether a course should be included in a user's list of courses. When the end date is past, the course is no longer listed in the navigation and is listed as past in the course overview. The course end date may also be used by custom reports. Users can still enter the course after the end date; in other words the date does not restrict access. |

*Evaluation:* -todo-

**2. Retrieve slide sets from a course**

*Description:* -todo-

*Evaluation:* -todo-

**3. Retrieve lecture recordings / videos from a course**

*Description:*
Assuming the platform has been set up according to the subsection 'Mandatory preliminary setup' on this page, navigate to Plugins -> Web Services and edit the IT-Rex external service.
Under 'show more', enable file downloads.  
At this point, downloading or retrieving video files from Moodle is a 2-step-process. First, you fetch a general overview of a given course's contents using **core_course_get_contents**, then you extract your content's *fileurl* from the response. The result is an URL similar to this: [http://129.69.217.173:8081/webservice/pluginfile.php/42/mod_resource/content/2/cursed.mp4?forcedownload=1](http://129.69.217.173:8081/webservice/pluginfile.php/42/mod_resource/content/2/cursed.mp4?forcedownload=1).  
To be able to complete this request though, it is necessary to append one additional parameter–the user token. This is the same service token used as *wstoken* in other requests. In order for pluginfile.php to accept the token, the aforementioned *enable file downloads* setting has to be ticked for the associated service as otherwise the platform will return with a content access violation error.
The final request will thus become [http://129.69.217.173:8081/webservice/pluginfile.php/42/mod_resource/content/2/cursed.mp4?forcedownload=1&token=9d03213a36ba2475cb90a557c1a10e0b](http://129.69.217.173:8081/webservice/pluginfile.php/42/mod_resource/content/2/cursed.mp4?forcedownload=1&token=9d03213a36ba2475cb90a557c1a10e0b), which yields the requested file.
  
*Evaluation:* -todo-

**4. Check / retrieve course membership**

*Description:* -todo-

*Evaluation:* -todo-

#### Final verdict and reasoning
**Should we integrate with Moodle at all?:** -todo-  
**Is data exchange viable?:** -todo-  
**Is the data model compatible?:** -todo-  

---

### API Calls documentation (deferred)

**Editor's note:** Work on this has been abandoned as Moodle itself provides a very extensive and thorough documentation on its own API including sample responses [here](http://129.69.217.173:8081/admin/webservice/documentation.php).  
The small amount of useful information that has been accumulated here is retained solely for referencing purposes.

The following table aims to track interesting REST routes that we might make use of later on.
Moodle's official documentation on these can be found at [https://docs.moodle.org/dev/Web_service_API_functions](https://docs.moodle.org/dev/Web_service_API_functions).

| Web Service Function | Parameters | Required capabilities | Description |
| :--- | :--- | :--- | :--- |
| **core_enrol_get_users_courses** | userid | (?); Depending on userid, response yields varying levels of detail. | Returns a list of courses that a given user is enrolled in. |
| **core_course_get_contents** | courseid | (?) | Returns course content overview (incl. URLs for sub-content) |
| **core_course_get_courses** | (?) | (?) | Returns list of all courses (no parameter = all courses on platform?); check out **core_course_get_courses_by_field** to get results by certain criteria |
| core_course_get_course_module | cmid | (?) | Returns general information on specific course module (e.g. a quiz); not necessarily content! |
| core_course_get_module | id (= cmid) | (?) | Returns an html fragment representing the specified module; not exactly sure what this is good for |
| core_enrol_get_enrolled_users |  |  | to check -- potentially used to fetch user roles |
