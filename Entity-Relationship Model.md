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

### ER Notations
````col
```col-md
flexGrow=1
===
#### Chen's Notation
![](Pasted%20image%2020260401051724.png)
```
```col-md
flexGrow=1
===
#### Crow's Foot Notation
![](Pasted%20image%2020260401053934.png)
```
````
#### Naming & Layout Conventions: Chen’s Notations

| Description                                                  | Example                                 |
| ------------------------------------------------------------ | --------------------------------------- |
| Use singular nouns to represent one instance of an entity.   | STUDENT, COURSE (not STUDENTS, COURSES) |
| Entity and relationship names are written in UPPERCASE.      | STUDENT, ENROLLS                        |
| Attribute names start with a capital letter.                 | StudentID, Name, Age                    |
| Use nouns for entity types and verbs for relationship types. | PERSON (noun), WORKS_FOR (verb)         |
| Attributes typically arise from descriptive nouns            | Salary, Address, Grade                  |
#### Associative Entity
- An entity used in a many-to-many relationship (represents an extra table).
- Each side from the associative entity to the original entities is 1:N.
![](Pasted%20image%2020260401054326.png)


