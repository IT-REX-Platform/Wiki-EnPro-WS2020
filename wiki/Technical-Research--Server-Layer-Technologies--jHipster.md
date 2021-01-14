# jHipster



## Why jHipster

## Install jHipster-generator

Preconditions:

- JDK 11 (OpenJDK or https://adoptopenjdk.net/)
- NodeJS LTS

```bash
npm install -g generator-jhipster
```

### Alternativ with Docker

```
docker container run --name jhpster_generator -v $(pwd):/home/jhipster/app -v ~/.m2:/home/jhipster/.m2 -p 8080:8080 -p 9000:9000 -p 3001:3001 -it --rm jhipster/jhipster:v6.10.5 bash
```

## JDL

Can be edited with [JDL-Studio](https://start.jhipster.tech/jdl-studio/) or [VS-Code](https://www.jhipster.tech/configuring-ide-visual-studio-code/)

Sample idl-File with first microservices and entities [it-rex](./resource/it-rex.jdl)

## Work with jHipster

### Keycloak

We use keycloak as authentication provider.
To use keycloak in a Docker container, the host name keycloak must point to localhost.

Append `127.0.0.1 keycloak` to
- UNIX: `/etc/hosts`
- Windows: `%windir%\system32\drivers\etc\HOSTS`

### Clone Repos

Create a new folder called `Backend`.
Clone the following repos into the `Backend` folder.

- git@github.com:IT-REX-Platform/Gateway.git
- git@github.com:IT-REX-Platform/CourseService.git

### Start services

Now start keycloak and the jHipster Registry
- `docker-compose -f Gateway/src/main/docker/keycloak.yml up`
- `docker-compose -f Gateway/src/main/docker/jhipster-registry.yml up`

Open the folders Gateway and CourseService with IntelliJ IDEA, start coding ;)


### Generate new microservice

Marcel Weller: I got lots of issues adding the Media service with the import-jdl command. It also lead to some changes in the already generated services. Integration into existing docker compose files was tedious.


### Generate Code from JDL-File

Create new Directory and execute command:

```shell
jhipster import-jdl my_file.jdl
```


### Generate Docker image in local Docker registry

Go in root directory if the project and issue

``` 
./gradlew -Pprod bootJar jibDockerBuild
```