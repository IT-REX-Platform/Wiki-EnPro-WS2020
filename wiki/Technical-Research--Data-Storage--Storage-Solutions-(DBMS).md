todo

- firebase
- (influxdb)

- (keycloak)

- rdbms
  - postgres (vorschlag, dass wir das benutzen)
  - mariadb
  - mysql
  
---

# Firebase
## Overview
A cross-plattform app developement environment. Includes services like User Authentification, hosting and data-storage. 

## Storage Options:
1. **Firebase Realtime DB:** Firebase's original, cloud hosted and **NoSQL** database for mobile apps that require synced states across clients in realtime. Data is stored as JSON and and all users connected to it receive live updates after every change.
2. **Cloud Firestore:** A cloud-hosted, **NoSQL** database that web apps can access directly via native SDKs. Data is stored in documents as key-value pairs. Like Firebase Realtime DB, it keeps your data in sync across client apps through realtime listeners and offers offline support for mobile and web so you can build responsive apps that work regardless of network latency or Internet connectivity
3. **Cloud Storage:** An oject storage service for storing files such as images, videos, and audio as well as other user-generated content that can be up- or downloaded directly from clients. If the network connection is poor, the client is able to retry the operation right where it left off, saving time and bandwidth.

**TODO:** Is it possible to connect an existing DB like e.g. MySQL to Firebase / model realational Data in Firebase? (On the first look the answer seems to be yes but this needs more research. Here is a first video: https://www.youtube.com/watch?v=sSDHdWrSqLY)
For a comparision btw. *Firebase Realtime DB* and  *Cloud Firestore*  see [Choosing a Firebase Data Storage](https://firebase.google.com/docs/firestore/rtdb-vs-firestore?hl=en).

For more information see the [Firebase Documentation](https://firebase.google.com/docs). 



# RDBMS

It is likely that we are going to use a relational database management system for storing and accessing lots of data. **MariaDB**, **MySQL** and **PostgreSQL** are three of the most popular open source solutions.  

Reasons in favor of Postgres:

- very little to no maintenance required
- clients have good backwards compatibility (as opposed to MariaDB)
- (almost) fool-proof replication
- good blob storage (MariaDB has been catching up lately)
- good performance, especially with big databases
