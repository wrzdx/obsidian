## RDBMS Limitations
### Scalability
Traditional RDBMS systems are mainly designed for *vertical scaling*.

- Vertical scaling has practical limits 
	- hardware becomes expensive 
	- there is always a maximum machine size
- Horizontal scaling across many servers is harder in RDBMS
	- distributed joins are expensive 
	- synchronization between nodes is complex 
	- sharding is often difficult to manage
- At very large scale, performance bottlenecks appear
	- write-heavy workloads 
	- globally distributed applications 
	- high-concurrency systems
### Rigid Schema and Limited Flexibility
RDBMS requires a predefined schema (tables, columns, types, keys, constraints). 
Semi-structured and nested data does not fit naturally into tables.

### Join Complexity
Complex joins may lead to *slower query execution* and *heavier memory and CPU usage*.

### RDBMS & Distributed Environments
Strong consistency is a strength of RDBMS, but it also makes large-scale distribution more difficult.

**In distributed settings, difficulties include:** 
- replication lag 
- conflict resolution 
- maintaining strong consistency across nodes

**Strict ACID guarantees are valuable, but can reduce:** 
- availability during failures 
- write throughput 
- geographic distribution efficiency

**Global applications often need:** 
- always-on service 
- low latency across regions 
- tolerance to network partitions

## NoSQL
NoSQL (non-relational) databases are designed for high-performance, flexible data models and horizontal scalability, handling large volumes of unstructured or rapidly changing data.

NoSQL is not a replacement for SQL in all cases; it is an alternative family of database models optimized for different trade-offs.

**Designed for workloads where:**
- schema changes frequently 
- data volume is very large 
- low-latency distributed access is required 
- rigid normalization is not ideal

**NoSQL systems prioritize:**
- horizontal scalability 
- replication 
- partition tolerance 
- flexible schema

### Categories
- **Key-Value Stores:** 
	- data as (key, value) 
	- extremely fast lookup by key example use: caching, session storage