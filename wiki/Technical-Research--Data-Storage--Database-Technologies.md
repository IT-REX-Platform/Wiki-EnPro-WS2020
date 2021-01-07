# Database Technologies

## Scaling

**noSQL-Databases** usually scale horizontally which means by simply adding more servers because they offer record-level atomicity.
Therefore making it the preferred choice for large and constantly evolving data sets.

**SQL-Databases** are usually vertically scalable by increasing / upgrading the hardware components. The concept of ACID makes it hard to scale them horizontally, although possible if you can split large tables based on ranges of values in a key field, e.g. time-value based on semester.

## mySQL

A mySQL-RDBMS will be used to store the **Course** Data.

The **Course** Database will store standardized, consistent and an overseeable amount of data making RDBMS an optimal choice.

mySQL will be used because the **User** Data will be received from ILIAS and ILIAS is currently using mySQL aswell.

Related Pages:
* [Course Structure Data Model](./Application-Architecture--Data-Model--Course)

## noSQL

The **Quiz**-, **RexDuel**- and **Content** Data will be stored in a mongoDB-noSQL-Database.

The **Quiz** Data will be of different attribute types based on different question types making it easier to fit into a document-based Database.

**RexDuel** Data will have exponentially increasing amounts of data scaling with increasing amount of users and consequentially the increasing amount of duels played.

**Content** Data will have metadata and pointers to the uploaded course content in the File Storage System.

Related Pages:
* [Quiz Data Model](./Application-Architecture--Data-Model--Quiz)
* [Content Data Model](./Application-Architecture--Data-Model--Content)
