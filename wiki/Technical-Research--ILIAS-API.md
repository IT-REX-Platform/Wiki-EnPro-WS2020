# General Information

For researching purposes, our [vServer](vServer) is hosting an instance of ILIAS for the devs to experiment on.
This instance can be found at [http://129.69.217.173:8082/](http://129.69.217.173:8082/) from within the University network (use VPN!).

# Platform Account Credentials

There are two points of entry for the ILIAS platform.

## Admin Interface

The admin interface can be accessed via [http://129.69.217.173/ilias/setup/setup.php](http://129.69.217.173/ilias/setup/setup.php) and will lead to an admin interface.

The **client administrator login** can be done using a client-id and any administrator username/password. The client-id for our client will (for now only) be `itrex-client`. Therefore, an example login can be:

* **Client ID**: `itrex-client`
* **Username**: `root`
* **Password**: `homer`

A client administrator login will allow you to change settings regarding that specified client.

To access the global ILIAS settings, use the *login with master password* option and use the password `password`. This will open the global settings and allow adding clients, changing the system settings and resetting the password.

## User Interface

The available users to test for (when not modified yet) are:

| Login | Password | First Name | Last Name | Access (until) | Role |
| :--- | :--- | :--- | :--- | :--- | :--- |
| root | homer | root | user | Unlimited | Administrator |

Users can be modified when logged in as an administrator and using the navigation for **Administration > User Management**.

### Default Roles

The roles available on ILIAS by default are:

| Role Name | Description | Context |
| :--- | :--- | :--- | :--- |
| Administator | Role for systemadministrators. This role grants access to everything! | Global |
| Anonymous | Default role for anonymous users (with no account) | Global |
| Guest | Role grants only a few visible & read permissions. | Global |
| User | Standard role for registered users. Grants read access to most objects. | Global |

Roles can be modified when logged in as an administrator and using the navigation for **Administration > Roles**.

# ILIAS REST API

ILIAS does not provide a REST API out of the box. To make an API available anyway, we're using the RESTPlugin for ILIAS found at [https://github.com/hrz-unimr/Ilias.RESTPlugin](https://github.com/hrz-unimr/Ilias.RESTPlugin). It makes REST routes available and provides a OAuth2 way of authenticating the user.

## Mandatory preliminary setup

When using a fresh and newly installed ILIAS instance, login as an administrator and install the RESTPlugin.

1. Login as an administrator (see: [user interface logins](#user-interface) for reference)
2. Access the plugin management page under **Administration > Plugins** using the dropdown navigation.
3. If the plugin is not already listed, install the plugin by cloning it from GitHub first. This will not be necessary in the near future™.
   1. Login to the server instance and access the ILIAS docker container.
   2. Make a directory inside the ILIAS instance for plugins: `mkdir -p /var/www/html/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook`
   3. Move into that directory: `cd /var/www/html/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook`
   4. Clone the RESTPlugin into its own folder: `git clone https://github.com/hrz-unimr/Ilias.RESTPlugin.git REST`
4. Open the *Actions* dropdown. If there is no option to *Activate* the plugin, choose *Update*. Otherwise continue to step 5.
   * After the update is completed, continue with the next step.
5. Open the *Actions* dropdown and choose *Activate*.

After that, you can open the *Actions* dropdown again and choose *Configure* to change different options of the RESTPlugin, manage API-keys and try out the API as different users.

## Checkout Queries

The RESTPlugin allows for a simple way of testing routes with any user and checking its output given a method and parameters. This can be found under [http://129.69.217.173:8082/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/apps/checkout/index.php](http://129.69.217.173:8082/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/apps/checkout/index.php)

## API Keys

The RESTPlugin uses different REST clients identified by API keys to control who has access to the routes and is allowed to perform requests.

These API keys can be managed under [http://129.69.217.173:8082/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/apps/admin/index.php#/clientlist](http://129.69.217.173:8082/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/apps/admin/index.php#/clientlist).  
By default, only one API key is made available with rights to only a few chosen routes. It is adviced to create an "almighty" API key with rights to all routes for testing, if it is not already available.

`// TODO: Any API key can be linked to authorization via OAuth2. This has to be researched further though.`

## Sample requests

Every request to the API can be done using the base address:

```
http://129.69.217.173:8082/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/api.php
```

The route can be appended after the `api.php` file in the URL.

## API Calls documentation

The following table aims to track the REST routes that we might make use of later on.

This table assumes **only using a fresh instance of ILIAS** with added RESTPlugin to ensure maximum compatibility. The *Plugin* column is there in case we start using plugins and trying out their routes as well, depending on our needs for the API.

| Method | Route | Parameters | Result Structure | Description | Plugin |
| :--- | :--- | :--- | :--- | :--- | ---: |
| GET | `/v1/clients` | -- | An object with indices for keys and objects for values. | Returns the list of API clients in an indexed object. Provides information about API client capabilities. | -- |

