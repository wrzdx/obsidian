
>[!summary] Informal Design Guidelines for Relational DB 
>- Each tuple in a relation should represent one entity or relationship instance
>- Relations should be designed such that their tuples will have as few NULL values as possible
>- The lossless join property ensures that JOIN operations produce meaningful and accurate results

**Database normalization** is a process of organizing attributes and relations to: 
- Reduce redundancy 
- Eliminate anomalies 
- Improve data integrity 

Database normalization is based on functional dependencies and keys.

## Functional Dependencies
A functional dependency X → Y holds if whenever two tuples have the same value for X, they must also have the same value for Y. In other words, X uniquely determines Y.

The constraint must hold for every relation instance r(R). 

The functional dependency must be true for all possible valid states of the table, not just the current data.

If K is a key of R, then K functionally determines all attributes in R.

>[!quote] Короче
>Если сущность одна, она не может отличаться от самого себя во всех проявлениях.
>Похоже на single source of truth.

## Normal forms
- **1NF**: 
	- All columns contain atomic values (no composite or multivalued attributes).
- **2NF**: 
	- Relation should be in First Normal Form (1NF).
	- Only applies when the primary key has multiple attributes
	- Every non-prime attribute functionally depends on the whole set of attributes of every candidate key (no partial dependencies).
- **3NF**:
	- Relation should be in Second Normal Form (2NF).
	- Each non-prime attribute must depend solely on each candidate key.
	- No non-prime attribute functionally depends of other non-prime attribute.
- Boyce–Codd Normal Form
