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
- 
```
```col-md
flexGrow=1
===

```
```col-md
flexGrow=1
===

```
````
