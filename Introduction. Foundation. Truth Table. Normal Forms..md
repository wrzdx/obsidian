---
tags:
  - 1stYear
---
# Material: 
- [Lecture](https://moodle.innopolis.university/pluginfile.php/209942/mod_resource/content/1/Lec1.pdf)
- [Tutorial](https://moodle.innopolis.university/pluginfile.php/209943/mod_resource/content/1/Tut1.pdf)
- [Lab](https://moodle.innopolis.university/mod/resource/view.php?id=115260)
# Main Points:
## Disjunctive Normal Form (DNF):
- A disjunctive normal form (DNF) is one conjunct or a disjunction of conjuncts.
- A conjunct (conjunctive term) is one literal or a conjunction of literals, where each literal is either a variable, or its negation.
- To obtain a Disjunctive Normal Form (DNF) from truth table, use the following algorithm: 
	- selecting all rows that evaluate to 1,
	- for each such row, construct a conjunct of literals in the following way: 
		- positive literals for corresponding 1 values for the propositional variable,
		- negative literals, otherwise (for corresponding 0 values),
- The DNF is the disjunctions of all these conjuncts
**Example:**
- Obtain DNF from the truth table: T(a, b) = (1110)
**Solution:**

|  a  |  b  | T(a,b) | $$ \neg a\wedge\neg b $$ | $$\neg a \wedge b$$ | $$a \wedge \neg b$$ |
| :-: | :-: | :----: | :----------------------: | :-----------------: | :-----------------: |
|  0  |  0  |   1    |            1             |          0          |          0          |
|  0  |  1  |   1    |            0             |          1          |          0          |
|  1  |  0  |   1    |            0             |          0          |          1          |
|  1  |  1  |   0    |            0             |          0          |          0          |
**Answer:** $$(\neg a \wedge \neg b) \vee (\neg a \wedge b) \vee (a \wedge \neg b)$$
## Conjunctive Normal Form (CNF):
- A conjunctive normal form (CNF) is one disjunct or a conjunction of disjuncts.
- A disjunct (disjunctive term) is one literal or a disjunction of literals, where each literal is either a variable, or its negation.
- To obtain a Conjunctive Normal Form (CNF) from truth table, use the following (inverted) algorithm:
	- selecting all rows that evaluate to 0, 
	- for each such row, construct a disjunct of literals in the following way:
	- positive literals for corresponding 0 values for the propositional variable,
	- negative literals, otherwise (for corresponding 1 values), 
- The CNF is the conjunctions of all these disjuncts
**Example:**
- Obtain CNF from the truth table: T(a, b) = (1000)
**Solution:**

| a   | b   | T(a, b) | $$a \vee \neg b$$ | $$\neg a \vee b$$ | $$\neg a \vee \neg b$$ |
| --- | --- | ------- | ----------------- | ----------------- | ---------------------- |
| 0   | 0   | 1       | 1                 | 1                 | 1                      |
| 0   | 1   | 0       | 0                 | 1                 | 1                      |
| 1   | 0   | 0       | 1                 | 0                 | 1                      |
| 1   | 1   | 0       | 1                 | 1                 | 0                      |
**Answer:**
$$(a \vee \neg b) \wedge (\neg a \vee b) \wedge (\neg a \vee \neg b) $$