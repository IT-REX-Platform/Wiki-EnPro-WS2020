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
A proprietary (close-source) cross-plattform app developement environment by Google (IOS, Android, Web). Firebase provides services like User Authentification, hosting and data-storage. There are two pricing plans available: A free - bur very limited - one, which is most certainly not sufficent for managing the IT-Rex data. The other one extends the free version. The limit for resource-/ service usage provided by the free plan remains free. After this is exhausted one pays per use on top. For further information see: https://firebase.google.com/pricing 

## Storage Options:
1. **Firebase Realtime DB:** Firebase's original, cloud hosted and **NoSQL** database for mobile apps that require synced states across clients in realtime. Data is stored as JSON and and all users connected to it receive live updates after every change.
2. **Cloud Firestore:** A cloud-hosted, **NoSQL** database that web apps can access directly via native SDKs. Data is stored in documents as key-value pairs. Like Firebase Realtime DB, it keeps your data in sync across client apps through realtime listeners and offers offline support for mobile and web so you can build responsive apps that work regardless of network latency or Internet connectivity
3. **Cloud Storage:** An object storage service for storing files such as images, videos, and audio as well as other user-generated content that can be up- or downloaded directly from clients. If the network connection is poor, the client is able to retry the operation right where it left off, saving time and bandwidth.

## REST-Interface
Firebase offers for both DB-solutions a REST-Interface where any Firebase-DB can be defined as an endpoint. It is possible to model relational data in Firebase, which is described in this [Video]https://www.youtube.com/watch?v=sSDHdWrSqLY). The video also explains, how to connect Firebase to a MySQL-DB via Cloud Functions.
The Interfaces are described in the [Firebase Documentation](https://firebase.google.com/docs). 


# RDBMS

It is likely that we are going to use a relational database management system for storing and accessing lots of data. **MariaDB**, **MySQL** and **PostgreSQL** are three of the most popular open source solutions.  

Reasons in favor of Postgres:

- very little to no maintenance required
- clients have good backwards compatibility (as opposed to MariaDB)
- (almost) fool-proof replication
- good blob storage (MariaDB has been catching up lately)
- good performance, especially with big databases
