# How-To

Make sure you have configured your dev-environment. [Environment-Setup](Development--Environment-Setup.md)

## General

### Clone Repos

Clone the Frontend:

- git@github.com:IT-REX-Platform/MediaService.git

Create a new folder called `Backend`.
Clone the following repos into the `Backend` folder.

- `git@github.com:IT-REX-Platform/Gateway.git`
- `git@github.com:IT-REX-Platform/CourseService.git`
- `git@github.com:IT-REX-Platform/MediaService.git`

## Start Backend-Environment

- `docker-compose -f Gateway/src/main/docker/keycloak.yml up`
- `docker-compose -f Gateway/src/main/docker/jhipster-registry.yml up`

Open the folders Gateway and CourseService with IntelliJ IDEA, start coding ;)

## Frontend

Checkout `git@github.com:IT-REX-Platform/Frontend.git`

Go into the `Frontend`-Folder and run `npm install` to install all the necessary dependencies.
Whenever the file `package.json` has been changed, this command must be executed.
So when fetching/rebasing, pay attention to whether the file has been changed.

### Run the Frontend

Go into the `Frontend`-Folder and run:

```
npm run web
```
