# How to replicate our Moodle testing instance

1. ```git clone https://github.com/IT-REX-Platform/moodle-docker``` -> /srv/moodle-docker
2. ```git clone https://github.com/moodle/moodle``` -> /srv/moodle
3. ```mkdir /srv/moodle-db-pg```, make sure docker can write here
4. ```cd /srv/moodle-docker && ./launch.sh```
