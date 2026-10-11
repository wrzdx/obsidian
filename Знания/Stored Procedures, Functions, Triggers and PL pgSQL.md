## Functions
Function in PostgreSQL is a reusable block of SQL logic that accepts parameters and returns a value. 

Functions are stored inside the database and can be called from: 
- SQL queries 
- applications 
- other functions

**Key characteristics**:
- Stored inside the database 
- Can receive input parameters 
- Must return a value 
- Can contain SQL and procedural logic

```sql
CREATE FUNCTION function_name(parameters)
RETURNS return_type
LANGUAGE plpgsql
AS $$
BEGIN
	-- logic
END;
$$;
```

```sql
SELECT square_number(5);
```

## Stored Procedures
Stored Procedure is a precompiled database routine stored inside the database that performs a sequence of SQL statements.

Stored procedures are stored *in the database schema*.

**Benefits**:
- Reusability of database logic 
- Improved performance (precompiled execution) 
- Enhanced security (restricted access to tables) 
- Reduced network traffic between application and database

```sql
CREATE PROCEDURE procedure_name(parameters)
LANGUAGE plpgsql
AS $$
BEGIN
	-- SQL statements
END;
$$;
```

```sql
CALL hello_world();
```

Use stored procedures when: 
- Complex database logic must be reused 
- Batch operations are required Multiple SQL operations must be executed atomically 
- Logic should be kept inside the database instead of the application

## Functions vs Stored Procedures

| Feature                        | Function                                                                          | Stored Procedure                                                                  |
| ------------------------------ | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| **Definition**                 | A reusable database routine that returns a value                                  | A routine that performs actions in the database                                   |
| **Primary purpose**            | Calculations and data retrieval                                                   | Performing operations and managing transactions                                   |
| **Execution**                  | SELECT function_name()                                                            | CALL procedure_name()                                                             |
| **Can be used inside queries** | Yes                                                                               | No                                                                                |
| **Can appear in SELECT list**  | Yes                                                                               | No                                                                                |
| **Must return value**          | Yes                                                                               | No                                                                                |
| **Can use COMMIT**             | No                                                                                | Yes                                                                               |
| **Can use ROLLBACK**           | No                                                                                | Yes                                                                               |
| **Use Cases**                  | calculations, derived values, reusable expressions, data retrieval inside queries | batch operations, data modification, administrative tasks, transaction management |
## Triggers
**Trigger** is a special database object that *automatically executes* a function when a *specific event occurs* on a table.

> Triggers are used to enforce rules or automate actions when data changes.

Common triggering events: 
- INSERT 
- UPDATE 
- DELETE

> [!example] Example situations
> - When an employee’s salary is updated, automatically store the old and new salary in a salary history table. 
> - When a row is deleted from a table, automatically save the deleted data in an archive table. 
> - After a new order is inserted, automatically decrease the product quantity in the inventory table.

### General Syntax
- **Trigger Function**: A function that contains the logic executed when the trigger fires. 
- **Trigger Definition**: Specifies when the trigger runs and which table it is attached to.

`````col
````col-md
flexGrow=1
===
**Trigger Function**
```sql
CREATE FUNCTION triger_function_name()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $$
BEGIN
	-- trigger logic
RETURN NEW;
END;
$$;
```
````
````col-md
flexGrow=1
===
**Trigger Definition**
```sql
CREATE TRIGGER trigger_name
{BEFORE | AFTER} {INSERT | UPDATE | DELETE}
ON table_name
[FOR EACH ROW | FOR EACH STATEMENT]
EXECUTE FUNCTION trigger_function_name();
```
````
`````

## PL / pgSQL
**PL/pgSQL** (Procedural Language / PostgreSQL) is PostgreSQL’s procedural extension of SQL.
- It allows developers to write procedural logic inside the database.

**Key Characteristics**:
- Extends SQL with procedural programming features 
- Used to create functions, procedures, and triggers 
- Executes directly inside PostgreSQL server 
- Supports variables, loops, and conditional statements

**When Use**:
- Perform complex operations inside the database 
- Reduce application–database communication 
- Improve performance and maintainability

**Conditional Statements:**
```sql
IF grade >= 90 THEN
	result := 'Excellent';
ELSIF grade >= 60 THEN
	result := 'Pass';
ELSE
	result := 'Fail';
END IF;
```

**While loop**:
```sql
WHILE counter <= 10 LOOP
	counter := counter + 1;
END LOOP;
```

**Loop**:
```sql
LOOP
	EXIT WHEN counter > 10;
	counter := counter + 1;
END LOOP;
```

**For loop**:
```sql
FOR i IN 1..10 LOOP
	RAISE NOTICE 'Value: %', i;
END LOOP;
```

