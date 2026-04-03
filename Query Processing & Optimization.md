**Query processing** is the set of activities involved in retrieving data from a database. 

It includes translating a high-level query written in SQL into a sequence of low-level operations that the database system can execute efficiently.

>[!summary] Main Goals
>- Correctly retrieve requested data 
>- Execute queries efficiently 
>- Minimize resource usage (CPU, memory, disk I/O)

## Steps
1) **Scanning:**
   The scanner identifies the query tokens (SQL keywords, attribute names, and
   relation names).
2) **Parsing**:
   The parser checks the query syntax to determine whether it is formulated according to the syntax rules of the query language.
3) **Validating**:
   The query is validated by checking that all attribute and relation names are valid and semantically meaningful names in the schema of the particular database.
4) **Internal representation of the query:**
   *Query tree*: A query tree is a tree representation of relational algebra operations. It shows execution order of operations, where leaves are representing base tables, where the root represents the final result of the query.
5) **Query optimization & execution plan**
   The DBMS creates an execution strategy or query plan for retrieving the results of the query from the database files.
6) **Query code generator & runtime database processor** 

## From SQL to Relational Algebra
**Extended Relational Algebra** is an extension of the basic relational algebra that introduces additional operations to support queries commonly used in SQL.

## External Sorting
Sorting is one of the primary algorithms used in query processing. 

We need soring when using: 
- ORDER BY 
- JOIN (merging) 
- DISTINCT

**External sorting** refers to sorting algorithms that are suitable *for large files* of records stored on disk that do not fit entirely in main memory.

## Query Optimization
### Indexes
Indexes in SQL are special database structures that *speed up data retrieval* by allowing quick access to records instead of scanning the entire table. 

They act like a lookup system and play an important role in improving query performance and database efficiency.

