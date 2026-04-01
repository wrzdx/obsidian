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

## Entity-Relationship Model
### Basic Concepts
````col
```col-md
flexGrow=1
===
![](Pasted%20image%2020260401045545.png)
**Entities**

- An entity represents a *thing* or *object* in the real world.
```
```col-md
flexGrow=1
===
![](Pasted%20image%2020260401045633.png)
**Attributes**

- Attributes represent the properties or characteristics of entities and relationships.
```
```col-md
flexGrow=1
===
![](Pasted%20image%2020260401045703.png)
**Relationships**

- Relationships define how entities are connected to each other and describe the associations between them.
```

````
![](Pasted%20image%2020260401045746.png)

### Attributes
| Attribute                      | Description                                                                                | Example                                  |
| ------------------------------ | ------------------------------------------------------------------------------------------ | ---------------------------------------- |
| **Simple (atomic) attributes** | attributes that cannot be broken down into smaller parts                                   | ![](Pasted%20image%2020260401050015.png) |
| **Composite attributes**       | attributes that can be divided into smaller subparts with their own meanings               | ![](Pasted%20image%2020260401050045.png) |
| **Stored attributes**          | attributes that are physically stored in the database rather than computed from other data | ![](Pasted%20image%2020260401050201.png) |
| **Derived attributes**         | attributes that can be derived or calculated from other attributes                         | ![](Pasted%20image%2020260401050217.png) |
| **Multivalued attributes**     | attributes that can hold multiple values for a single entity                               | ![](Pasted%20image%2020260401050253.png) |
| **Key attributes**             | one or more attributes that uniquely identify an entity                                    | ![](Pasted%20image%2020260401050318.png) |

### Entity Types vs Entity Sets
````col
```col-md
flexGrow=1
===
#### Entity Type
- Entity type describes a group of entities that have similar characteristics (the same attributes). 
- Each entity type in the database is described by its name and attributes.

**Example:**
A university has thousands of students who share the same attributes (student ID, name, date of birth), but each entity has its own specific values for those attributes.
```
```col-md
flexGrow=1
===
#### Entity Set
- Entity set is the collection of all entities of a particular entity type.
```
````

### Entity Keys
````col
```col-md
flexGrow=1
===
#### Superkey
- A superkey is *any set of attributes* that can uniquely identify an entity in an entity set. It may contain extra attributes that are not necessary for uniqueness.
```
```col-md
flexGrow=1
===
#### Candidate Key
- A candidate key is a *minimal superkey*. It uniquely identifies an entity and contains no unnecessary attributes.
```
```col-md
flexGrow=1
===
#### Primary Key
- A primary key is the *candidate key chosen* by the database designer to serve as the main identifier for the entity type. There may be several candidate keys, but only one primary key.

- **Composite Key** - is a primary key made up of two or more attributes.
```
````

````col
```col-md
flexGrow=1
===
> [!example] 
> `STUDENT(id, email, name)`
> **Superkeys:**
> {id}, {email}, {id, email}, {id, name}, {email, name}, {id, email, name}
```
```col-md
flexGrow=1
===
> [!example] 
> `STUDENT(id, email, name)`
> **Candidate keys:**
> {id}, {email}
```
```col-md
flexGrow=1
===
> [!example] 
> `STUDENT(id, email, name)`
> **Candidate keys:**
> {id}, {email}
```
````

### Relationships
- A relationship describes how two entity types are *connected* in a database.

#### Degree of Relationship
- the count of entity types involved in a relationship.

![|800](Pasted%20image%2020260401051439.png)

- **Ternary Relationship**: Involves three entity types simultaneously
- **N-ary Relationship:** involved more than three entity types simultaneously

The function that an entity plays in a relationship is called its **role**. 
Roles are normally explicit and not specified.

#### Cardinality
````col
```col-md
flexGrow=1
===
##### One-to-One (1:1)
Each passport belongs to one person; each person has one passport.
```
```col-md
flexGrow=1
===
##### One-to-Many (1:N)
One department has many employees, but each employee is employed in only one department.
```
```col-md
flexGrow=1
===
##### Many-to-Many (M:N)
Students enroll in many courses; courses have many students.
```
````
````col
```col-md
flexGrow=1
===
![](Pasted%20image%2020260401051639.png)
```
```col-md
flexGrow=1
===
![](Pasted%20image%2020260401051711.png)
```
```col-md
flexGrow=1
===
![](Pasted%20image%2020260401051724.png)
```
````

#### Participation
>[!note] Participation constraints 
>Participation constraints specify whether the existence of an entity depends on its being related to another entity via the relationship type. 
>
>*Scholarship cannot exist without being assigned to a student.*

````col
```col-md
flexGrow=1
===
##### Partial Participation
Entity may or may not participate in the relationship.

*A student may or may not have a scholarship.*
```
```col-md
flexGrow=1
===
##### Total Participation
Entity must participate in the relationship.

*Each scholarship must be assigned to a student.*
```
````
````col
```col-md
flexGrow=1
===
![](Pasted%20image%2020260401052312.png)

```
````

>[!important] 
>Participation constraints and cardinalities must be ENFORCED when implementing the database.

#### Strong vs Weak Entity Types
````col
```col-md
flexGrow=1
===

##### Strong entity types
- Entity types that *have a key attribute* are called strong entity types.

##### Weak entity types
- Entity types that *do not have key attributes* of their own are called weak entity types.

- Weak entities are identified with one of their attribute values in combination with another entity type (owner entity type).

>[!note] 
>- Weak entity type always has a total participation constraint with respect to its identifying relationship.

##### Weak Relationships
- A weak relationship is the identifying relationship that *links a weak entity type to its owner entity*. 

- It represents the dependency of the weak entity on the owner for its identification and existence.
```
```col-md
===
![](Pasted%20image%2020260401053021.png)

```
````

