# jHipster



## Why jHipster

## Install jHipster-generator

Preconditions:

- JDK 11 (OpenJDK or https://adoptopenjdk.net/)
- NodeJS LTS

```bash
npm install -g generator-jhipster
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



### Generate Code from JDL-File

Create new Directory and execute command:

```shell
jhipster import-jdl my_file.jdl
```