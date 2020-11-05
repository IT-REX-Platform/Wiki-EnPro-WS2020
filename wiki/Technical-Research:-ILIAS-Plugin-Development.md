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

 

 