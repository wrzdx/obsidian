## Concurrency Control
**Concurrency**: multiple processes executing at the same time
**Concurrency control**: techniques to manage simultaneous transactions

>[!info] Sequential Execution
>- One process executes completely before another begins 
>- No overlap in execution 
>- Simple but inefficient for multiuser systems

>[!info] Interleaved Execution
>- Multiple processes share a single CPU 
>- Execution is divided into small time slices 
>- Processes appear to run simultaneously

>[!info] Parallel Execution
>- Multiple processes run at the same time 
>- Requires multiple CPUs or cores 
>- Provides true simultaneous execution and higher performance

**Why We Need Concurrency Control?**
- Race Condition

## Transactions
- A transaction is a sequence of operations treated as a single unit.
- All operations must succeed or none at all

>[!note] ACID
>- **Atomicity**:A transaction is executed completely or not at all. If any part fails, all changes are rolled back.
>- **Consistency**: A transaction must take the database from one valid state to another. All integrity constraints must be preserved.
>- **Isolation**: Concurrent transactions do not interfere with each other. Each transaction behaves as if it is executed alone.
>- **Durability**: Once a transaction is committed, its changes are permanent. They will survive system failures or crashes.

### Structure
- BEGIN / START TRANSACTION 
- One or more READ / WRITE operations 
- COMMIT (save changes) 
- ROLLBACK (undo changes if needed)

A transaction always ends with either COMMIT or ROLLBACK
A transaction goes through several states: 
- Active – executing operations 
- Partially Committed – last statement executed 
- Committed – successfully completed 
- Failed – error occurred 
- Aborted – rolled back

### Schedules of Transactions
Schedule is the order in which operations from multiple transactions are executed.

>[!note] Conflicting Operations
>Two operations in a schedule are said to conflict if they satisfy all three of the following conditions:
>1. They belong to different transactions.
>2. They access the same item.
>3. At least one of the operations is a write operation.

#### Types of Schedules Based on Recoverability
Once a transaction T is committed, it should never be necessary to roll back T. 
This ensures that the durability property is not violated. 

The schedules that theoretically meet this criterion are called *recoverable schedules*. 

A schedule where a committed transaction may have to be rolled back during recovery is called *nonrecoverable schedule* and hence should not be permitted by the DBMS.

>[!note] Recoverable Schedule
>A schedule S is recoverable if no transaction T in S commits until all transactions T’ that have written some item X that T reads have committed.


#### Types of Schedules Based on Serializability
**Serial Schedule**:
- Transactions are executed one after another, with no overlap.

**Non-Serial Schedule**:
- Operations of multiple transactions are interleaved.

>[!note] Conflict-Serializable Schedule
>A non-serial schedule that produces the same result as some serial schedule, based on the order of conflicting operations. 
>If conflicts are ordered correctly, the schedule is safe.

### PostgreSQL
By default, PostgreSQL runs in auto-commit mode: Each SQL statement is its own transaction that is commited automatically.

```sql
BEGIN;
// set of statements
[COMMIT | ROLLBACK];
```

>[!note] SAVEPOINT
>A SAVEPOINT in PostgreSQL is a mechanism that allows you to create intermediate checkpoints inside a transaction.
>Instead of rolling back the entire transaction when something goes wrong, you can roll back only to a specific point.
>```sql
>BEGIN; 
>
>UPDATE accounts SET balance = balance - 100 WHERE id = 1; 
>
>SAVEPOINT sp1; 
>
>UPDATE accounts 
>SET balance = balance + 100 
>WHERE id = 2; 
>
>ROLLBACK TO sp1; 
>
>COMMIT
>```

#### Isolation
Isolation defines how transactions interact with each other. It controls visibility of changes between concurrent transactions.

**Read Committed (Default)** 
- A transaction sees only committed data 
- Each query sees the latest committed version

**Repeatable Read**
- All queries see the same snapshot of data 
- Data does not change during the transaction

**Serializable**
- Highest isolation level 
- Execution behaves like transactions run one by one

```sql
BEGIN TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```
```
```