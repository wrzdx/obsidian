---
tags:
  - 1stYear
---
# Naive Set Theory postulates existence of:
- the empty set and enumerable sets, an infinite set,
- maps (functions from a set in a set) and power-sets (the sets of all subsets of a set),
- specified subsets by properties,
- unions and Cartesian products of sets.
# The Empty Set, Enumerable Sets, Extensionality:
- There is an empty set $\varnothing$ which has no elements at all: $A \notin \varnothing$ for every set of $A$.
  
- For any infinite collection of sets of $A_{1},\ ...\ A_{n}$ there exists set $\{A_{1},\ ...\ A_{n}\}$ which elements are exactly $A_{1},\ ...\ A_{n}$.
  **Explanation:** In other words, any set is contained in another set.
  
- For all sets of $A$ and $B$, $B\subseteq A$ if $C \in B$ implies $C \in A$ for all $C$; sets are equal when they include each other: $A = B$ if  $A \subseteq B$ if $A \subseteq B$ and $B \subseteq A.$ 
# An (Actual) Infinity:
- There is a set of $\omega$ that:
	- inlcudes the empty set $\varnothing$,
	- with each element $A$ contains a two-element set $\{A, \{A\}\}$: for any $A$, if $A \in \omega$, then $\{A, \{A\}\} \in \omega$.  
# Set Union, Power-set and Specified subset:
- **Definition:** For any set of $A$ there the union ($\cup_{B\in A} B$) is a set which consists of all "elements of elements" in $A$: $C \in (\cup_{B\in A} B)$ if $C \in B$ for some $B \in A$.
  **Explanation:** It gets all unique elements from $A$ and if there are nested sets then it discloses them but only first level nested sets.
  **Example:** $A = \{\{1,2\},2,\{3,4\},\{\{2\}\}\}$, then $\cup_{B\in A}B = \{1,2,3,4,\{2\}\}$.     
  
- **Definition:** For any set $A$ the power-set of all his subsets (designation $2^{A}$, $P(A) \ or \ \{B:\ B\subseteq A\}$) is a set.
  **Explanation:** $P(A)$ is set of all subset of set $A$. Count of elements of $P(A)$ is calculated by $2^A$ formula.
  **Example:** Let $A = \{1,2\}$, then $P(A) = \{\varnothing,\{1\},\{2\},\{1,2\}\}$ and quantity of his elements is $2^{2}=4$. 
  
- **Definition:** For any set $A$ and any property $\phi$ (formulated in terms of the naive set theory) collection $\{B:\ B\in A$ and $\phi (B)\}$ is a set (comprising elements of $A$ which enjoy the property $\phi$).
  **Explanation:** $\phi$ - это некоторое условие, по которому отбираются элементы множества $B$ из множества $A$, то есть $B$ это отфильтрованное множество $A$ по условию $\phi$.
  **Example:** $A = \{1,2,3,4,5\},\ \phi(B)$ = "$B$ is a even number." Then:
  $\{B: B\in A$ and $\phi(B)\}$$= \{2,4\}$   
# Optional (to complicated): Axiom of Choice (Cartesian Products):
- For all sets of $A$ and $B$ every total function (correspondence) $F: \ A \rightarrow B$ is a set.
  > [!Help]- Explanation: 
  > $F: \ A\rightarrow B$ means $F(a)\in B$ for each element $a\in A.$ Thus, we get set of elements $\{a,F(a)\ |\ a\in A\}\Leftrightarrow\{a,B\ | \ a\in A\}$. If we will apply this function to each element of $A$ then we get a new set of **ordered pairs**$\{\{a_{1},F(a_{1})\},...,\{a_{n},F(a_{n})\}\ |\ a_{i}\in A\} \Leftrightarrow \{\{a_{1},b_{1}\},...,\{a_{n},b_{n}\}\ |\ a_{i}\in A,\ b_{i}\in B\}.$It's the set of function itself.

- For all sets of $A$ and $B$, any total function $I: \ A \rightarrow B$
  if $I(A)$ doesn't contain the empty set, then there exists the set $\Pi_{C\in A}I(C) \neq \varnothing$ of all functions $F: \ A \rightarrow (\cup_{D\in B}D)$ such that $F(C)\in I(C)$ for every $C \in A.$  
  >[!Help]- Explanation: 
  >1) Let we have set $A$, and each element of this set is also set that not equals to $\varnothing$: $A =\{a,b,c\ \ | \ a=\{..\}\neq\varnothing,\ b=\{..\}\neq\varnothing,\ c=\{..\}\neq\varnothing\}$, then the Axiom of Choice above says that it is possible to choose at least one element from each set of set $A$. 
  2) Function $I: A\rightarrow B$ just explicit show us the set of set A: Let $A=\{a,b\}$ where $a,b,c$ are sets as well and let $a=\{1,2\},\ b=\{3,4\}$, then $I_{C\in A}(C)=\{\{1,2\},\{3,4\}\},\ (I_{C\in A}(C)\Leftrightarrow I(C),\ C\in A)$. And $B=I_{C\in A}(C).$
  >3) $\Pi_{C\in A}I(C) \neq \varnothing$ means *The Cartesian Product* of $I_{C\in A}(C)$ exists and don't equal an empty set, i.e there is at least one combination of elements. For example: Let we have $A = \{a,b\},\ a=\{1,2\},\ b=\{3,4\},$ then $I_{C\in A}(C)=\{\{1,2\},\{3,4\}\},$ and $\Pi_{C\in A}I(C) = \{\{1,3\},\{1,4\},\{2,3\},\{2,4\}\}.$
  > 4) Function $F()$ just maybe functions for selecting some element from each set, I'm not sure because the statement not clear.