## Joins
**JOIN** clause is used to combine rows from two or more tables, based on a related column between them.
![|600](Pasted%20image%2020260403050143.png)
![](Pasted%20image%2020260403050844.png)

## Subqueries
A **subquery** is a query nested inside another SQL query.
![](Pasted%20image%2020260403050919.png)

- **IN**
```sql
SELECT name
FROM student
WHERE student_id IN (
	SELECT student_id
	FROM gradebook
	WHERE course_id = 10
);
```
- **EXISTS**
```sql
SELECT name
FROM student s
WHERE EXISTS (
	SELECT 1
	FROM gradebook g
	WHERE g.student_id = s.student_id
);
```
- **ANY**
```sql
SELECT *
FROM gradebook
WHERE grade > ANY (
	SELECT grade
	FROM gradebook
	WHERE student_id = 3
);
```
- **ALL**
```sql
SELECT *
FROM gradebook
WHERE grade > ALL (
	SELECT grade
	FROM gradebook
	WHERE student_id = 3
);
```
- **Division from Relational Algebra**
```sql
SELECT s.student_id FROM student s
WHERE NOT EXISTS (
	SELECT course_id FROM course c
	WHERE NOT EXISTS (
		SELECT 1 FROM gradebook g
		WHERE g.student_id = s.student_id
		AND g.course_id = c.course_id
	)
);
```
