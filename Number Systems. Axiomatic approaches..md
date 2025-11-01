---
tags:
  - 1stYear
---
# Peano Postulates (Axioms):
- Peano axioms (Dedekind-Peano axioms or the Peano postulates), are axioms for the natural numbers presented by Italian mathematician Giuseppe Peano  in 1889.
- We introduce Peano axioms with operation "+1" only while addition and multiplication may be introduced as derived operations.
- It is usually assumed that 1 is the first natural number, but we will assume that 0 is the first natural number. (However, it is always necessary and possible to agree.)
- The number following (by "+1" operation) any natural is also a natural; if a natural number $x$ immediately follows both the number $y$ and the number $z$, then $y$ and $z$ are equal.
  
> [!abstract] Axioms of Induction: 
  If a proposition $P(n)$
  >- (base of induction) proved for a given natural number $m$ (for example, for m = 2023)
  >- and if (step of induction) from the hypothesis (assumption) that $P(k)$ is true for a natural number $k$, it follows that it is true for the natural following $k$ (i.e, for (k+1)),
>
>then the proposition $P(n)$ is true for all natural numbers starting from $m$.

# Tarski's axiomatization
- Alfred Tarski set out (in 1936) an axiomatization of the real numbers and their arithmetic, using the following signature:
	- $\mathbb{R}$ for the set of reals,
	- infix "<" for a total binary relation on $\mathbb{R}$,
	- infix "+" for addition over $\mathbb{R}$,
	- and the constant $1$.
- We introduce Tarski axioms with operation "+" only while multiplication may be introduced asd derived operation.
  
- **Permutable associativity**: For all $x,y,$ and $z$, $x+(y+z)=(x+z)+y.$
- **Subtraction:** For all $x,y,$ there exists some $z$ such that $x+z=y.$
- **Monotonicity:** If $x+y<z+w$, then $x<z$ or $y<w$.
- **Axioms for one:** $1\in \mathbb{R}$ and $1<1+1$.
- **Irreflexivity of $<:$** if $x<y$. then not $y<x$.
- **$<$ is dense:** If $x<z$, there exists a $y$ such that $x<y$ and $y<z$.
- **$<$ is Dedekind-complete:**
	- for all $X,Y \subseteq \mathbb{R}$,
	- if for all $x\in X$ and $y\in Y$, if $x<y$,
	- then there exists some $z$ such that
	- for all $x\in X$ and $y \in Y$,
	- if $z\not = x$ then $x<z$ and if $z\neq y$ then $z<y$.
# Real numbers is a field..:
- **Commutativity, Associativity, Distributivity works.**
- **Additive and multiplicative identity:** there exists two distinct elements $0$ and $1$ that $a+0=a$ and $a\cdot 1 = a$ for every $a$.
- **Multiplicative inverses:** for every $a\neq 0$ there exists an element $a^{-}$ ) also denoted as $\frac{1}{a}$) such that $a\cdot a^{-}=1$.
# But a special field..:
- Every upper / down bounded $A\subseteq \mathbb{R}$ has supremum / infimum respectively:
	- If there exists some $b\in \mathbb{R}$ such that if $a < b$ for all $a\in A$, then there exists some $c\in \mathbb{R}$ such that if $a\leq c$ for all $a\in A$, and $c\leq d$ where $d$ is any upper bound for $A$ (i.em $a\leq$ d for all $a\in A$).
	  **Explanation:** First statement: "If there exists some $b\in \mathbb{R}$ such that if $a < b$ for all $a\in A$" - says that $A$ is *finite*. Second statement: "there exists some $c\in \mathbb{R}$ such that if $a\leq c$ for all $a\in A$" says that there is the exact max value in $A$ (not that value who are reaches).    
	- If there exists some $b\in \mathbb{R}$ such that if $b<a\ |\ \forall a\in A$, then there exists some $c\in \mathbb{R}$ such that if $c\leq a \ | \ \forall a\in A$, and $d\leq c$ where $d$ is any upper bound for $A$ (i.e., $d\leq a \ |\ \forall a \in A$).
- Supremum and infimum of a set $A$ are denoted (if any) as sup $A$ and inf $A$ respectively: