## Relational Model
- represents the database as a collection of relations.

````col
```col-md
flexGrow=1
===
**Row (or Tuple)**: A single record in the table that represents one instance of an entity. For example, a row in the *Employee* table represents one employee.
```
```col-md
flexGrow=1
===
**Column (or Attribute)**: A named field that describes a property of the entity. For example, columns like *Name* and *Ssn* describe employee properties. All values in a column are of the same data type.
```
````
  ![](Pasted%20image%2020260401075734.png)

### Relation Schema vs Relation
````col
```col-md
flexGrow=1
===
**Relation Schema**
- A relation schema defines the structure of a relation.
  $$R(A_{1}, A_{2}, ..., A_{n})$$
*STUDENT(Ssn, Name, Phone, Address, Age, Gpa*
```
```col-md
flexGrow=1
===
**Relation (Relation State)**
- A relation (or relation state) is the current set of tuples that exist in a table for a given relation schema.
```
````

### Relational Model Constraints
1) **Model-Based Constraints (Implicit Constraints)**
   integrity rules that are automatically enforced by the data model itself, meaning they hold for every valid database instance without being explicitly declared by the designer
   *A relation cannot have duplicate tuples.*
2) **Schema-Based Constraints (Explicit Constraints)**
   integrity rules that are intentionally defined by the database designer to enforce applicationspecific or business rules that are not automatically guaranteed by the data mode
   *Email addresses must be unique*
   *Total credits of a student ≤ 240*
3) **Application-Based Constraints (Business Rules)**
   integrity rules that describe the real-world meaning and policies of the system but cannot be fully captured using the data model
   *A student may register for a course only if they have passed all prerequisites*

#### Schema-Based Constraints
- **Domain Constraints**: restricts the type, range, and format of values allowed in a column
  *Salary must be non-negative*
- **Key Constraints**: guarantees that a key value uniquely identifies a row
  *Primary key is the main unique identifier*
- **NULL Constraints**: specifies whether a column is allowed to be empty
- **Entity Integrity Constraint**: A primary key must be unique AND not NULL
- **Referential Integrity Constraint**: maintains correct relationships between tables by ensuring that a foreign key always refers to an existing primary key
  *Enrollment.StudentID = 105 → Student 105 exists*
### Foreign Key

````col
```col-md
flexGrow=1
===
- A foreign key is an attribute (or set of attributes) in one table that *refers to the primary key of another table*.
- Its purpose is not only to link tables, but also to *enforce referential integrity*.
- A foreign key may be part of a primary key (weak entities), but does not have to be.
```
```col-md
![](Pasted%20image%2020260401080751.png)
```
````

### Operations
- **Retrievals**: reading and querying data
- **Updates**: modifying the data
	- **Insert** - adds one or more new tuples (rows) to a relation 
	- **Delete** - removes existing tuples from a relation 
	- **Update** - modifies the values of one or more attributes in existing tuples

#### INSERT: Constraint Violations
- **Domain constraint violation**: An attribute value is outside its allowed domain
- **Entity integrity violation**: A primary key attribute of a tuple is NULL
- **Key constraint violation**: The primary key duplicates an existing key value
- **Referential integrity violation**: A foreign key refers to a tuple that does not exist

>[!info] Solution
>- **Reject insertion**: Rejects an attempt to insert an invalid tuple

#### DELETE: Constraint Violations
- **Referential integrity violation**: A tuple being deleted is referenced by other relations

>[!info] Solutions
>- **Reject deletion**: Prevent the tuple from being removed 
>- **Cascade deletion**: Automatically delete all referencing tuples (and any tuples that reference them, recursively) 
>- Update the foreign key attributes in referencing tuples to NULL or another valid value that references a different existing tuple

#### UPDATE: Constraint Violations
- **Key constraint violation**: The primary key duplicates an existing key value
- **Referential integrity violation**: A foreign key refers to a tuple that does not exist

>[!info] Solutions
>- **Reject update**: Prevent the modification from being applied 
>- **Modify foreign key values**: Modify foreign key values in referencing tuples setting them to NULL, or another valid value that references a different existing tuple

## Relational Algebra
- *Relational Algebra* is a formal query language for the relational data model. 
  It provides a set of mathematical operations for retrieving data stored in relations.
- A *relational algebra expression* is a sequence of relational algebra operations in which the order of operations matters.

>[!note] 
>- In Relational Algebra, each operation takes relations as input and produces a new relation as output.
>![](Pasted%20image%2020260401081641.png)

### Operations
````col
```col-md
flexGrow=1
===

```
````
``````col
`````col-md
flexGrow=2
textAlign=center
===
#### Basic Operations
````col
```col-md
##### Unary Operations
- Projection [ π ] 
- Selection [ σ ] 
- Rename [ ρ ]
```
```col-md
##### Binary Operations
- Union [ ∪ ] 
- Cartesian Product [ × ] 
- Set Difference / Minus [ - ]
```
````

`````
`````col-md
flexGrow=1
===
#### Derived Operations
- Join [ ⨝ ]
- Division [ ÷ ]
- Intersection [ ∩ ]
`````
``````

#### Projection \[ π \]
- Projection chooses which columns (attributes) to keep in a relation. In other words, it removes unwanted attributes.
$$\pi_{attributeList} (Relation)$$
**Properties**:
- Removes attributes 
- May remove duplicate rows 
- Keeps all tuples, unless duplicates are eliminated

![](Pasted%20image%2020260401083207.png)

#### Selection \[ σ \]
- Selection chooses which rows (tuples) to keep in a relation. It applies a condition to each tuple and keeps only those that satisfy it.
$$\sigma_{condition}(Relation)$$
**Properties**:
- Does not change the structure of the table 
- Only reduces the number of rows 
- Condition can use: = , < , > , AND, OR, NOT
![](Pasted%20image%2020260401083348.png)

#### Rename \[ ρ \]
- The rename operation changes the name of a relation, and/or the names of its attributes without changing any data.
$$\rho_{NewRelationName(Attr1,Attr2,...)}(OldRelation)$$
**Rename is essential when**:
- The same relation is used more than once in a query 
- Two relations have attributes with the same name 
- We want clearer attribute names in the result
![](Pasted%20image%2020260401083710.png)
