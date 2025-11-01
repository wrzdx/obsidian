---
tags:
  - 1stYear
---
# Definition and properties:
- A *natural number* is a measure of the quantity of (indivisible) objects.
- Let $\mathbb{N}$ is the set that satisfies the following two properties:
	- $\mathbb{N}\subseteq \omega, \ \varnothing \in \mathbb{N}$ and with each element $A \in \mathbb{N}$ it contains the set $\{A,\{A\}\};$
	- N is *smallest* collection that satisfies (1) i.e $\mathbb{N} \subseteq M$ for every set $M$ such that $M \subseteq \omega,\ \varnothing \in M$ and with each element $A \in M$ it contains the set $\{A,\{A\}\}$. 
# Constants, predicates and operations on natural numbers:
- Let $0$ be $\varnothing$; if $n$ is defined already then let $(n+1)$ be $\{n,\{n\}\}.$ For example: 1 is $\{\varnothing,\{\varnothing\}\},$ 2 is $\{\{\varnothing,\{\varnothing\}\},\{\{\varnothing,\{\varnothing\}\}\}\},$ etc.
- We can define:
	- predicate $(n=0)$ on $\mathbb{N}$ as $(n = \varnothing);$
	- function (+1): $\mathbb{N}\rightarrow\mathbb{N}$ is $n$ $\mapsto \{n,\{n\}\}$.
# Induction principle and proofs by induction:
- Let $P$ be a monadic predicate (i.e a property of natural numbers):
	- If $0 \in P$ (induction basis),
	- and for $n \in P$ (induction hypothesis) implies $(n+1) \in P$ (induction step) every $n\in \mathbb{N}$
	- then $P = \mathbb{N}$
- The principle follows from the definition of the natural numbers and set theory axiomatic.