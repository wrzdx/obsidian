---
tags:
  - 1stYear
---
# Basic elements:

> [!abstract] Naive definition
> A set is an unordered collection of things (not counting multiplicities), its elements.
> **Description:**
> *List* $X = \{x_{1}, x_{2},..., x_{n}\}$
> *Rule* $X = \{x\ |$ some condition on $x$ holds$\}$

> [!abstract] Extension Principal (Leibniz)
> Two sets equal if and only if they have the same elements.
> $$A=B$$

>[!abstract] Subset
>If every element of a set $A$ is also a element of $B$, then we say that $A$ is a subset of $B$, and write $$A\subseteq B$$
>If $A\subseteq B$ but $A\neq B$, we write $A\subsetneq B$ and say that $A$ is a proper subset of $B$.
>$$A=B \texttt{ iff both } A\subseteq B \texttt{ and } B\subseteq A$$

>[!abstract] Empty set
>The empty set is the empty list $$\emptyset = \{\}$$

>[!abstract] Universal set
>The universal set $\mathbb{U}$ is a fixed set such that all considered sets of  given problem are its subsets.

>[!abstract] Complement
>For any set $A$, the **complement** of $A$ is the set $$\overline{A} = \{x\ |\ x\in \mathbb{U} \wedge x\not\in A\}$$
>![|400](Pasted%20image%2020240926220649.png)

>[!abstract] Intersection 
>For any sets $A_{1}$ and $A_{2}$, the intersection of $A_{1}$ and $A_{2}$ is the set $$x\in A_{1} \vee A_{2} \text{ iff } (x\in A_{1})\wedge (x\in A_{2})$$
>![|400](Pasted%20image%2020240926221207.png)

>[!abstract] Union
>For any sets $A_{1}$ and $A_{2}$, the union of $A_{1}$ and $A_{2}$ is the set
>$$x\in A_{1}\vee A_{2} \text{ iff } (x\in A_{1})\vee (x\in A_{2})$$
>![|400](Pasted%20image%2020240926221413.png)

>[!abstract] Difference 
>For any sets $A_{1}$ and $A_{2}$ the difference of $A_{1}$ and $A_{2}$ is the set 
>$$x\in A_{1} \text{ \\ } A_{2} \text{ iff } (x\in A_{1}) \wedge (x\not \in A_{2}) $$
>$$x\in A_{1} \text{ \\ } A_{2} = A_{1}\wedge \overline{A_{2}}$$
>![|400](Pasted%20image%2020240926221720.png)

---
# Cartesian product:

>[!abstract] Definition 
>For any sets $A_{1}$ and $A_{2}$, the Cartesian product of $A_{1}$ and $A_{2}$ is the set $A_{1} \times A_{2} = \{(x,y)\ | \ x\in A_{1}\wedge y\in A_{2}\}$, 
>where $(x,y)$ is an ordered pair.

>[!abstract] Non-idempotent 
>$A\times A \neq A$

>[!abstract] Non-commutative
>$A\times B \neq B\times A$

>[!abstract] Null 
>$A \times \emptyset = \emptyset \times A = \emptyset$

>[!abstract] Associative
>$A\times (B\times C) = (A\times B) \times C$
>*$(x,(y,z)) = ((x,y),z) = (x,y,z)$

>[!abstract] $\vee$-properties
>$$(A\vee B)\times C = (A\times C)\vee (B\times C)$$
>$$A\times (B\vee C) = (A\times B) \vee (A\times C)$$

>[!abstract] $\wedge$-properties
>$$(A\wedge B)\times C = (A\times C)\wedge (B\times C)$$
>$$A\times (B\wedge C) = (A\times B)\wedge (A\times C)$$

>[!abstract] Extended $\wedge$-property
>$$(A\wedge B)\times (X\wedge Y) = (A\times X) \wedge (B\times Y)$$

---

# Power Set:

>[!abstract] Definition 
>For a set $A$, the **Power Set** of $A$ is the set 
>$$2^{A} = \mathcal{P}(A) = \{B \ | \ B\subseteq A\}$$ 

---

# Cardinality:

>[!abstract] Definition
>Intuitively, the cardinality of a set $A$, denotes by $|A|$, is the number of elements of $A$

>[!abstract] Standard
>To use $|\cdot|$, we need a standard (etalon)! This etalon is empty set $\emptyset$, because it's unique.

>[!abstract] Natural numbers
>Since all natural numbers $0,1,2,3...$ are defined, define the set $\mathbb{N} = \{k\ | \ k$  is a natural number$\} = \{0,1,2,3...\}$
>$\mathbb{N} = \omega$ or $\aleph_{0}$, i.e., $\mathbb{N}$ is countable.

>[!abstract] Integer Number 
>$$Z = \{..., -3,-2. -1 ,0 , 1, 2, 3...\}$$
>$|\mathbb{Z}| = \omega$

>[!abstract] Rational numbers 
>$$\mathbb{Q} = \{(n,m) \in \mathbb{Z} \ | \ m\neq 0 \wedge \frac{n}{m} \text{is irreducible}\}$$
>$$|\mathbb{Q}|=\omega$$ 

>[!abstract] Real numbers
>$$|\mathbb{R} |= 2^{\omega}$$

>[!abstract] Properties 
>$$|A\vee B | = |A| + |B| - |A\wedge B|$$
>![|400](Pasted%20image%2020240927111043.png)
>$$|A\vee B| = | A| + |B|, \text{ if $A\wedge B = \emptyset$}$$
>$$|A\times B| = |A| \cdot |B|$$