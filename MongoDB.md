MongoDB is a document-oriented NoSQL database that *stores* data in *documents* rather than rows.

Documents are grouped into *collections*. A collection is a grouping of related documents and is the *equivalent of a table* in a relational database system.

It is designed for:
- flexible schema
- rapid development
- horizontal scaling
- handling semi-structured and nested data

>[!note] Why Use MongoDB?
>MongoDB uses a flexible document model. 
>Documents in one collection do not have to contain the same fields. A field can even have different data types across documents.

>[!note] 
>MongoDB commonly works with BSON internally

```json
{ 
	"_id" : 101, 
	"name" : "Ivan", 
	"major" : "Computer Science", 
	"year" : 2, 
	"skills" : [
		"SQL", 
		"Python", 
		"MongoDB"
	], 
	"address" : { 
		"city" : "Kazan", 
		"country" : "Russia" 
	} 
}
```

## Create Collection
**Method 1**
```python
db.createCollection("posts")
```

**Method 2**
creation during the insert process (assuming it doesn't already exist)
```python
db.posts.insertOne(object)
```
## Insert
**Insert One**
```python
db.posts.insertOne({ 
	title: "Post Title 1", 
	body: "Body of post.", 
	category: "News", 
	likes: 1, 
	tags: ["news", "events"], 
	date: Date() 
})
```

**Insert Many**
```python
db.posts.insertOne([
	{ 
		title: "Post Title 1", 
		body: "Body of post.", 
		category: "News", 
		likes: 1, 
		tags: ["news", "events"], 
		date: Date() 
	},
	{ 
		title: "Post Title 2", 
		body: "Body of post.", 
		category: "Event", 
		likes: 1, 
		tags: ["news", "events"], 
		date: Date() 
	}
])
```

## Find
**Find all**
```python
db.posts.find()
```

**Find the first element**
```python
db.posts.findOne()
```

**Querying documents**
```python
b.students.find({ year: 2 })
db.students.find({ year: { $gte: 2 } })
db.students.find({ "address.city"
:
"Kazan" })
db.students.find({ skills:
"Python" })
db.students.find({ $or: [ { year: 1 }, { year: 2 } ] })
```