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
```sql 
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

## SQL Database Definition

`````col
````col-md
flexGrow=1
===
>[!abstract] CREATE SCHEMA
>The CREATE SCHEMA command is used to specify a new schema by assigning it a name and defining the user who is authorized to manage the objects created within it.

>[!abstract] CREATE TABLE
>The CREATE TABLE command is used to specify a new relation by giving it a name and spacifying its attributes and initial constraints.

````
````col-md
flexGrow=1
===
```sql
-- Create Catalog
CREATE DATABASE MY_DATABASE;

-- Create schema
CREATE SCHEMA COMPANY AUTHORIZATION admin_user;

-- Create table
CREATE TABLE COMPANY.EMPLOYEE (
	employee_id SERIAL PRIMARY KEY,
	first_name VARCHAR(100) NOT NULL,
	last_name VARCHAR(100) NOT NULL,
	hire_date DATE NOT NULL,
	salary NUMERIC(10, 2) CHECK (salary > 0)
);
```
````
`````

>[!note]- PRIMARY KEY
>```sql
>CREATE TABLE EMPLOYEE (
> 	id INT PRIMARY KEY,
> 	name TEXT
> );
>```
>```sql
>CREATE TABLE EMPLOYEE (
> 	id INT,
> 	name TEXT,
> 	PRIMARY KEY (id)
> );
>```
>```sql
>CREATE TABLE ENROLLMENTS ( 
>	student_id INT, 
>	course_id TEXT, 
>	CONSTRAINT pk_enrollments PRIMARY KEY 
>	(student_id, course_id) 
>);
>```
>```sql
>ALTER TABLE EMPLOYEE 
>ADD PRIMARY KEY (id);
>```

### Constraints on Attribute Values

| Constraint | Description                                          | Example                                                                                           |
| ---------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| NOT NULL   | attribute must contain a value                       | `{sql} full_name VARCHAR(80) NOT NULL`                                                            |
| UNIQUE     | attribute value must be distinct                     | `{sql} email VARCHAR(120) UNIQUE`                                                                 |
| DEFAULT    | assign automatic value when none is provided         | `{sql} quantity INT DEFAULT 1, `<br>`{sql unwrap} created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP` |
| CHECK      | enforce logical conditions on values                 | `{sql} price NUMERIC(10, 2) CHECK (price > 0),`<br>`{sql} stock INT CHECK (stock >= 0)`           |
| IN         | attribute value should match one of specified values | `{sql} grade VARCHAR(30) NOT NULL CHECK (role IN (1, 2, 3))`                                      |
| DOMAIN     | constraints - reusable type with rules               | `{sql} CREATE DOMAIN positive_int AS INT CHECK (VALUE > 0);`<br>`{sql} temperature positive_int`  |
### ALTER - Modifying Existing Tables

>[!note] Add new column
>```sql
>ALTER TABLE employee 
>ADD COLUMN email VARCHAR(120);
>```

>[!note] Add a constraint
>```sql
>ALTER TABLE employee 
>ADD CONSTRAINT emp_email_unique UNIQUE (email);
>```

>[!note] Rename a column
>```sql
>ALTER TABLE employee 
>RENAME COLUMN full_name TO name;
>```

>[!note] Modify column definition
>```sql
>ALTER TABLE employee 
>ALTER COLUMN email TYPE VARCHAR(200);
>```

>[!note] Delete a column
>```sql
>ALTER TABLE employee 
>DROP COLUMN email;
>```

>[!note] Add a foreign key
>```sql
>ALTER TABLE employee 
>ADD CONSTRAINT fk_emp_dept FOREIGN KEY (dept_id) REFERENCES department(dept_id) 
>ON DELETE CASCADE;
>```

