The ISTE has set us up with a vServer to run applications and services for development on.
It is currently equipped with 4 processing cores and 8GB of memory.  
For researching and development purposes we configured it to run docker hosting instances of Moodle and soon Ilias (WIP).

The server can be reached at `129.69.217.173` from within the University network (use VPN!).  
To connect through SSH, message Noel about setting up access (pubkey).  
Our shared Moodle instance is currently listening on port 8081 and can thus be accessed at [http://129.69.217.173:8081/](http://129.69.217.173:8081/).

Files for running services are currently located at:  
```
/srv/moodle              ; Moodle codebase
/srv/moodle-docker       ; Docker-compose wrapper etc. for Moodle Docker containers
/srv/moodle-db           ; Mapped volume for Moodle MySQL database files
```
