- SQL is a standardized language used to store, manage, and retrieve data in relational databases.

````col
```col-md
flexGrow=1
===
**Purposes**
- Specify syntax / semantics for data definition and manipulation
- Allow database to work across different SQLcompatible systems without needing major changes
- Provide standardized ways to represent data (tables, rows, columns)
- Allow the language to evolve and support new features without breaking existing systems
```
```col-md
flexGrow=1
===
**Benefits**
- Productivity 
- Application portability 
- Application longevity 
- Reduced dependence on a single vendor 
- Cross-system communication
```
````

## SQL Components
- **DDL - Data Definition Language**
  Defines the structure of the database (schemas, tables, indexes, constraints) 
  *CREATE, ALTER, DROP, TRUNCATE, RENAME*
- **DQL - Data Query Language**
  Retrieves data from the database 
  *SELECT*
- **DML - Data Manipulation Language**
  Commands used to insert, modify, and delete data stored within database tables
  *INSERT, UPDATE, DELETE, MERGE*
- **DCL - Data Control Language**
  Controls access (permissions and privileges)
  *GRANT, REVOKE*
- **TCL - Transaction Control Language**
  Controls transaction behavior
  *(commit, rollback, savepoint)*

## Catalog & Schema in SQL
`````col
````col-md
flexGrow=1
===
**Schema**
- A SQL schema is a *logical container* in a database that organizes and groups related objects such as tables, views, indexes, and functions.
```sql unwrap
CREATE SCHEMA COMPANY AUTHORIZATION 'admin_user';
```
*Creates a schema called COMPANY owned by the user with authorization identifier admin_user*
- A Not all users are authorized to create schemas and schemas elements. The privilege to create schemas, tables, and other constructs must be granted to the relevant user accounts by the system administrator.
````
````col-md
flexGrow=1
===
**Catalog**
- A SQL catalog is the container in a database system that holds one or more schemas.
````
`````


