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
	- extremely fast lookup by key 
	- example use: caching, session storage
- **Document Databases:**
	- JSON/BSON-like documents 
	- nested and semi-structured data 
	- example use: user profiles, product catalogs
- **Wide-Column Stores:**
	- distributed tables with flexible columns 
	- optimized for huge write/read throughput 
	- example use: telemetry, event storage
- **Graph Databases:**
	- nodes, edges, properties 
	- optimized for relationship-heavy traversal 
	- example use: fraud detection, social graphs
#### Key–Value Stores
**Basic model:** unique key identifies an arbitrary value 

**Operations** are usually simple: 
- *PUT(key, value)* 
- *GET(key)* 
- *DELETE(key)* 

````col
```col-md
flexGrow=1
===

>[!success] Strength
>- very high performance 
>- simple partitioning by key
>- excellent for caching and transient state 

```
```col-md
flexGrow=1
===

>[!failure] Weaknesses 
>- poor support for complex queries 
>- no relationship modeling
>- querying by value fields is limited or impossible

```
````

>[!summary] 
> If access is almost always by primary identifier, key-value is often enough.
>

#### Document Databases
**Data model:** Data is stored as self-contained documents 

````col
```col-md
flexGrow=1
===

>[!success] Strength
>- natural mapping to application objects 
>- nested structures reduce joins
>- flexible evolution of fields 
>- indexing on document attributes

```
```col-md
flexGrow=1
===

>[!failure] Weaknesses 
>- duplication is common 
>- joins are often limited or less efficient than in RDBMS
>- poor design can create update anomalies

```
````

>[!summary] 
> Document databases often shift complexity from joins to applicationaware document design

#### Wide-Column Stores
**Data model:** row key, column families, sparse columns, distributed partitions 

- A wide-column store can be interpreted as a two-dimensional key–value store

````col
```col-md
flexGrow=1
===

>[!success] Strength
>- enormous write volumes 
>- append-heavy workloads 
>- predictable queries on partition key

```
```col-md
flexGrow=1
===

>[!failure] Weaknesses 
>- weak support for ad hoc joins
>- denormalization is expected
>- poor partition-key design causes hotspots

```
````

>[!summary] 
> In wide-column systems, schema is often query-driven rather than entity-driven



#### Graph Databases
**Data model:** 
- nodes = entities 
- edges = relationships 
- properties = attributes

````col
```col-md
flexGrow=1
===

>[!success] Strength
>- shortest path 
>- recommendation 
>- dependency networks
>- social connections 
>- fraud ring detection

```
```col-md
flexGrow=1
===

>[!failure] Weaknesses 
>- not ideal for simple tabular data
>- can be harder to scale horizontally
>- performance depends heavily on query type

```
````

