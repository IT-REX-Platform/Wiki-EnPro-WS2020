# How to start a backend service

Add the following to your "C:\windows\System32\drivers\etc\hosts" or "/etc/hosts" file.

```
127.0.0.1   keycloak
127.0.0.1   jhipster-registry
```
And entries for the other services that are needed for the system to run.

```
127.0.0.1   NameOfTheServiceInTheDockerComposeDotYmlFile
```

Now go to the root of your project and from there to /src/main/docker/ and run 

```
docker-compose -f app.yml up -d 
```

Now start your service with IntelliJ.
Congrats😇