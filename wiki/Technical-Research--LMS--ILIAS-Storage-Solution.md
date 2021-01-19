# Viability for ILIAS as a Storage Solution

As we have a need for hosting storage either ourselves or use already existing CMS solutions for keeping our data in sync with the one used by the University/professors, the viability for ILIAS as a storage solution for data uploaded to IT-REX has to be evaluated.

A huge number of plugins are being shared at [the Extending ILIAS page](https://docu.ilias.de/goto_docu_dcl_3342_1.html) and also at [the plugins forum on the official ILIAS site](https://docu.ilias.de/goto_docu_frm_3474.html). These will be used as a basis for the evaluation.

## External to Internal Content (Management) Plugins

The following plugins all use the ILIAS platform to make external content accessible within it and integrating it into the native ILIAS experience.

### OpenCast Plugin (TIK)

The [OpenCast Plugin made by the TIK](https://github.com/TIK-NFL/ilias-oc-plugin) is most likely the one used at the university. It requires a [custom(?) version of OpenCast](https://github.com/TIK-NFL/opencast) for use with the plugin to be able to access the data.

This relates to the [ITREX-315 ticket for evaluation of OpenCast](https://it-rex.atlassian.net/browse/ITREX-315), this is the technical aspect of it.

It allows for uploading videos to ILIAS, which will then be uploaded as events to Opencast. It also supports editing the videos in a basic manner.

#### How it works

The plugin manually uses the database to create objects and write and read data from the database. Deletion of Opencast series will not lead to deletion of the ILIAS repository object. Similarly, deleting the ILIAS repository object will not remove the series from Opencast.

It uses [its own API to communicate with Opencast](https://github.com/TIK-NFL/ilias-oc-plugin/blob/master/classes/opencast/class.ilOpencastAPI.php). The corresponding counterpart for the API may have been added to the custom version of OpenCast used here. It also uses REST for communication.

Whether the plugin recognizes Opencast series created in Opencast itself is unknown, it doesn't seem like it catches these cases though. Maybe it can be configured when creating the Opencast repository object inside ILIAS, but the primary video upload should occur via ILIAS.

### OpenCast Plugin

The [OpenCast Plugin](https://github.com/studer-raimann/OpenCast) is an alternative to the TIK one, used to create and use OpenCast repository objects inside ILIAS for editing and viewing.

This relates to the [ITREX-315 ticket for evaluation of OpenCast](https://it-rex.atlassian.net/browse/ITREX-315), this is the technical aspect of it.

It allows the users to create OpenCast objects inside ILIAS, upload, schedule and edit events and watch and download uploaded videos with an integrated video player. This can be further looked at in [the feature wiki of the plugin](https://docu.ilias.de/goto_docu_wiki_wpage_4975_1357.html).

#### How it works

No detailed technical research has been done to check how exactly this plugin works.  
However, there is an extensive [configuration document with details for each available setting](https://github.com/studer-raimann/OpenCast/blob/master/doc/CONFIGURATION.md), which can give a good understanding on how it works.

It allows for creation and management of events and videos inside of ILIAS. It uses its own internal API, for which the [documentation can be found here](https://github.com/studer-raimann/OpenCast/blob/703f11ade24e8bcbd6be59f1185da3081e5b2951/classes/Service/README.md).  
The API seems to be the manager of where the information about the OpenCast objects are primarily stored. There is a difference between series and events. To quote:

> The SeriesAPI always handles both, the ILIAS object and the Opencast series and decides on it's own which data has to be changed where. However, the ILIAS reference ID is required as an identifier to find the objects and not the Opencast series ID, since multiple ILIAS objects can reference one Opencast series.

and

> Since no information about an event is stored in ILIAS (except for online/offline), the events do not have something like an ILIAS ID. Therefore, the identifier used for the following actions is the Opencast unique event identifier.
> All data is stored in Opencast, except for an online/offline flag.

More technical knowledge about OpenCast will be necessary to evaluate the structure correctly.

### External Content Plugin

The [External Content Plugin](https://docu.ilias.de/goto_docu_cat_3466.html) is a plugin which supports integrating external content as repository objects inside ILIAS.  
Quote from the page:

> It can be used for multiple purposes, like embedding a video from a video server or access an external site with the possibility to pass authentication.

This would allow us to keep ILIAS in sync with IT-REX when using external storage solutions such as MinIO.  
This can also be used for learning progress-related data, as it supports the LTI 1.1 feature set (see below).

#### How it works

The manual of the plugin is available to download at [https://docu.ilias.de/goto_docu_file_3470_download.html](https://docu.ilias.de/goto_docu_file_3470_download.html).  
The plugin allows definitions of custom types. It uses a [LTI 1.1 implementation](https://www.imsglobal.org/specs/ltiv1p1p1/implementation-guide). Therefore, a **learning progress** status can be added to any defined type, which also may be interesting for a custom type in which we keep track of watched video time, for example.

Defining a custom type involves creating an XML file according to the LTI standard, for example for defining the UI used by ILIAS to render the type when creating a custom page, additionally allowing usage of internal ILIAS variable available and usage of OAuth authentication for accessing the external content.  
The definition can also be a `link`, referencing external objects according to the type definition inside the XML.

## Internal to External Content (Management) Plugins

### REST Plugin

The [RESTPlugin](https://github.com/studer-raimann/Ilias.RESTPlugin) is the plugin for making a RESTful API available for use with external clients. It has been evaluated already [in its own wiki article about the ILIAS API](Technical-Research--LMS--ILIAS-API.md).

It is also a way to access internal ILIAS content via the use of an external client.

### How it works

The plugin uses OAuth and a RESTful API to communicate with the ILIAS server from the outside, giving the user access the only what they see.

The plugin also provides a way to create own routes, which (given the result of the other wiki article) would be the best solution for the IT-REX use case. Creating own routes leaves the complete ILIAS backend open for usage with the common access plugins have. This includes reading from and writing to the database and accessing and modifying information of any repository objects.

## Noteworthy Plugins

### Interactive Video Plugin

The [Interactive Video Plugin](https://github.com/DatabayAG/InteractiveVideo) is a plugin that allows creating a video objects and then interacting on that by leaving comments at the current time the video is at. These notes are then shared for each other viewer (or can be private, if wanted) while watching the video. The plugin can also be used by a tutor to add questions to a specified timestamp.  
This is similar to the **comment** feature IT-REX has proposed for its content.

#### How it works

The plugin allows an external video source via link (supported: YouTube, Vimeo, FAU Video Portal) or internal media object to be used as a source and then allows commenting/adding notes/adding questions to those videos.  
It uses internally unique ids for the objects created to keep track of its data in the database. It uses the ILIAS database for storing its information in its own table.

### VideoManager Plugin

The [VideoManager Plugin](https://github.com/studer-raimann/VideoManager) is a plugin which allows for easier management of videos on the ILIAS platform, such as organizing them in folders, searching and viewing videos and converting them into different formats (requires their [MediaConverter Plugin](https://github.com/studer-raimann/MediaConverter)). There is an extension for this to work inside page objects as well.

This is not a plugin for accessing the videos from an outside source, though it may be interesting to keep in mind for looking at how the videos are being managed inside of the plugin (id handling, file management, etc.). Further research is probably needed, this is just here as a possible candidate.

## Summary and Proposed Approach

The plugins described here offer a variety of choices for externalizing the content and being able to still access and (partly) manage it on the ILIAS platform.

The following are proposed approaches on how to utilize ILIAS as content storage for IT-REX:

1. **Adding custom route(s) to the RESTPlugin and combining it with the Opencast Plugin already present and used.**  
   As the [Opencast Plugin](#opencast-plugin-tik) will likely continue to be used at the University and the [RESTPlugin](#rest-plugin) will allow us to access content on the platform externally, adding custom route(s) to the RESTPlugin and combining this with the Opencast Plugin can be one possible approach to solve the problem. As the plugin also supports uploads to Opencast, it *should* be possible to use the functionality to enable uploading to Opencast using the RESTful API via IT-REX. This way, we can still keep an abstract adapter interface on the side of IT-REX for multiple LMSs and a modified version of the RESTPlugin can handle the server side, combined with the Opencast Plugin used by the University.
2. **Adding custom route(s) to the RESTPlugin, hosting videos externally using IT-REX and using the External Content Plugin for syncing to ILIAS.**  
   IT-REX videos are being uploaded and handled by the IT-REX side using MinIO. These external videos can then be integrated using the [External Content Plugin](#external-content-plugin) and be available in ILIAS as objects for lecturers to manage however needed. Combining this plugin with the [RESTPlugin](#rest-plugin) will allow the platform to send a request for creating an external content repository object using custom routes, therefore staying in sync when a video is uploaded to IT-REX.
3. **Adding custom route(s) to the RESTPlugin or using the default routes and using the default file management ILIAS has.**  
   Disregarding existing plugins other than the [RESTPlugin](#rest-plugin), the default file upload for media objects in ILIAS is not ideal, but can also be used to utilize the space on the ILIAS platform and having content in sync with the ILIAS platform (where it can be managed as needed) and only keeping references to that content on the IT-REX side. Using the RESTful API and e.g. the `files`-route, any content can be uploaded to the ILIAS platform. This can also be done using a custom route if needed to better refine how uploading should be handled.

The option of a custom plugin from scratch depends on the use case to be solved by it.  

The functionality which will possibly be used the most is accessing ILIAS and its data from within IT-REX. This is already a working solution using the [RESTPlugin](#rest-plugin) and therefore not in the need of a custom plugin. The RESTPlugin is already designed with being extendable in mind, and adding routes can easily be done by design. This then allows access to the internal ILIAS plugin API without having to develop the framework around it.

Any of the [external platform management plugins](#external-to-internal-content-management-plugins) above more than likely already cover the featureset needed, are well developed (, cannot be *not* used in one case) and can be used in junction with the RESTPlugin to allow accessing those plugins via IT-REX if needed.

In case there would be a use case for which developing a plugin is necessary, it could still be done and (hopefully easily) integrated into the RESTPlugin for accessing it from IT-REX.
