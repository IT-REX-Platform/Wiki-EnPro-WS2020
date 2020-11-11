## ILIAS Software Development 

Übersicht: https://docu.ilias.de/goto_docu_cat_582.html

Development Guide: https://docu.ilias.de/goto_docu_cat_582.html

## Plugin-Entwicklung 

Abschnitt im Development Guide: https://docu.ilias.de/ilias.php?ref_id=42&obj_id=27029&cmd=layout&cmdClass=illmpresentationgui&cmdNode=ba&baseClass=ilLMPresentationGUI

Möglichkeit zur Definition von _Plugin Slots_ zum Ansprechen einer bestimmten Schnittstelle. Alle definierten Plugin Slots: "in the ILIAS administration under section "Modules, Services and Plugins"" (see. 26.2 General: Implementing Plugins) 

Ein Plugin besteht aus: 

- plugin.php: definiert alle Plugin Eigenschaften 
- Plugin Klasse: eine Implementierung der abstrakten Klasse des Plugin Slots (in classes/ mit namen il<plugin_name>Plugin) Alle Funktionalität sollte in weitere Klassen im selben Ordner unterteilt werden. 
- Datenbank-Update-Skript: ein Skript zum Anpassen der Datenbank für das Plugin (sql/dbupdate.php) 
- (optionale) Sprachdateien: für Lokalisierung (lang/ subdirectory mit Namen ilias_<lang_code>.lang) 
- (optionale) UI-Templates: zum Generieren der Oberfläche des Plugins (templates/ subdirectory) 

Plugin Base Generator: https://plgen.studer-raimann.ch/

## ILIAS SOAP API 

Dokumentation: https://docu.ilias.de/webservice/soap/server.php
- login / loginCAS / loginLDAP / loginStudipUser 
- logout 
- lookupUser / searchUsers (getUser) / importUsers (deleteUser) 
- addCourse / deleteCourse 
- assignCourseMember / excludeCourseMember / isAssignedToCourse 
- getCourseXML / updateCourse 
- addUserRoleEntry / deleteUserRoleEntry 
- getExerciseXML / addExercise / updateExercise 
- hasSCORMCertificate / getSCORMCompletionStatus 
- getCoursesForUser / getGroupsForUser 
- getLearningProgressChanges / deleteProgress / getProgressInfo 

// braucht ein bisschen mehr Research, sieht aber sehr umständlich zu verwenden aus – alles sind XML responses und man müsste nachprüfen, wie die genau aussehen; wahrscheinlich eher das schon vorhandene REST-Plugin verwenden (siehe unten) 

Beispiel für einen SOAP-Client: https://github.com/leifos-gmbh/ILIASSoapClient/blob/master/soapclient.php 

## Ein konkretes Plugin Beispiel 

Die fertige App; Fokus auf Offline-Verfügbarkeit von Inhalten: https://www.ilias-pegasus.de/ 
Deren Sourcecode: https://github.com/studer-raimann/ILIAS-Pegasus 
Deren Helperplugin: https://github.com/studer-raimann/PegasusHelper 

Funde daraus: 
- es gibt schon ein REST-API Plugin für ILIAS (if (!$ilPluginAdmin->isActive(IL_COMP_SERVICE, 'UIComponent', 'uihk', 'REST')) { wird abgefragt)
  - die originale Version: https://github.com/hrz-unimr/Ilias.RESTPlugin 
    - Beispiel für alle Endpunkte der API anhand einer anderen ILIAS-Instanz https://ilias.uni-marburg.de/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/api.php/v2/util/routes 
    - wird in Kombination mit OAuth2 verwendet werden müssen, für Access Control 
  - die auf das Plugin angepasste Version: https://github.com/studer-raimann/Ilias.RESTPlugin 
  - die Implementierung des REST-Clients in der App: https://github.com/studer-raimann/ILIAS-Pegasus/blob/29bbc8506da2b610c822e2e7995427566b039595/src/app/providers/ilias/ilias.rest.ts 

- die Modelle, die die App verwendet, werden manuell in der für die App angelegte Tabelle der Datenbank gespeichert (https://github.com/studer-raimann/ILIAS-Pegasus/blob/29bbc8506da2b610c822e2e7995427566b039595/src/app/models/active-record.ts; afaik, keine Verwendung von den angesprochenen Custom Objects (ich weiß noch nicht, wo die überhaupt sind)) 

## Misc 

- es gibt ein Repository mit schon vorbereiteten Dockerfiles zum schnellen Aufsetzen einer ILIAS Instanz: https://github.com/kekru/ilias-docker ist aber schon älter, vielleicht muss man das noch auf aktuellen Stand bringen 
  - davon gibt es auch eine Version von den Entwicklern der Pegasus App (https://github.com/studer-raimann/docker-ilias) 

## REST-Plugin API Endpunkte 

Nach Beispielquery eines aktiven ILIAS-Servers mit integriertem REST-Plugin. 

- REST-Plugin: https://github.com/hrz-unimr/Ilias.RESTPlugin 
- Beispielroutes: https://ilias.uni-marburg.de/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/api.php/v2/util/routes 

// TODO: Lokale, frische ILIAS-Instanz aufsetzen und Plugin selbst testen für native Routes vs eventuelle Plugins 

// TODO: Auf lokaler Instanz testen, welche Antworten kommen und wie sie aufgebaut sind 

| Typ    | Enpunkt                                                                    | Access-Typ (PER=Permission) |
|--------|----------------------------------------------------------------------------|-----------------------------|
| GET    | v1/admin/files/:id                                                         | ADMIN                       |
| POST   | v1/admin/files                                                             | ADMIN                       |
| GET    | v1/admin/describe/:id                                                      | ADMIN                       |
| GET    | v1/admin/desktop/overview                                                  | ADMIN                       |
| ...    | (mehr admin routes)                                                        | ...                         |
| GET    | v1/biblio/:ref_id                                                          | OAuth PER                   |
| GET    | v1/cal/events/:user_id                                                     | OAuth PER                   |
| GET    | v1/cal/icalurl/:user_id                                                    | OAuth PER                   |
| GET    | v1/cal/events                                                              | OAuth PER                   |
| GET    | v1/cal/icalurl                                                             | OAuth PER                   |
| GET    | v1/contacts                                                                | OAuth PER                   |
| POST   | v1/contacts/add                                                            | OAuth PER                   |
| DELETE | v1/contacts/:addr_id                                                       | OAuth PER                   |
| PUT    | v1/contacts/:addr_id                                                       | OAuth PER                   |
| GET    | v1/contacts/:user_id                                                       | ADMIN                       |
| GET    | v1/courses                                                                 | OAuth PER                   |
| GET    | v1/courses/:ref_id                                                         | OAuth PER                   |
| POST   | v1/courses                                                                 | OAuth PER                   |
| DELETE | v1/courses/:ref_id                                                         | OAuth PER                   |
| POST   | v1/courses/enroll                                                          | ADMIN                       |
| GET    | v1/courses/join/:ref_id                                                    | OAuth PER                   |
| GET    | v1/courses/leave/:ref_id                                                   | OAuth PER                   |
| GET    | v1/courses/export/create/:ref_id                                           | OAuth PER                   |
| GET    | v1/courses/export/download/:ref_id                                         | OAuth PER                   |
| GET    | v1/courses/export/list/:ref_id                                             | OAuth PER                   |
| GET    | v1/courses/searchCourse/:ref_id                                            | OAuth PER                   |
| GET    | v2/courses/course/:refid                                                   | OAuth PER                   |
| PUT    | v2/courses/course/:refid                                                   | OAuth PER                   |
| POST   | v2/courses/course                                                          | OAuth PER                   |
| DELETE | v2/courses/course/:refid                                                   | OAuth PER                   |
| GET    | v2/courses/participants/:refid                                             | OAuth PER                   |
| GET    | v2/courses/participants/:type/:refid                                       | OAuth PER                   |
| GET    | v2/courses/participant/:refid/:userid                                      | OAuth PER                   |
| GET    | v2/courses/participant/:type/:refid/:userid                                | OAuth PER                   |
| POST   | v2/courses/participant/:type/:refid/:userid                                | OAuth PER                   |
| DELETE | v2/courses/participant/:refid/:userid                                      | OAuth PER                   |
| GET    | v1/desktop/overview                                                        | OAuth PER                   |
| DELETE | v1/desktop/overview                                                        | OAuth PER                   |
| POST   | v1/desktop/overview                                                        | OAuth PER                   |
| GET    | v1/ebook                                                                   | OAuth TOKEN                 |
| ...    | (mehr ebook-Routes)                                                        | ...                         |
| GET    | v1/files/:id                                                               | OAuth PER                   |
| GET    | v1/groups                                                                  | OAuth PER                   |
| GET    | v1/groups/:ref_id                                                          | OAuth PER                   |
| GET    | v1/groups/join/:ref_id                                                     | OAuth PER                   |
| GET    | v1/groups/leave/:ref_id                                                    | OAuth PER                   |
| GET    | v1/ilias-app/desktop                                                       | OAuth TOKEN                 |
| ...    | (mehr ilias-app Routes <br>// TODO: sind die eingebaut oder ein Plugin?)   | ...                         |
| GET    | v1/learning-module/:refId                                                  | OAuth TOKEN                 |
| GET    | v1/learning/:ref_id                                                        | OAuth PER                   |
| GET    | v1/learning/objectives/:ref_id                                             | OAuth PER                   |
| GET    | v1/learning/objectives/:ref_id/:user_id                                    | OAuth PER                   |
| GET    | v1/learning/objectives/:ref_id/:user_id/:objective_id                      | OAuth PER                   |
| GET    | v1/learning/scos/:ref_id                                                   | OAuth PER                   |
| GET    | v1/learning/scos/:ref_id/:user_id                                          | OAuth PER                   |
| GET    | v1/learning/scos/:ref_id/:user_id/:sco_id                                  | OAuth PER                   |
| GET    | v1/learning/progress/:ref_id                                               | OAuth PER                   |
| GET    | v1/learning/progress/:ref_id/:user_id                                      | OAuth PER                   |
| GET    | v1/m/feedbackdrop                                                          | OAuth PER                   |
| ...    | (mehr m-Routes <br>// TODO: was genau ist der "m"-Teil der Route? Module?) | ...                         |
| GET    | v1/questionpools/getQuestions/:ref_id                                      | OAuth PER                   |
| GET    | v1/questionpools/getQuestionsWithAnswers/:ref_id                           | OAuth PER                   |
| GET    | v1/questionpools/getTextAnswers/:ref_id                                    | OAuth PER                   |
| GET    | v1/questionpools/getSingleChoiceAnswers/:ref_id                            | OAuth PER                   |
| GET    | v1/questionpools/getMultipleChoiceAnswers/:ref_id                          | OAuth PER                   |
| GET    | v1/tests/routesAccess                                                      | --                          |
| GET    | v1/tests/download/:ref_id                                                  | OAuth PER                   |
| GET    | v1/tests/:ref_id                                                           | OAuth PER                   |
| GET    | v1/tests/getQuestions/:ref_id                                              | OAuth PER                   |
| GET    | v1/tests/getQuestionsWithAnswers/:ref_id                                   | OAuth PER                   |
