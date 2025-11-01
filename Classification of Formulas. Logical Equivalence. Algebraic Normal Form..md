---
tags:
  - 1stYear
---
# Classification of Formulas:
- Definition of a (Math Logic) formula:
	- Any proposition is a formula.
	- If $\phi, \ \phi_{1}, \ \phi_{2}$ are formulas then the following are formulas:
		- $(\neg \phi)$
		- $(\phi_{1}\ \land \phi_{2})$
		- $(\phi_{1} \vee \phi_{2})$
		- $(\phi_{1} \rightarrow \phi_{2})$
		- $(\phi_{1}\leftrightarrow \phi_{2})$
- A proposition (formula) that is always true is called a ***tautology***.  
  ![|300](Pasted%20image%2020240905125651.png)  
- A proposition (formula) that is always false is called a ***contradiction.***
  ![|300](Pasted%20image%2020240905125724.png)
- A proposition (formula) that is neither a tautology nor a contradiction is called a ***contingency.***
  ![|300](Pasted%20image%2020240905125812.png) 
- A proposition/formula is ***satisfiable*** (can be satisfied) if there is an assignment of truth values (true or false) to its variables that makes it true. It means it is not a contradiction.
  **Explanation:** There is at least one combination of values to variables such that a result of formula is true.
  **Example:** $x\ \&\ y$ is satisfiable because there is a ***solution*** $-$ $x= 1$and $y=1$. But $x\ \&\ \neg x$ is not satisfiable.
- ***Cook-Levin Theorem*** $-$ Satisfiability problem is NP (Non-deterministic Polynomial) $-$ complete.
# Logical Equivalence:
- Propositions (formulas) $P_{1}$ and $P_{2}$ are called logically equivalent if the truth tables of $P_{1}$ and $P_{2}$ are the same or, in another words, $P_{1}\leftrightarrow P_{2}$ is a tautology.
  **Denotations:** $P_{1}\equiv P_{2} \Leftrightarrow P_{1}\cong P_{2}\Leftrightarrow P_{1}\simeq P_{2}\Leftrightarrow P_{1}\sim P_{2}$           
  **Explanation:** The results of these are the same.
## Laws:
- Excluded Third Laws:
	- $a \vee \neg a \equiv 1$
	- $a \wedge \neg a \equiv 0$  
- Identity Laws: 
	- $a \vee 0 \equiv a$
	- $a\ \wedge 1 \equiv a$ 
- Domination laws:
	- $a \vee 1 \equiv 1$ 
	- $a \wedge 0 \equiv 0$
- Idempotent Laws:
	- $a \wedge a \equiv a$
	- $a \vee a \equiv a$  
- Double Negation Law:
	- $\neg(\neg a)\equiv a$
- Commutative Laws:
	- $a \wedge b \equiv b \wedge a$
	- $a \vee b \equiv b\vee a$
- Associative Laws:
	- $a \wedge (b \wedge c) \equiv (a\wedge b) \wedge c$
	- $a\vee (b \vee c) \equiv (a \vee b) \vee c$
- Distributive Laws:
	- $a \wedge (b\vee c) \equiv (a\wedge b)\vee (a \wedge c)$
	- $a \vee (c \wedge b) \equiv (a\vee b) \wedge (a\vee c)$
- De Morgan's Laws:
	- $\neg (a \wedge b) \equiv \neg a \vee \neg b$
	- $\neg(a\vee b)\equiv \neg a \wedge \neg b$
- Absorption Laws:
	- $a\vee (a\wedge b) \equiv a$
	- $a\wedge (a\vee b)\equiv a$
	- $a\vee(\neg a \wedge b) \equiv a\vee b$
	- $a\wedge (\neg a \vee b) \equiv a\wedge b$ 
- Implication:
	- $a \rightarrow b \equiv \neg a \vee b$
	- $a \rightarrow b \equiv \neg b \rightarrow \neg a$
- Bi-implication:
	- $a\leftrightarrow b \equiv (a \rightarrow b) \wedge (b \rightarrow b)$
	- $a \leftrightarrow b \equiv \neg a \leftrightarrow \neg b$ 
	- $\neg(a\leftrightarrow b)\equiv a \leftrightarrow \neg b$
	- $a \leftrightarrow b \equiv (a \wedge b) \vee (\neg a \wedge \neg b)$
	- $a\leftrightarrow b \equiv (\neg a \vee b) \wedge (a \vee \neg b)$ 
# Algebraic Normal Form:
- Logic Algebra Formula:
	- Any proposition (including 0 and 1) is a formula.
	- Suppose that $\phi_{1}, \ \phi_{2}$ are formulas. Then the following are formulas:
		- ($\phi_{1}\cdot\phi_2$)
		- $(\phi_{1} \oplus \phi_{1})$ 
- ***Algebraic Normal Form*** of a formula is a logical equivalent polynomial modulo 2 (Zhegalkin polynomial).
  **Explanation:** It's just approach to represent any usual for us formula to more simple way by using only two operators and two values $-$ 1 and 0:
	- multiplication $-$ $\cdot$
	- addition $-\ \oplus$ (XOR)
	![|360](Pasted%20image%2020240906094210.png)
  Rules are the same as in usual arithmetic but if we get value greater then 1 in our expression then we just take it by modulo 2.
- Replacements and useful notation:
	- $x^{n}\equiv x$
	- $x\oplus x \equiv 0$
	- $\neg x \equiv x\oplus 1$
	- $x \wedge y\equiv xy \leftrightarrow x\cdot y$
	- $x \rightarrow y \equiv 1 \oplus x \oplus xy$
	- $x\leftrightarrow y \equiv x\oplus y \oplus 1$
# Tutorial:
### Some task:
- $T(x,y)\equiv (1110)$

| x   | y   | T(x,y) |
| --- | --- | ------ |
| 0   | 0   | 1      |
| 0   | 1   | 1      |
| 1   | 0   | 1      |
| 1   | 1   | 0      |
**DNF:** $(\neg x \wedge \neg y) \vee (\neg x \wedge y) \vee (x \wedge \neg y)$ 
**CNF:** $\neg x \vee \neg y$
**DNF $\rightarrow$ CNF:** $(\neg x \wedge \neg y) \vee (\neg x \wedge y) \vee (x \wedge \neg y)$ $\equiv(\neg x \wedge (\neg y \vee y)) \vee (x \wedge \neg y)$ $\leftrightarrow \neg x \vee (x \wedge \neg y)$ $\equiv (\neg x \vee x) \wedge (\neg x \vee \neg y)\equiv \neg x \vee \neg y$ 

- Find Algebraic Normal Form for $(a \wedge \neg b) \rightarrow \neg a$:
  Solution:
  $(a \wedge \neg b) \rightarrow \neg a \equiv \neg a \vee b \vee \neg a \equiv \neg a \vee b \equiv (1\oplus a)\oplus b \oplus b(a\oplus 1)\equiv$
  $(1\oplus a) \oplus b\cdot(1\oplus a \oplus 1)\equiv 1\oplus a\oplus ab$