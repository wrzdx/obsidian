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
- **ALTER TABLE** - change structure of an existing table
- ALTER TABLE modifies schema, not data.

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

### DROP - Removing Existing Tables
- **DROP TABLE** - permanently remove the table and all its data
- DROP TABLE cannot be undone (unless backups / transactions are used).

#### Drop Table
```sql
DROP TABLE employee;
```
#### Drop table and remove dependent objects
```sql
DROP TABLE department CASCADE;
```
#### Drop table if exists (safe version)
```sql
DROP TABLE IF EXISTS employee;
```
#### Drop table only if dependent objects do not exist
```sql
DROP TABLE department RESTRICT;
```

### TRUNCATE - Emptying a Table
- **TRUNCATE TABLE** - removes all rows from a table at once (without row-by-row deletion), keeping the table structure but emptying its data
- Truncate is faster than DELETE without WHERE.
```sql
TRUNCATE TABLE employee;
```

### RENAME - Renaming a Table
- **RENAME** - changes the name of a database without changing its data or structure
```sql
ALTER TABLE employee RENAME TO staff;
```
## DML - Data Manipulation Language
### INSERT - Inserting Data
**Insert one row:**
```sql
INSERT INTO employee (full_name, dept_id)
VALUES ('John Smith', 2);
```

**Insert multiple rows:**
```sql
INSERT INTO employee (full_name, dept_id)
VALUES ('Jane Johnson', 1),
       ('Mark Lee', 1);
```

**Insert from a query:**
```sql
INSERT INTO employee (full_name, dept_id)
SELECT name, dept_id
FROM candidates
WHERE approved = true;
```

**Get inserted rows back:**
```sql
INSERT INTO employee (full_name, dept_id)
VALUES ('John Doe', 3)
RETURNING emp_id, full_name;
```

>[!important] If you omit a NOT NULL column (without a DEFAULT), the insert fails.

### UPDATE - Updating Data
**Update with a condition:**
```sql
UPDATE employee
SET dept_id = 2
WHERE emp_id = 10;
```

**Update multiple columns:**
```sql
UPDATE employee
SET full_name = 'John A. Smith', dept_id = 4
WHERE emp_id = 10;
```

**Update based on another table:**
```sql
UPDATE employee e
SET dept_id = d.dept_id
FROM department d
WHERE e.dept_id IS NULL AND d.name = 'HR';
```

**Return updated rows:**
```sql
UPDATE employee
SET dept_id = 5
WHERE dept_id = 2
RETURNING emp_id, full_name, dept_id;
```

>[!important] Update without a condition is used ONLY if you truly want to update all rows.
### DELETE - Deleting Data
**Delete selected rows:**
```sql
DELETE FROM employee
WHERE emp_id = 10;
```
**Delete based on another table:**
```sql
DELETE FROM employee e
USING department d
WHERE e.dept_id = d.dept_id AND d.name = 'Old Dep.';
```
**Return deleted rows:**
```sql
DELETE FROM employee
WHERE dept_id = 3
RETURNING emp_id, full_name;
```

>[!important] Without WHERE, DELETE removes all rows.

### MERGE - Merging Data
- **MERGE** - used for “synchronizing” a target table with a source dataset
```sql
MERGE INTO employee AS t 
USING employee_updates AS s 
ON t.emp_id = s.emp_id 
WHEN MATCHED THEN 
	UPDATE SET full_name = s.full_name, dept_id = s.dept_id 
WHEN NOT MATCHED THEN 
	INSERT (full_name, dept_id) VALUES (s.full_name, s.dept_id);
```

>[!tip] You can also add WHEN MATCHED THEN DELETE to remove rows based on a condition.

### Referential Integrity
- Referential integrity is a constraint that ensures foreign key values in a dependent (child) table must match primary key values in a referenced (parent) table in 1:M relationships.
#### Delete
- **ON DELETE RESTRICT** – Rejects deletion if referenced rows exist
- **ON DELETE CASCADE** – When a parent row is deleted all related child rows are automatically deleted.
- **ON DELETE SET NULL** – When the parent row is deleted the child foreign key becomes NULL
- **ON DELETE SET DEFAULT** – When parent row is deleted child foreign key is set to its default value.

#### Update
- **ON UPDATE RESTRICT** – Rejects update if referenced rows exist
- **ON UPDATE CASCADE** – When the parent key is updated the child foreign key is automatically updated
- **ON UPDATE SET NULL** – When the parent key is updated the child foreign key becomes NULL
- **ON UPDATE SET DEFAULT** – When the parent key is updated the child foreign key is set to its default value

#### Insert
- When inserting a dependent (child) row, PostgreSQL checks the foreign key constraint. 
- If the referenced parent does not exist the INSERT is rejected.
- Foreign keys prevent insertion of child records that have no matching parent.

## DQL - Data Query Language
- **SELECT** is used to retrieve data from one or more tables without modifying the database. It returns a result set (virtual table) produced from stored data.
```sql
SELECT column_list
FROM table_name
[WHERE conditions]
[ORDER BY sort_columns]
[LIMIT n]
[OFFSET m];
```

### SELECT - Querying Data
Конечно, вот всё из картинки в таком же формате 👇

---

**Select specific columns:**

```sql
SELECT full_name, dept_id
FROM employee;
```

**Select all columns:**

```sql
SELECT *
FROM employee;
```

**Filtering rows:**

```sql
SELECT *
FROM employee
WHERE dept_id = 3;
```

**Sorting results:**

```sql
SELECT full_name, dept_id
FROM employee
ORDER BY dept_id ASC;
```

**Removing duplicates:**

```sql
SELECT DISTINCT dept_id
FROM employee;
```

**Limiting rows:**

```sql
SELECT *
FROM employee
LIMIT 5;
```

**Limiting rows with pagination:**

```sql
SELECT *
FROM employee
LIMIT 5 OFFSET 10;
```

**Column aliases:**

```sql
SELECT full_name AS name, dept_id AS department
FROM employee;
```
