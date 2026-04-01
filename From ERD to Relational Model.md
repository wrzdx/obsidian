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
  Partial Key - unique 
- A weak entity cannot exist without its owner, so it uses the owner’s key

```
```col-md
===
![](Pasted%20image%2020260401163528.png)
```
````

