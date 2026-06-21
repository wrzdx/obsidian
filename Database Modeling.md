- **Data** – is a collection of *raw facts*, figures, numbers, words, or observations that can be processed, analyzed, and interpreted to gain meaningful insights and make decisions.

>[!abstract] DIKW Pyramid
>
| Level                                | Description                                                                                                                 | Example                                                                        |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **Wisdom**<br>knowledge insight      | understanding, integration, applied, reflected upon, actionable, accumulated, principles, patterns, decision-making process | I better stop the car!                                                         |
| **Knowledge**<br>information meaning | idea, learning, notion, concept, synthesized, compared, thought-out, discussed                                              | The traffic light I am driving towards has turned red                          |
| **Information**<br>data<br>context   | organized, structured, categorized, useful, condensed, calculated                                                           | South facing traffic light on corner of Pitt and George Streets has turned red |
| **Data**                             | individual facts, figures, signals, measurements                                                                            | Red, 192.234.235.245.678 v2.0                                                  |

## Database and Database Management System
- **Database** – a collection of related data.
- **Database Management System (DBMS)** – a computerized system that enables users to create and maintain a database.

| Aspect                                | File-Processing System                                                               | Database Management System                                                    |
| ------------------------------------- | ------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------- |
| **Data Redundancy and Inconsistency** | The same data may be duplicated in multiple files, leading to inconsistency          | Data is centralized and managed through normalization, ensuring consistency   |
| **Difficulty in Accessing Data**      | Data retrieval is difficult and inefficient; requires custom programs for each query | Easy and efficient data access using query languages like SQL                 |
| **Data Isolation**                    | Data is scattered across multiple files and formats, making it hard to integrate     | Data is stored in a single database, simplifying access and relationships     |
| **Concurrent Access**                 | Difficult to manage simultaneous access; may cause data conflicts or corruption      | Supports controlled concurrent access with locking and transaction management |
| **Security Issues**                   | Security enforcement is manual and limited                                           | Provides robust access control, authentication, and authorization mechanisms  |

### Requirements
- Structured data storage 
- Data manipulation capabilities 
- Querying support 
- Data integrity enforcement 
- Concurrency control 
- Security features 
- Backup and recovery mechanisms 
- Scalability

### Data Models
````col
```col-md
flexGrow=1
===
**Data Model**

- an *abstract model* that organizes data elements and standardizes how they relate to one another and to properties of the real-world entities.

Types:
- Relational model 
- Entity-relationship (ER) model 
- Object-based data model 
- Semi-structured data model
```
```col-md
flexGrow=1
===
**Database Model**

- a specific type of data model that defines the *logical structure of a database* and specifies how data is stored, organized, and manipulated.
```
````

### Data Abstraction
- is the process of hiding complex data structures and implementation details from users by providing simplified views of the data.

#### Data abstraction levels:
````col
```col-md
flexGrow=1
===
##### Conceptual Level
- Provides a broad, *abstract view* of the data – what entities exist and how they are related
- Represents data in a way that’s easy for users to understand
  
**Example:**
A Student entity is related to a Course entity through Enrollment.

**Output:** *ER Model*
```
```col-md
flexGrow=1
===
##### Logical Level
- Describes what data is stored in the database and how the data items are related
- Focuses on tables, columns, relationships, and constraints

**Example:**
There is a table Students with columns StudentID, Name, and CourseID

**Output:** *Database schema*
```
```col-md
flexGrow=1
===
##### Physical Level
- Describes how the data is actually stored in the system
- Includes details like file organization, indexes, data blocks, and access paths
  
**Example:**
Data is stored in B-tree indexes or linked blocks on a disk
```
````

### Database Development Process
![](Pasted%20image%2020260401044850.png)

| Stage                        | Actions                                                                                                                                                                                                    | Output                                                                                                                    |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Requirements Gathering**   | - Interview database users to understand the proposed system<br>- Identify and document data and functional requirements                                                                                   | - A document describing detailed user requirements                                                                        |
| **Data Analysis**            | - Describe data properties, relationships, and usage in detail <br>- Ensure the model fully reflects user requirements                                                                                     | - A conceptual data model representing a shared understanding between clients and developers<br>- Example: ER Diagram<br> |
| **Logical Database Design**  | - Decide on the type of database system (relational, object-oriented, network, etc.)<br>- Keep the design independent of any specific DBMS                                                                 | - A complete logical schema defining tables, relationships, and constraints                                               |
| **Implementation**           | - Build the database according to the logical schema<br>- Define storage structures, security rules, and external schemas<br>- Adapt implementation to the selected DBMS, tools, and operating environment | - A fully constructed, populated, and secure database system                                                              |
| **Testing**, **Maintenance** |                                                                                                                                                                                                            | - Released Schema and Database                                                                                            |
### Memory-Time Tradeoff
We can *reduce execution time* by storing precomputed results, at the cost of increased memory usage.

**Common techniques:**
- Caching: store results of expensive operations
- Lookup tables: precompute values instead of recalculating
- Indexing in databases: extra structures to speed up queries
- Memoization: store results of function calls

