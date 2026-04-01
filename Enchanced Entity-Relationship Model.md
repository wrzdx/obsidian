**Enhanced Entity–Relationship (EER)** diagrams – an extended and more expressive version of traditional ER diagrams.

| ERD                                           | EERD                                            |
| --------------------------------------------- | ----------------------------------------------- |
| Models basic data structure and relationships | Models complex real-world semantics             |
| Strong and weak entities                      | Strong, weak, and subtype/supertype hierarchies |
| Inheritance not supported                     | Inheritance supported (ISA relationships)       |

### Concepts
![](Pasted%20image%2020260401055501.png)

#### Superclass and Subclass
- **Superclass:** A general entity that represents common properties and relationships.
  *Vehicle (Make, Model, Year)*
- **Subclass:** A specialized entity that extends a superclass and may add its own attributes or relationships.
  *Car and Truck are subclasses of Vehicle*
- **Inheritance:** Subclasses automatically inherit all attributes and relationships of the superclass.
  It ensures that subclasses reuse the attributes and relationships of the superclass.
#### Generalization and Specialization
- **Generalization:** A bottom-up process in which common attributes and relationships from multiple subclasses are combined into a single superclass.
  *Car, Truck, Motorcycle → Vehicle*
- **Specialization:** A top-down process in which a superclass is divided into more specific subclasses based on distinct attributes or relationships.
  *Vehicle → Car, Truck, Motorcycle*


#### Constraints
##### Disjoint vs Overlapping
````col
```col-md
flexGrow=1
===
**Disjoint *d***
Subclasses are *mutually exclusive*. An entity can belong to only one subclass.

*A Vehicle can be either a Car or a Truck, but not both.*
![](Pasted%20image%2020260401060132.png)
```
```col-md
flexGrow=1
===
**Overlapping *o***
Subclasses *can overlap*. An entity may belong to multiple subclasses.

*A Part can be both a Manufactured Part and a Purchased Part at the same time.*
![](Pasted%20image%2020260401060145.png)
```
````

##### Total vs Partial Specialization
````col
```col-md
flexGrow=1
===
**Total Specialization =**
Every superclass entity must belong to *at least one subclass*. Shown with a double line.

*A Vehicle MUST be either a Car or a Truck.*
```
```col-md
flexGrow=1
===
**Partial Specialization -**
Some superclass entities *may not belong to any subclass*. Shown with a single line.

*Some Employees are neither Secretaries nor Technicians nor Engineers*
```
````
````col
```col-md
flexGrow=1
===
![](Pasted%20image%2020260401060535.png)
```
```col-md
flexGrow=1
===
![](Pasted%20image%2020260401060520.png)
```
````
#### Specialization Lattice
A specialization lattice is a hierarchy in which a subclass can have *more than one superclass*, allowing shared properties to be inherited from multiple parent entity types.

![|600](Pasted%20image%2020260401060803.png)

#### Union Type
A union (also called a category) is a subclass that is formed from the union of two or more superclasses that do not share the same primary key.

**Key Characteristics:**
- The category is a subset of the union of multiple entity types. 
- It represents a common role played by different entities. 
- It can inherit attributes and relationships from multiple parents.

>[!note] 
>A category member must exist in at least one of its superclasses.

