# Keycloak

We are currently evaluating Keycloak as a possible solution for User Access Management.
Our testing instance is running at [https://129.69.217.173:9443/](https://129.69.217.173:9443/) (use VPN!).  
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
