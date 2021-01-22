The ISTE has set us up with a vServer to run applications and services for development on.
It is currently equipped with 4 processing cores and 32GB of memory.  
For researching and development purposes we configured it to run docker hosting instances of Moodle and Ilias.

The server can be reached at `129.69.217.173` from within the University network (use VPN!).  
To connect through SSH, message Noel about setting up access (pubkey).  

The following services are currently running on the server:
| **URI** | **Description** |
| :--- | :--- |
| http://129.69.217.173:8081/ | Moodle testing instance |
| http://129.69.217.173:8082/ | Ilias testing instance |
| http://129.69.217.173:9080/ | Keycloak testing instance (HTTPS only) |
| http://129.69.217.173:8084/  | Jenkins Server | 
| http://129.69.217.173:8085/  | Apache HTTP Server for running our Frontend testwise |
| http://129.69.217.173:8086/  | InfluxDB (?) |
| http://129.69.217.173:8087/ | MinIO Dev instance for hosting videos |
| http://129.69.217.173:9001/  | SonarQube |
| http://129.69.217.173:3000/ | Grafana |

Files for running services are currently located at:
| **Path** | **Description** |
| :--- | :--- |
| /srv/moodle | Moodle codebase 
| /srv/moodle-docker | Docker-compose wrapper etc. for Moodle Docker containers |
| /srv/moodle-db | Mapped volume for Moodle MySQL database files |
| /srv/ilias-docker | Docker-compose and Dockerfile for Ilias |
| /srv/ilias-docker/resources | Docker helper scripts for Ilias |
| /srv/ilias-docker/shared/db | Mapped volume for Ilias MySQL database files |
| /srv/ilias-docker/shared/ilias_html | Mapped volume for Ilias codebase |
| /srv/ilias-docker/shared/ilias_data | Mapped volume for Ilias client/user data |
| /srv/keycloak | Docker-compose for Keycloak |
| /srv/keycloak/db_data | Mapped volume for Keycloak Postgres database files |
| /srv/keycloak/https/tls.* | Mapped certificate and key for TLS |
| /srv/minio | Docker-compose for MinIO dev instance |
| /srv/minio/data | Mapped volume for MinIO blob storage |
