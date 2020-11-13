# General Information
For researching purposes, our [vServer](vServer) is hosting an instance of Moodle for the devs to experiment on.
This instance can be found at [http://129.69.217.173:8081/](http://129.69.217.173:8081/) from within the University network (use VPN!).

# Platform Account Credentials
The following common user accounts are available (more to follow):
| Account name | Password | Informal Role / Capacity |
| :--- | :--- | :--- |
| admin | password | Platform administrator (please don't mess up, there is no backup :P) |
| user | password | Generic student |

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

### API Calls documentation
The following table aims to track interesting REST routes that we might make use of later on.

| Web Service Function | Parameters | Required capabilities | Description |
| :--- | :--- | :--- | :--- |
| core_enrol_get_users_courses | userid | (?); Depending on userid, response yields varying levels of detail. | Returns a list of courses that a given user is enrolled in. |
