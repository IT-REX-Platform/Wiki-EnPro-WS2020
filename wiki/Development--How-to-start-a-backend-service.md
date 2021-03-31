# How to start a backend service

Add the following to your "/etc/hosts" file.

```
127.0.0.1   keycloak
127.0.0.1   jhipster-registry
127.0.0.1   minio
```

There are two flavors to choose from: **Full deployment** in Docker, where all services will run inside Docker containers, or **Partial deployment** in Docker, where only a lightweight environment consisting of Keycloak, MinIO and the JHipster Registry are launched.
The former is likely to be the more interesting option if your aim is to develop frontend while the latter might be more appealing towards backend developers as it allows you to debug microservices by running them in IntelliJ instead.

## Steps

### 0. Clone the IT-Rex-dev bundle

> `$ git clone --recursive https://github.com/IT-REX-Platform/IT-Rex-dev`

### 1. **(Full deployment only)** Compile and load Docker images for all services into your local Docker daemon.  

Make sure your current working directory is the `IT-Rex-dev` root folder and execute:
> `$ ./build-all.sh`

This will automatically build and import the images into Docker.

### 2. Launch the backend

Open a shell and navigate to *Backend-Deploy/docker-compose/local*.

For **Full deployment**, run
> `$ ./launch-all.sh`  

For **Partial deployment**, run
> `$ ./launch-slim.sh`  

### 3. **(Partial deployment only)** Launch the remaining services outside of Docker

Launch your service(s) using IntelliJ or by executing
> `$ ./gradlew -Pdev bootRun`

in their respective root directories.

**Note:** You will *always* also have to launch the Gateway outside of Docker in addition to your service(s) of choice.
Trying to run one or more services on your host system while keeping the Gateway inside a Docker container will not work properly.

---

The backend should be up and running now.  
Congrats 😇

---

### 4. Shutdown IT-REX

To shut everything down, execute
> `$ ./stop-all.sh`  
