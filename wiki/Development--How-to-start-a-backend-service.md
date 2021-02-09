# How to start a backend service

Add the following to your "C:\Windows\System32\drivers\etc\hosts" or "/etc/hosts" file.

```
127.0.0.1   keycloak
127.0.0.1   jhipster-registry
127.0.0.1   minio
```

There are two flavors to choose from: **Full deployment** in Docker, where all services will run inside Docker containers, or **Partial deployment** in Docker, where only a lightweight environment consisting of Keycloak, MinIO and the JHipster Registry are launched.
The former is likely to be the more interesting option if your aim is to develop frontend while the latter might be more appealing towards backend developers as it allows you to debug microservices by running them in IntelliJ instead.

## Steps

### 0. Clone all Service repos (Gateway, CourseService, MediaService, ...) and the Backend-Deploy repo

`git clone [..]`

### 1. **(Full deployment only)** Compile and load Docker images for all services into your local Docker daemon.  

Navigate into each service's root directory and execute `./gradlew -Pdev jibDockerBuild`.  
This will automatically build and import the image into Docker.

### 2. Launch the backend

Open a shell and navigate to *Backend-Deploy/docker-compose/local*.

For **Full deployment**, run 
`./launch_all.sh`  
**or** `docker-compose up -d`  
(**or** `docker-compose -f launch_for_services_inside_docker.yml up -d` if the shell script and the symlink don't work for some reason).

For **Partial deployment**, run
`./launch_slim.sh`  
(**or** `docker-compose -f launch_for_services_outside_docker.yml up -d`).

### 3. **(Partial deployment only)** Launch the remaining services outside of Docker

Launch your service(s) using IntelliJ or by executing `./gradlew -Pdev bootRun` in their respective root directories.

**Note:** You will *always* also have to launch the Gateway outside of Docker in addition to your service(s) of choice.
Trying to run one or more services on your host system while keeping the Gateway inside a Docker container will not work properly.

---

The backend should be up and running now.  
Congrats 😇

---

### 4. Shutdown backend

`CTRL + C` in all terminal windows running local services.  
Then, execute `docker-compose down` in *Backend-Deploy/docker-compose/local*.
