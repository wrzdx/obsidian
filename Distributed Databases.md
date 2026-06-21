Modern organizations often store large amounts of data for analysis, reporting, and decision-making. Two common approaches are *data warehouses* and *data lakes*.

````col
```col-md
flexGrow=1
===
## Data Warehouse
Data warehouse stores structured, cleaned, and organized data prepared for reporting and business analysis.
- schema is usually defined before data is loaded
- optimized for SQL queries and dashboards
- suitable for historical reporting and decision support
```
```col-md
flexGrow=1
===
## Data Lake
Data lake stores large volumes of raw data in its original form, including structured, semi-structured, and unstructured data.
- schema is often applied when data is read
- supports flexible analytics, big data processing, and machine learning
- suitable for logs, sensor data, multimedia, and exploratory analysis
  
Data lake usually stores diverse raw data for future processing.
```
````

## Scalability
Database scaling is the process of enhancing a database's *ability to handle increased data volume and user load*, primarily through *vertical* scaling or *horizontal* scaling.

While vertical scaling is easier to implement, it has limitations, whereas horizontal scaling provides greater capacity, distributing data across multiple nodes to maintain performance.

````col
```col-md
flexGrow=1
===
**VERTICAL SCALING**
Scaling Up: upgrading to a larger server
```
```col-md
flexGrow=1
===
**HORIZONTAL SCALING (SHARDING)**
Scaling Out: Adding more machines
```
````

## Distributed Database
Distributed database is a collection of logically related data stored across multiple physical locations. These locations may be in different servers, cities, or even countries.

>[!note] 
>To end users, a distributed database should still appear as a single database system.

Management of distributed databases is performed by a Distributed Database Management System (DDBMS).

Why Use Distributed Databases?
- **Scalability** — easier to grow storage
- **Availability** — system can continue working even if one site fails
- **Performance** — data can be placed closer to users or applications
- **Reliability** — no complete dependence on one central machine
- **Local autonomy** — different sites may manage their own data locally

## Types of Distributed Databases
````col
```col-md
flexGrow=1
===
**Homogeneous distributed databases**
Homogeneous distributed databases are distributed database systems in which all participating sites use the same DBMS and usually the same data model.
- simpler coordination between nodes
- easier replication and synchronization
```
```col-md
flexGrow=1
===
**Heterogeneous distributed databases**
Heterogeneous distributed databases are distributed database systems in which different sites may use different DBMSs, schemas, or even data models.
- supports existing legacy systems
- allows organizational independence
```
````

## Distributed Databases Architecture
````col
```col-md
flexGrow=1
===
**Client-server architecture**
- One or more server nodes store and manage data
- Client nodes send requests for queries, updates, or transactions
- Servers perform most of the database processing
```
```col-md
flexGrow=1
===
**Peer-to-peer architecture**
- All nodes can act as both clients and servers.
- Each node may store data, process requests, and cooperate with other nodes
- There is no strict central coordinator in the pure form
```
````


## Query Processing in Distributed Databases
1) A user submits one global query
2) The DDBMS decomposes it into subqueries
3) Subqueries are sent to relevant sites
4) Partial results are combined into the final answer

>[!note] 
>The main challenge is to minimize communication cost across the network

## Advantages & Challenges
````col
```col-md
flexGrow=1
===
**Advantages**
- High availability
- Better scalability
- Improved local response times
- Fault tolerance
- Geographic distribution support
```
```col-md
flexGrow=1
===
**Challenges**
- Greater design complexity
- Network delays and communication overhead
- Difficult concurrency control
- More complex recovery after failures
- Maintaining consistency among replicas
- Security management across multiple locations
```
````

# CAP Theorem
CAP theorem (or Brewer's theorem) states that any distributed data store can provide at most two of the following three guarantees:
- *Consistency (C)* – every user sees the most recent valid data
- *Availability (A)* – every request receives a response, even if some nodes fail
- *Partition Tolerance (P)* – the system continues operating despite communication failures between nodes

>[!note] 
>When a network partition occurs, a distributed system must choose between consistency and availability.

# Other Databases
## HBase Data Model
Apache HBase is a distributed NoSQL database built for storing very large amounts of sparse data.

HBase stores data in tables, but these are not relational SQL tables. Its core data model is based on:
- *Row key* – unique identifier of a row
- *Column family* – a group of related columns stored together
- *Column qualifier* – specific column name inside a family
- *Cell* – intersection of row key and column, containing a value
- *Timestamp / versions* – each cell can keep multiple versions of data over time

## Cassandra
Apache Cassandra is an open-source distributed NoSQL database designed for high availability, fault tolerance, and horizontal scalability. It uses a partitioned wide-column storage model.

- uses a peer-to-peer architecture with no single master node
- data is distributed across multiple nodes
- supports replication for fault tolerance
- designed for linear scalability
- allows a trade-off between consistency and availability through configurable consistency levels

# NewSQL
NewSQL is a category of modern relational databases that aim *to combine the SQL model and ACID-style guarantees* of traditional relational systems *with the scalability and fault tolerance* associated with distributed systems.

- Google Spanner
- CockroachDB
- TiDB
- YugabyteDB

>[!note] 
>NewSQL databases are still focused on structured data.

