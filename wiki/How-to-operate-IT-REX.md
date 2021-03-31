# How to operate IT-REX as an administrator or lecturer

This page aims to help you, as a platform administrator or lecturer looking to use IT-REX, to set up your own functioning instance.
The goal of this guide is to set up IT-REX with Docker.

| :warning: Attention! IT-REX in its current configuration is insecure and should therefore not be exposed to the internet! |
| --- |

---
<br/><br/>

## Prerequisites

- Working **Docker** and **Git** installations
- A few gigabytes of unused disk space for good measure
- Unoccupied **ports 8080**, **8085** and **9080** on your machine
- (*Optionally, if you wish to build from source:* a working build environment featuring Java 11 (openjdk) and gradle)

## Step 1: Obtain all the required files

Clone the deployment repository (recursively to fetch all the submodules).  
This contains the tools and Docker config required to launch all the different components and backend dependencies of IT-REX, as well as the source code of the platform itself.  
To do this, run the following command in your terminal:  
> `$ git clone --recursive https://github.com/IT-REX-Platform/IT-Rex-deployment`

This may take a while. You can speed up the process by appending a "`-j 8`" switch to run multiple concurrent jobs. Feel free to replace '8' with any number.  
Then, navigate into the project folder that you just retrieved:
> `$ cd IT-Rex-deployment`

## Step 2: (Re-)Configure hosts

You'll need to (re-)configure the host of Keycloak, the identity provider, for IT-REX' services to find it.
To do so, navigate into every service project folder (`CourseService`, `MediaService`, `QuizService`, `Gateway` and `JHipster-Registry`), and edit their respective `docker-compose.yml` file as follows:

Find the line that sets the environment variable named `SPRING_SECURITY_OAUTH2_CLIENT_PROVIDER_OIDC_ISSUER_URI` and replace the default IP address of the value it is being set to. This can either be a local IP of the host machine you're looking to host IT-REX on, or a public IP if the host is exposed to the internet (may require additional firewall setup; allow incoming TCP on ports 8080, 8085 and 9080).

(In the following, the IP address `192.168.0.2` is being used to represent your host machine. Use your own IP address in its place when making edits!)

**Example:**  
Change...  
`- "SPRING_SECURITY_OAUTH2_CLIENT_PROVIDER_OIDC_ISSUER_URI=http://129.69.217.173:9080/auth/realms/jhipster"`

...to...  
`- "SPRING_SECURITY_OAUTH2_CLIENT_PROVIDER_OIDC_ISSUER_URI=http://192.168.0.2:9080/auth/realms/jhipster"`

Make sure to only replace the IP address while leaving the rest of the line (i.e. the port, path, etc.) unmodified!

<br>

Next, navigate into `Frontend` and edit `app.config.ts`, replacing the default IP address for all endpoints in the `staging` profile following the same pattern:  
Change...
```
        staging: {
            apiUrl: "http://129.69.217.173:8080/",
            authEndpoint: "http://129.69.217.173:9080/auth/realms/jhipster/protocol/openid-connect/auth",
            authTokenEndpoint: "http://129.69.217.173:9080/auth/realms/jhipster/protocol/openid-connect/token",
            authTokenRevoke: "http://129.69.217.173:9080/auth/realms/jhipster/protocol/openid-connect/logout",
            frontendUrl: "http://129.69.217.173:8085/",
```
...to...
```
        staging: {
            apiUrl: "http://192.168.0.2:8080/",
            authEndpoint: "http://192.168.0.2:9080/auth/realms/jhipster/protocol/openid-connect/auth",
            authTokenEndpoint: "http://192.168.0.2:9080/auth/realms/jhipster/protocol/openid-connect/token",
            authTokenRevoke: "http://192.168.0.2:9080/auth/realms/jhipster/protocol/openid-connect/logout",
            frontendUrl: "http://192.168.0.2:8085/",
```

This concludes the necessary configuration editing.

## Optional Step 3: Build the platform from source

(**Recommended**: You can skip to step 4 if you wish to use the prebuilt Docker images instead.)

Make sure your current working directory is the `IT-Rex-deployment` root folder and execute:
> `$ ./build-all.sh`

This will automatically compile all binaries from source, package them up and load them into your local Docker installation using [jib](https://github.com/GoogleContainerTools/jib).  
This process may take some time to complete.

## Optional Step 4: Download and import the prebuilt Docker images

(If you have followed the procedure in step 3 and built your own Docker images, you can skip to step 5.)

Download the following service Docker images:

| Service | Download link |
| --- | --- |
| **Frontend** | [Release v1.0.0](https://github.com/IT-REX-Platform/Frontend/releases/tag/v1.0.0) |
| **Gateway** | [Release v1.0.0](https://github.com/IT-REX-Platform/Gateway/releases/tag/v1.0.0) |
| **Course Service** | [Release v1.0.0](https://github.com/IT-REX-Platform/CourseService/releases/tag/v1.0.0) |
| **Media Service** | [Release v1.0.0](https://github.com/IT-REX-Platform/MediaService/releases/tag/v1.0.0) |
| **Quiz Service** | [Release v1.0.0](https://github.com/IT-REX-Platform/QuizService/releases/tag/v1.0.0) |

Import the images into your Docker daemon one-by-one by executing the following command:
> `$ docker load -i {filename}`

## Step 5: Launch the platform

Run
> `$ ./launch-all.sh`

to launch the platform.

---

# Additional information

The Web Frontend will be listening on port 8085. 
The default platform accounts are:

| Username | Password | Platform Roles |
| --- | --- | --- |
| admin | admin | ITREX_Admins |
| lecturer | lecturer | ITREX_Lecturers |
| student | student | ITREX_Students |

Keycloak is responsible for user management, authentication and authorization.  
You can reach the web interface on port 9080 (or 9443 for HTTPS).  
Make sure to assign one of the three platform roles listed above to any new user you create in Keycloak by adding it to the Keycloak group with the same name.

The following two Keycloak meta accounts exist:

| Username | Password |
| --- | --- |
| jhipster_admin | admin |
| jhipster_user | user |

<br>

For more information, check out [user access management](https://github.com/IT-REX-Platform/Wiki/wiki/Application-Architecture--User-Access-Management).

It is strongly recommended that you change the passwords for all of these preexisting accounts for security reasons.

## Creating new accounts

- Open the Keycloak admin console (http://your-hostname-or-ip:9080/) and log in as user "admin"
- Click on "Users" under the "Manage" grouping on the lefthand side
- Click on "Add user" and enter a username as well as additional information
	- Under "Required User Actions", pick "Update Password", then click "save" to proceed to the freshly created account's settings page
- Switch to the "Groups" tab and assign one of the three platform roles (ITREX_*)
- Click on the credentials tab and set a new temporary password

Share these credentials with your user. On their first login, they will be prompted to update their password.


