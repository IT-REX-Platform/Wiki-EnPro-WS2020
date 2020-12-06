- sqli protection
- db user permissions (read only access for everyday queries)


# Potential attacks
- attacks on backups (e.g. growing data volumes)
- SQL / NoSQL injection attacks
- DoS / DDoS
- infrastructure (dbms restart)


# Secure database

## Secure Queries

A SQL injection attack consists of insertion or “injection” of a SQL query via the input data from the client to the application. A successful SQL injection exploit can read sensitive data from the database, modify database data (Insert/Update/Delete), execute administration operations on the database (such as shutdown the DBMS), recover the content of a given file present on the DBMS file system and in some cases issue commands to the operating system.

The main consequences are:

- **Confidentiality**: Since SQL databases generally hold sensitive data, loss of confidentiality is a frequent problem with SQL Injection vulnerabilities.
- **Authentication**: If poor SQL commands are used to check user names and passwords, it may be possible to connect to a system as another user with no previous knowledge of the password.
- **Authorization**: If authorization information is held in a SQL database, it may be possible to change this information through the successful exploitation of a SQL Injection vulnerability.
**Integrity**: Just as it may be possible to read sensitive information, it is also possible to make changes or even delete this information with a SQL Injection attack.

### Preventing SQL injection

- Option 1: Use Prepared Statements (with Parameterized Queries)
- Option 2: Use Stored Procedures
- Option 3: Whitelist Input Validation
- Option 4: Escaping all User supplied input

Prepared Statements are supported by ORM Frameworks such das Hibernate and Spring Data JPA or *plain* Java.

## Secure Configuration

- separate database server from web server
- run the dbms with a user which has restricted privileges (No root or system user)
- only allow connectiosn form whitelisted hosts
- only allow encrypted connections
- remove any default accounts and databases

## Secure communication

- in general: dont use built-in accounts such as root, sa or SYS
- minimize privileges assigned to every database account
    - e.g. only execute select, update and delete
    - restrict access to certain tables, columns
    - account should not be the owner of the database
    - if a account only need access to portions of a table, use views which limits the access
- don't assign DBA or admin type access to your application accounts
    
