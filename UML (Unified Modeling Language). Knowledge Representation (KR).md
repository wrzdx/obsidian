## UML
**UML (Unified Modeling Language** – is a standard visual language used to model, design, and document software system.
- Provides a common language for developers, analysts, and designers 
- Helps visualize system structure and behavior 
- Improves communication and reduces ambiguity 
- Supports planning, analysis, and documentation
### UML Class Diagram
A UML Class Diagram is a *structural diagram* that shows: 
- Classes in a system 
- Their attributes and methods 
- The relationships between classes
It is used to model the static structure of an object-oriented system.

> [!note] 
> Class diagrams can also be used for data modeling.

![|600](Pasted%20image%2020260401073752.png)

### Relationships Between Classes

| Relationship                     | Description                                                                                                       | Notation                                 |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| **Association**                  | A general connection between two classes. Objects know about each other. <br>*Student — enrolls → Course*         | ![](Pasted%20image%2020260401073947.png) |
| **Inheritance (Specialization)** | A subclass inherits attributes and methods from a superclass.<br>*Car ⟶ Vehicle*                                  | ![](Pasted%20image%2020260401074021.png) |
| **Realization**                  | A class implements an interface. <br>*ArrayList ⟶ List*                                                           | ![](Pasted%20image%2020260401074053.png) |
| **Dependency**                   | A class temporarily uses another class (method parameter, local variable).<br>*OrderService → PaymentService*<br> | ![](Pasted%20image%2020260401074358.png) |
| **Aggregation**                  | Whole–part relationship where parts can exist independently.<br>*team and player*                                 | ![](Pasted%20image%2020260401074348.png) |
| **Inheritance (Generalization)** | Whole–part relationship where parts cannot exist without the whole. <br>*house and room*                          | ![](Pasted%20image%2020260401074338.png) |

### Cardinality
![](Pasted%20image%2020260401074438.png)

### UML Class Diagram vs ER Diagram

| Aspect            | UML Class Diagram                            | ER Diagram (ERD)                    |
| ----------------- | -------------------------------------------- | ----------------------------------- |
| **Purpose**       | Models software classes and object structure | Models data and database structure  |
| **Focus**         | Behavior + structure                         | Data and relationships only         |
| **Main elements** | Classes, attributes, methods                 | Entities, attributes, relationships |
| **Operations**    | Yes (methods)                                | No                                  |
| **Typical use**   | Software design (OO systems)                 | Database design                     |
## Knowledge Representation
- **Goal:** develop concepts for accurately modeling some domain of knowledge by creating an *ontology* that describes the concepts of the domain and how these concepts are interrelated.
- **Ontology:** a formal, explicit specification of the concepts in a domain and the relationships between them.
	- What exists in this domain?  
	- How are they related? 
	- What rules or constraints apply?

> [!example] University Ontology Example
> **Classes:**
> - Student
> - Course
> - Professor
> 
> **Relations:**
> - enrolledIn(Student, Course)
> - teaches(Professor, Course)
> 
> **Attributes:**
> - Student → hasID, name
> - Course → hasCredits
> 
> **Axioms:**
> - Every Course is taught by exactly one Professor
> - A Student cannot teach a Course

### KR vs Conceptual Modeling

| Aspect                   | Knowledge Representation (KR)                         | Conceptual Modeling (CM)                                            |
| ------------------------ | ----------------------------------------------------- | ------------------------------------------------------------------- |
| **Main goal**            | Represent knowledge so a machine can reason and infer | Represent a system/domain so humans can design databases & software |
| **Origin**               | Artificial Intelligence                               | Software Engineering & Databases                                    |
| **Focus**                | Meaning, logic, inference                             | Structure, data, system requirements                                |
| **Level of abstraction** | Very high (semantic & logical)                        | Medium (business/system view)                                       |
| **Typical models**       | Ontologies, semantic networks, frames, rules          | ER diagrams, UML class diagrams                                     |
| **World assumption**     | Open World                                            | Closed World                                                        |
| **Primary users**        | AI systems, knowledge engineers                       | System analysts, DB designers, developers                           |



