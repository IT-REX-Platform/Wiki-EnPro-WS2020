# Authz Verification Flow

to do: something about stateless JWT stuff
* current state: centrally generated JWT, decentral enforcement
* considered alternatives (policy-based, central in gateway/BFF, ...) and argumentation

# Authorization

We have three system roles (Roles are typically assigned once and rarely changed):
* Admin
* Lecturer
* Student

And three course roles (Roles will be added and changed when using the IT-REX platform):
* Owner
* Manager
* Participant

(See all details: [User Data Model](Application-Architecture--Data-Model--User))

As different micorservices require this information for authorization, it should all be included in the JWT. Consequence: The information must be available in keycloak as issuer of the JWT. All roles (system and course level) will be implemented as roles in keycloak. The system-level roles are static: there will be only admin, lecturer and student. 

The course-level roles are dynamic: For each course, there will be the above mentioned three roles that can then be assigned to a user. The CourseService encapsulates all functionality for managing a course. Therefore, these roles must be created in keycloak when creating a course.

As all rights within an individual course depend on the course role of a user, a microserive must store the course ID of all entities and resources it stores in order to manage access in a decentral way. So for instance, the media service must store the course ID for any video it stores.

## Known Authorization Limitations

We do not have shared data between microservices. This may lead to limitations to enforcing access control if other properties than a course ID are relevant, e.g. the publication state of a content item.

Currently, there are no limitations implemented. Once implemented, they will be listed here including measures to mitigate the effect.

# Keycloak

Keycloak is used for implementing the User Access Management. Keycloak is also the issuer of the JWTs.
The keycloak instance in our CD environment is running at [https://129.69.217.173:9443/](https://129.69.217.173:9443/) (use VPN!).  
Admin credentials are username `admin` and password `admin`.

# External Identity Providers

**State of implementation:** not implemented

**State of research:** general feasibility check with keycloak and Uni Stuttgart SAML

Keycloak is capable of acting as a broker to external identity providers. This means: Users can access IT-REX with an existing account and still authenticate with keycloak as our UAM Solution. For this purpose, the external provders must be registered in our keycloak and we must register with the respective external provider.

**General Data Flow with external identity provider:** User authenticates with external provider, and if not already existant the user will be created in the keycloak database.


Keycloak can act as Identity Broker for: **SAMLv2.0, oAuthv2.0, OpenID Connect v1.0** (see [Documentation](https://www.keycloak.org/docs/latest/server_admin/index.html#_identity_broker))

**SAML/Shibboleth IDP of University of Stuttgart:** [SAML Config](https://idp.uni-stuttgart.de/idp/shibboleth). Feasibility was tested from a technical perspective: SAML Config can be read by keycloak. Organizational boundary: keycloak / IT-REX must be registered with the university SAML so it is allowed to use it.

ILIAS may offer oAuth. However, the maturity of the implementation is a little unclear (see [Blogpost](https://docu.ilias.de/goto_docu_wiki_wpage_3521_1357.html)). Also, see https://github.com/IT-REX-Platform/Wiki/wiki/Technical-Research--LMS--ILIAS-API#getting-an-oauth2-token for more information about the ILIAS API.

In keycloak, users may have additional roles/rights. For SAML (maybe for oAuth as well), it is possible to create "mappers" in keycloak: SAML attributes can be automatically mapped to roles in keycloak. 
