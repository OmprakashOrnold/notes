# ORM : Object Relational Mapping (Theory)                 
*  ORM says '**Perform Database Operations in Object Format**'.
  save(object), update(object),delete(object), get(id):object
  all operations are executed using objects (input/output). 
* We need to follow Mapping Rule.
*  class     -----mapped with -----   table
*  variable  -----mapped with -----   column
* then 
* object  <<---->>  Row   (No SQL query given by programmer).


### Database 
   Database  2 types  SQL Based(Oracle,MySQL..) , NoSQL Based(MongoDB, Redis, Casandra..etc)

* Spring Data supports performing database operations with both types of databases.  (SQL Based and NoSQLbased).
* For SQL based Database operations are done using JPA(Java Persistency API).

## What is the difference between below concepts?

* **JDBC**--- Perform Database operations using Java Database Connectivity API with SQL
* **ORM**--- Theory , that says do DB operations in Object format
* **JPA**-- Specification (Interfaces, Annotations,...) given by SunMicrosystem/Oracle
*   **Hibernate**-- Implementation of JPA.
*   **Spring JDBC**-- Perform Database operations using  JDBC + SQL with JdbcTemplate.
*   **Spring ORM** --- do DB operations using JPA with Hibernate using Template programming
*  But Configuration is required.
*  **Spring Data using Boot**:  do DB operations using JPA with any vendor(3rd party).
*  AutoConfiguration, Code Generated for basic operations.

**RAD - Rapid Application Development. (Less Lines of Code, faster coding).**

As of now, Any Database programming finally executing as JDBC(SQL) logic only,

   even any webapplication finally executed as Servlets concept only.


## ORM/JPA Properties
**dialect :** It is a class, that generates SQL query when we perform database operation.

* SQL queries are database dependent. So, do not use a direct SQL query in application
ie one SQL working fine with Oracle, may or may not work with SQLServer,MySQL..etc 
* Use Dialect in applications, that generates SQL  based on database.
* Few Dialects: Oracle10gDialect, MySQL8Dialect, ..etc

For every database one dialect class is provided by JPA/Vendors..
Link:
https://docs.jboss.org/hibernate/orm/5.2/javadocs/org/hibernate/dialect/package-summary.html

**show-sql :** It is boolean property. Do display/print generated SQL on console/log file
   provide its value as true, default is false.

 **hibernate-ddl.auto** :Tables/Sequences..etc DB Schema can be created manually by
   programmer or even ORM can create same. It has possible values

   
* **hibernate-ddl.auto = create**: Hibernate create new table every time. If old table exist then drop old table and create new table.

* **hibernate-ddl.auto = update** : Hibernate create new table if table not exist, else use same.

* **hibernate-ddl.auto = validate** : Hibernate does nothing, all schema design must be handled by programmer manually.
  
* **hibernate-ddl.auto = create-drop** : Hibernate create new table on application startup and drops same table when application is stopped.

