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

| Feature                        | Function                                         | Stored Procedure                                |
| ------------------------------ | ------------------------------------------------ | ----------------------------------------------- |
| **Definition**                 | A reusable database routine that returns a value | A routine that performs actions in the database |
| **Primary purpose**            | Calculations and data retrieval                  | Performing operations and managing transactions |
| **Execution**                  | SELECT function_name()                           | CALL procedure_name()                           |
| **Can be used inside queries** | Yes                                              | No                                              |
| **Can appear in SELECT list**  | Yes                                              | No                                              |
| **Must return value**          | Yes                                              | No                                              |
| **Can use COMMIT**             |                                                  | Yes                                             |
| **Can use ROLLBACK**           |                                                  | Y                                               |
| **Use Cases**                  |                                                  |                                                 |
