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