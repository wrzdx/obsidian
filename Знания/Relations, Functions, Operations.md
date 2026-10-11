---
tags:
  - 1stYear
---
# Definition:
- Relation (or predicate) on a set $X$ is some subset $Y$ of $X$.
- Examples:
	- natural numbers $p$ and $q$ are co-prime
	- a natural numbers $z$ is a common multiple of two natural numbers $x$ and $y;$
	- a natural number is prime.
# Arity (number of arguments):
- $Y$ is a binary relation on $X_{1}$ and $X_{2}$ if $X$ is Cartesian product of sets $X_1$ and $X_{2}$ (i.e $Y \subseteq X_{1}\times X_{2}$);
- $Y$ is a ternary relation on $X_{1},\ X_{2}$ and $X_{3}$ if $X$ is Cartesian product of sets $X_{1},\ X_{2}$ and $X_{3}$ (i.e $Y \subseteq X_{1}\times X_{2}\times X_{3}$);
- when $X$ isn't a Cartesian product then predicate $Y$ is a monadic pradicate.
# Relations on a set:
- Multi-arity relation on a set is any subset of $X\times ...X=X^{k}\ (k\in \mathbb{N})$. 
  **Explanation:** Just one of all combination with repeations that selects by some property. 
- Binary relation on a set is
	- reflexive if $xRx$ for every x;
	- irreflexive if never $xRx$;
	- symmetric if $xRy$ implies $yRx$ for all $x$ and $y$;
	- transitive if $xRy$ and $yRz$ implies $xRz$ for all $x$,$y$ and $z$
# Equality:
- Reflexive, symmetric and transitive relation is called equivalence.
- Equality is the equivalence that satisfies Leibnitz axiom: $x=y$ iff $\phi(x)\Leftrightarrow \phi(y)$ for every property $\phi.$
# Pre-order, partial and linear order:
- Pre-order (or quasi-order) is a reflexive and transitive relation.
- (Partial) order is an anti-symmetric pre-order, i.e, for any $x$ and $y$, if $xRy$ and $yRx$ then $x=y$.
  **Note:** It means that anti-simmetric relation can be simmetric iff their arguments are equal, otherwise, relation is not anti-simmetric
  **Note:** If a relation is **not anti-symmetric**, it does not imply that it is **symmetric**.
- Linear order is a partial order where all elements are compatible (comparable), i.e., for all $x$ and $y$, either $xRy$ or $yRx$. (Examples?)
# Fucntion is a Relation:
- Function $F:\ D\rightarrow R$ is a binary relation $F\subseteq D\times R$ such that for every $x\in D$ there exists at most one $y\in R$ such that $(x,y)\in F.$
	- $D \rightarrow R$ is type of $F$,
	- $D$ is called domain of $F$,
	- $R$ is called range (or co-domain) of $F$,
	- support of $F$ is the set $\{x\in D:F$ is defined on $x\}$,
	- image of $F$ is the set $\{F(x):x\in D\}$.
# Injection, bijection, surjection..:
- Let $F:D\rightarrow R$ be a function.
	- $F$ is a total if the support equals to the domain;
	- $F$ is a surjection if the range equals to the image;
	- $F$ is a bijection if it is a total surjective injection.
# Operation on a set:
- A function $F:D\rightarrow R$ is an operation on $R$ if it is total and the domain is Cartesian product of some copies of range $R$ (i.e., $D=R\times ... R$).
  **Example:** Let $R$ is a set $\{0,1\}$ and function $f(x)$ is for example conjuction & between 2 element, then $D$ is a $R^{2}$ $\{(0,0),(0,1),(1,0),(1,1)\}$
- Remark: elements of $R$ may be considered as constant operations with zero-arity.
  **Explanation:** $R=\{f(),\ g(),\ ...\}$, $f()=a,\ g()=b,...$ always.
- Algebraic system is a set with a fixed set of predicates and operations on it. Algebra is an algebraic system with a single predicate equality.
  i.e There are no unknown predicates and operations.
# $\lambda$-notation (by examples):
- $2\times y +3$ where $y\in \mathbb{R}$ that depends on a *parameter* $y$, but not a function;
- $\lambda y \in \mathbb{R}.\ (2\times y + 3)$ is a (nameless) function with variable $y$ on real numbers that maps every real value $r\in R$ to real number $(2\times r +3)\in \mathbb{R}$;
- $f = \lambda y \in \mathbb{R}.\ (2\times y + 3)$ is equality between two functions (anonymous function $\lambda y \in \mathbb{R}.\ (2\times y +3$) has got name $f$.