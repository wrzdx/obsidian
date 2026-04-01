## Step 1: Mapping strong entities
````col
```col-md
flexGrow=1
===

- Create a table for each strong entity
- Include all the simple attributes of the entity
- Select a primary key from the entity’s key attributes
- If the key is composite, use all its parts together as the primary key
- Each strong entity becomes one table with its own primary key

```
```col-md
===
![|250](Pasted%20image%2020260401163003.png)
```
````

## Step 2: Mapping weak entities
````col
```col-md
flexGrow=1
===

- Create a table for each weak entity
- Include all the simple attributes of the entity
- Add the primary key of its owner entity as a *foreign key*
- The primary key of this table is a combination of the owner’s key and the weak entity’s partial key
  *Partial Key* - unique attribute that makes weak entity unique for its owner
- A weak entity cannot exist without its owner, so it uses the owner’s key

```
```col-md
===
![](Pasted%20image%2020260401163528.png)
```
````

## Step 3: Mapping 1:1 relationships
### One or no total participation
````col
```col-md
flexGrow=1
===

- Choose the entity with total participation (if any)
- Add a foreign key in that entity’s table that references the primary key of the other entity
- Include any relationship attributes in the same table
- If neither entity has total participation, choose either side for the foreign key
- In rare cases, additional crossreference relation (extra intermediate table) may be created
```
```col-md
===
![](Pasted%20image%2020260401164229.png)
```
````

### Both total participation
````col
```col-md
flexGrow=1
===

- Since both have total participation, they are fully dependent on each other
- Merge both entities and the relationship into a single table
- Choose one of the primary keys as the primary key of the merged table
- When both sides are totally dependent, one combined table avoids redundancy
```
```col-md
===
![](Pasted%20image%2020260401164551.png)
```
````
## Step 4: Mapping 1:N relationships
````col
```col-md
flexGrow=1
===

- Find the entity on the N-side (many side)
- Add a foreign key in that entity’s table that references the primary key of the 1- side entity
- Add any relationship attributes to the same table on the N-side
- The foreign key always belongs to the “many” side
```
```col-md
===
![](Pasted%20image%2020260401164851.png)
```
````
