<!-- omit in toc -->
# Setup with Ubuntu 20.04

- [General Things](#general-things)
  - [Keycloak](#keycloak)
  - [Install NodeJs / expo](#install-nodejs--expo)
  - [Visual Studio Code (Frontend)](#visual-studio-code-frontend)
  - [IntelliJ IDEA Ultimate (Backend)](#intellij-idea-ultimate-backend)
  - [Static code analysis](#static-code-analysis)

## Install openjdk 11

```
sudo apt install openjdk-11-jdk
```

```
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```

## Install Docker and Docker Compose

Install Docker:
https://docs.docker.com/engine/install/ubuntu/

Manage Docker as a non-root user:

```
sudo groupadd docker
```

```
sudo usermod -aG docker $USER
```

Install Docker-Compose:
https://docs.docker.com/compose/install/

# General Things

## Keycloak

We use keycloak as authentication provider.
To use keycloak in a Docker container, the host name keycloak must point to localhost.

Append `127.0.0.1 keycloak` to

- UNIX: `/etc/hosts`
- Windows: `%windir%\system32\drivers\etc\HOSTS`

## Install NodeJs / expo

Install nodejs from [NodeJS](https://nodejs.org/en/download/current/).
And the following packages:

- Install expo `npm install -g expo-cli`

Please also check [Environment-Setup](https://reactnative.dev/docs/environment-setup) for Android / iOS Development

## Visual Studio Code (Frontend)

- article with usefule extensions: https://x-team.com/blog/best-vscode-extensions/

## IntelliJ IDEA Ultimate (Backend)

- install intelliJ from here: https://www.jetbrains.com/de-de/idea/download/#section=linux
- Uni Stuttgart is providing you with the ultimate version
- For ubuntu add intelliJ to the launcher:
  - open intelliJ
  - click on Tools>Create Desktop Entries

## Static code analysis

[This](./Development--Quality-Assurance-and-Methods--Setup-dev-environment)