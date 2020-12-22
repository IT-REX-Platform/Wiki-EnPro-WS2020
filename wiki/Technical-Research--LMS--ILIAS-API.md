# General Information

For researching purposes, our [vServer](vServer) is hosting an instance of ILIAS for the devs to experiment on.
This instance can be found at [http://129.69.217.173:8082/](http://129.69.217.173:8082/) from within the University network (use VPN!).

# Platform Account Credentials

There are two points of entry for the ILIAS platform.

## Admin Interface

The admin interface can be accessed via [http://129.69.217.173:8082/ilias/setup/setup.php](http://129.69.217.173:8082/ilias/setup/setup.php) and will lead to an admin interface.

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
| :--- | :--- | :--- |
| Administator | Role for systemadministrators. This role grants access to everything! | Global |
| Anonymous | Default role for anonymous users (with no account) | Global |
| Guest | Role grants only a few visible & read permissions. | Global |
| User | Standard role for registered users. Grants read access to most objects. | Global |

Roles can be modified when logged in as an administrator and using the navigation for **Administration > Roles**.

# ILIAS REST API

ILIAS does not provide a REST API out of the box. To make an API available anyway, we're using a custom fork of the RESTPlugin for ILIAS found at [https://github.com/IT-REX-Platform/Ilias.RESTPlugin](https://github.com/IT-REX-Platform/Ilias.RESTPlugin). It makes REST routes available and provides a OAuth2 way of authenticating the user. The custom fork is necessary, because it fixes issues with the original plugin which have not been dealt with yet.

## Mandatory preliminary setup

When using a fresh and newly installed ILIAS instance, login as an administrator and install the RESTPlugin.

1. Login as an administrator (see: [user interface logins](#user-interface) for reference)
2. Access the plugin management page under **Administration > Plugins** using the dropdown navigation.
3. If the plugin is not already listed, install the plugin by cloning it from GitHub first. This will not be necessary in the near future™.
   1. Login to the server instance and access the ILIAS docker container.
   2. Make a directory inside the ILIAS instance for plugins: `mkdir -p /var/www/html/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook`
   3. Move into that directory: `cd /var/www/html/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook`
   4. Clone the RESTPlugin into its own folder: `git clone https://github.com/IT-REX-Platform/Ilias.RESTPlugin.git REST`
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

### Getting an OAuth2 token

In case an OAuth2 token is needed in use with some routes, the following route can be accessed with the given parameters:

```
curl -X POST http://129.69.217.173:8082/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/api.php/v2/oauth2/token -d "grant_type=password&api_key=<apikey>&username=<user>&password=<password>"
```

, where `<apikey>` is the API-key, `<user>` the username and `<password>` the password to request a token for. This returns a JSON response with the token, its expiration time and scope.

The token can then be used as a header in the format: `Header: Bearer <token>`, where `<token>` is the received OAuth2 token.

---

## Integration

This integration section is analogous to the integration section in the Moodle-API document. The issue [ITREX-234](https://it-rex.atlassian.net/browse/ITREX-234) is referenced for this task. The main information to gather is the following:

1. Retrieve meta information on a user's courses
2. Retrieve lecture recordings / videos from a course
3. Retrieve slide sets from a course
4. Check / retrieve course membership (i.e. which courses is a given user a member of / who are the members of a given course)

Furthermore, there are the following two low-priority tasks:

5. Retrieve course appointments / dates
6. Retrieve quizzes (content)

### 1. Retrieve meta information on a user's courses

#### Get all courses (from a user's view)

REST call: `http://129.69.217.173:8082/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/api.php/v1/courses`

This route will only return valid data if called with a OAuth2 token header (as specified in [the OAuth2 token section](#getting-an-oauth2-token)). This OAuth2 token decides which information will be shown.

Example response:

```json
{
  "courses": [
    [
      {
        "ref_id": "61",
        "title": "Example course",
        "description": "Example description.",
        "create_date": "2020-11-18 12:08:30",
        "type": "crs"
      }
    ]
  ]
}
```

The response is an object with a `courses`-key. This maps to an array with an array of course objects (presumably for categories?).

| Key | Value in response | Description |
| :-- | :--- | :--- |
| ref_id | "61" | The id in the ILIAS database the course has. |
| title | "Example course" | The course's name. |
| description | "Example description." | The course's description. |
| create_date | "2020-11-18 12:08:30" | The timestamp when this course has been created. Given as a datetime string. |
| type | "crs" | The type of the object returned, should be "crs" (for course) for all of them. |

#### Information about a specific course (from a user's view)

REST call: `http://129.69.217.173:8082/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/api.php/v1/courses/<id>`

, where `<id>` is the id of the course to get the info of.

For example: REST call: `http://129.69.217.173:8082/ilias/Customizing/global/plugins/Services/UIComponent/UserInterfaceHook/REST/api.php/v1/courses/61`

This route will only return valid data if called with a OAuth2 token header (as specified in [the OAuth2 token section](#getting-an-oauth2-token)). This OAuth2 token decides which information will be shown.

Example response:

```json
{
  "contents": [
    {
      "ref_id": "62",
      "type": "fold",
      "title": "Folder in example course",
      "description": "It's a folder!",
      "parent_ref_id": "61"
    }
  ],
  "info": {
    "ref_id": "61",
    "title": "Example course",
    "description": "Example description.",
    "create_date": "2020-11-18 12:08:30",
    "type": "crs"
  },
  "members": [
    "6"
  ]
}
```

The response is an object with a `contents`-key, which maps to an array of contents inside the course, an `info`-key, which has information about the course (see [the previous section](#get-all-courses-from-a-users-view)) and a `members`-key, which maps to an array of all user-ids inside this course.

Inside the `contents`-key:

| Key | Example value | Description |
| :-- | :--- | :--- |
| ref_id | "62" | The id in the ILIAS database the content-item has. |
| type | "fold" | The type of this content-item, here "fold" (for folder). |
| title | "Folder in example course" | The title of the content-item. |
| description | "It's a folder!" | The description of the content-item. |
| parent_ref_id | "61" | The id of the parent this content-item belongs to. |

### 2. Retrieve lecture recordings / videos from a course

Retrieving the lecure recordings or videos from a course currently seems like a non-trivial task.

The course-route(s) discussed in [section 1](#1-retrieve-meta-information-on-a-users-courses) list direct children of the course in their content-key given an id of the course in question, but no recursive children after that.

In the routes available by default in the RESTPlugin there is a `v1/files/:refid` route, which retrieves any files given a valid `refid` in the database. However, this is direct downloading only.

Another possible candidate for accessing objects (recursively) is the route `v1/ilias-app/objects/:refid` (or its equivalent `v2/ilias-app/objects/:refid`), where (according to the code) a recursive list of elements per object and its subobjects is created and returned.  
**However**: until now there is apparently no way to easily access those routes, even with an API-key which has the rights to access this route. The response will be a "Unknown route" error.  
The sourcecode for the `ilias-app`-route is located in [`ILIASAppRoutes.php`](https://github.com/IT-REX-Platform/Ilias.RESTPlugin/blob/be0f8eecd2393dd7c67e34070b6f12bf49a5f050/RESTController/extensions/ilias_app_v2/routes/ILIASAppRoutes.php#L32) and suggests getting a recursive listing of the details of any object by `ref-id` of the ILIAS database. Once this route is accessible - either by getting the route to work or making our own variation of this API route - another verification is needed that this works like intended. If it does, we can use this route for accessing any object and its children.

### 3. Retrieve slide sets from a course

As the procedure would likely be equivalent, see [section 2 for details](#2-retrieve-lecture-recordings--videos-from-a-course).

### 4. Check / retrieve course membership (i.e. which courses is a given user a member of / who are the members of a given course)

Checking course membership is possible in both ways.

As the example response in [section 1 for a specific course](#1-retrieve-meta-information-on-a-users-courses) shows, the course has a `members`-key, which holds the id of the users enrolled in this course.

On the other hand, a course using the generic request `v1/course` should only appear in the list if the user is actually a member of the course, thus this property is already given.


## Integration - Summary / Final Verdict

Integration with ILIAS is possible and should be done. Because we further abstract the connection to a learning management system, it should be easy to access the relevant data for that in ILIAS.

The problem is the data exchange. Downloading and uploading direct files is possible (see [section 2](#2-retrieve-lecture-recordings--videos-from-a-course)). The (recursive) access to items inside a course is not given by a trivial route. There are candidates which look promising given the code, but can't be accessed (and there is no documentation on why not).  
Once these routes could be made accessible, retrieving videos/recordings and slidesets should be relatively trivial.

The data model should all in all be compatible with the one used in IT-REX.

---

## API Calls documentation

The following table aims to track the REST routes that we might make use of later on.

This table assumes **only using a fresh instance of ILIAS** with added RESTPlugin to ensure maximum compatibility. The *Plugin* column is there in case we start using plugins and trying out their routes as well, depending on our needs for the API.

| Method | Route | Parameters | Result Structure | Description | Plugin |
| :--- | :--- | :--- | :--- | :--- | ---: |
| GET | `/v1/clients` | -- | An object with indices for keys and objects for values. | Returns the list of API clients in an indexed object. Provides information about API client capabilities. | -- |

