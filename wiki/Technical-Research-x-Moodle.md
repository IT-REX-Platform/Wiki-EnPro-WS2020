# Moodle

## Useful Links

[Moodle Developer Reference](https://docs.moodle.org/dev/Main_Page)

Basic Plugin Tutorial / Overview: https://docs.moodle.org/dev/Tutorial 

Core APIs Overview (mit Erklärung): https://docs.moodle.org/dev/Core_APIs 

## APIs

API layers: https://docs.moodle.org/dev/External_services_security 
* External server interface (SOAP, REST, RSS, etc.) 
* Public PHP api (need to verify all parameters and access control, ...) 
* Low level internal api (fast, basic param validation, no access control, strict rules) 

Web services api (SOAP): https://docs.moodle.org/dev/Web_services_API 
* https://docs.moodle.org/dev/External_functions_API 
* Helper Plugin bauen und notwendige Daten darüber per Service zur Verfügung stellen 
* Basic example: Gruppe in Moodle-Kurs erstellen: https://docs.moodle.org/dev/Adding_a_web_service_to_a_plugin 

## Hierarchien extrahieren 

### Nutzer 
Auth: https://docs.moodle.org/dev/Authentication_plugins 

### Privilegien
https://docs.moodle.org/dev/Access_API 

When implementing access control always ask "Does the user have capability to do something?". It is incorrect to ask "Does the user have a role somewhere?".  
* Roles: https://docs.moodle.org/dev/Roles 
* Example capability: moodle/course:managegroups
  * e.g. create groups into moodle course 
  * `function has_capability($capability, context $context, $user = null, $doanything = true) `

### Kurse 
Navigation / Hierarchie: https://docs.moodle.org/dev/Navigation_API 

Grafische Übersicht Tree: https://docs.moodle.org/dev/images_dev/9/9c/Moodle-IA.png 

### Membership: 
Enrolment api: https://docs.moodle.org/dev/Enrolment_API 

Nutzer für Kurse: 
* `function is_enrolled(context $context, $user = null, $withcapability = '', $onlyactive = false) `
* `function get_enrolled_users(context $context, $withcapability = '', $groupid = 0, $userfields = 'u.*', $orderby = '', $limitfrom = 0, $limitnum = 0) `

Enrolled users may fully participate in a course. Active user enrolment allows user to enter course. Only enrolled users may be group members. Grades are stored only for enrolled users. 

## Inhalte extrahieren 
Verfügbarkeit: https://docs.moodle.org/dev/Availability_conditions 
* Dozenten können Inhalte beschränkt verfügbar machen 
* API zum checken 

Videos 

Vorlesungsfolien, etc. 

Daten einfügen 
* Custom fields in Nutzerprofile: https://docs.moodle.org/dev/User_profile_fields 

Im Zweifelsfall bleibt die Data Manipulation API (high level abstraction für RDBMSes): https://docs.moodle.org/dev/Data_manipulation_API 
* Queries schreiben 
