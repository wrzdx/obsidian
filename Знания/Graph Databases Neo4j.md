Neo4j is a graph database management system that uses the property graph model. Instead of organizing data mainly into tables and rows, it stores data as nodes, relationships, and properties.

Neo4j treats connections as first-class data, not just as foreign-key links between tables.

## Data Model
Neo4j uses a property graph database model.

In this model, the graph consists of:
- **Nodes** - entities or objects in the domain
- **Relationships** - connections between nodes
- **Properties** - key-value pairs attached to nodes or relationships
- **Labels** - categories used to classify nodes
- **Relationship types** - categories used to classify relationships

>[!note] Important characteristics
>- a node can have zero or more labels
>- a relationship always has a direction
>- a relationship must have one type
>- both nodes and relationships can store properties

## Cypher
### Nodes & Labels
*Nodes* are used to represent *entities* (discrete objects) of a domain.

*Labels* shape the domain by g*rouping nodes into sets* where all nodes with a certain label belong to the same set.

A node can have zero to many labels.

**Example:**
```cypher
CREATE (:Person:Actor {name: 'Tom Hanks' , born: 1956})
```

### Relationships
A relationship describes how a connection between a source node and a target node are related. It is possible for a node to have a relationship to itself.

A relationship:
- connects a source node and a target node
- has a direction
- must have a relationship type
- can have properties (key-value pairs)


**Example:**
```cypher
CREATE ()-[:ACTED_IN {roles: ['Forrest'], performance: 5}]->()
```

### Querying Data
- `{cypher}MATCH` – finds patterns in the graph
- `{cypher}WHERE` – adds conditions to a MATCH
- `{cypher}RETURN` – defines what should appear in the result

**Example:**
```cypher
MATCH (p:Person)-[:ACTED_IN]->(m:Movie) WHERE p.name = 'Tom Hanks' RETURN m.title
```

## When to Use Neo4j?
**Сommon applications:**
- recommendation engines
- fraud and anomaly detection
- dependency and network analysis
- knowledge graph applications

**Main strengths:**
- natural representation of relationships
- expressive graph queries with Cypher
- strong fit for traversal and pattern-matching tasks

>[!summary] 
>Neo4j is a strong choice when data is not just a set of records, but a network of connected entities.

