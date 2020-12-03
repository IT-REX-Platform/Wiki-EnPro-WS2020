todo

- firebase
- (influxdb)

- (keycloak)

- rdbms
  - postgres (vorschlag, dass wir das benutzen)
  - mariadb
  - mysql
  
---

# RDBMS

It is likely that we are going to use a relational database management system for storing and accessing lots of data. **MariaDB**, **MySQL** and **PostgreSQL** are three of the most popular open source solutions.  

Reasons in favor of Postgres:
	- very little to no maintenance required
	- clients have good backwards compatibility (as opposed to MariaDB)
	- (almost) fool-proof replication
	- good blob storage (MariaDB has been catching up lately)
	- good performance, especially with big databases
