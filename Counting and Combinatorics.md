---
tags:
  - 1stYear
---
# Basic Rules

> [!note] Sum Rule
$A_1$ is the set of all $n_1$ ways for an event $e_1$.  
$A_2$ is the set of all $n_2$ ways for an event $e_2$.  
"$e_1$ and $e_2$ are mutually exclusive" means $A_1 \cap A_2 = \emptyset$.
> 
> **Sum Rule (of mutually exclusive events):**
> $$|A_1 \cup A_2| = |A_1| + |A_2|$$

> [!note] Product Rule
> $A_1$ is the set of all $n_1$ ways for an event $e_1$,  
> $A_2$ is the set of all $n_2$ ways for an event $e_2$.
> 
 **Product Rule:**
> $$|A_1 \times A_2| = |A_1| \cdot |A_2|$$

---

# Principles

> [!note] Pigeonhole Principle
> If there are more objects than boxes then there is at least one box with more than one object.
![](Pasted%20image%2020241031102534.png)7 balls and 5 boxes

> [!note] Generalized Pigeonhole Principle
> If $n$ objects are placed into $k$ boxes then there is at least one box containing at least $\left\lceil \frac{n}{k} \right\rceil$ objects.

> [!note] Inclusion-Exclusion Principle
> If we used the sum rule some elements would be counted twice.  
> Use a sum rule and then correct for the overlapping elements.
> 
> $$|A_1 \cup A_2| = |A_1| + |A_2| - |A_1 \cap A_2|$$
> ![](Pasted%20image%2020241031103109.png)

> [!note] Generalized Inclusion-Exclusion Principle
> $$\displaylines{
|A_1 \cup A_2 \cup \dots \cup A_n| = \sum_{i=1}^n |A_i| -\sum_{i,j=1(i<j)}^n |A_i \cap A_j| + \\
\sum_{i,j,k=1(i<j<k)}^n |A_i \cap A_j \cap A_k| - \dots + (-1)^{n+1} |A_1 \cap A_2 \cap \dots \cap A_n|
}$$

---

# Pairs

> [!note] Definition
> $\{x, y\}$ is an unordered pair,  
> $(x, y)$ is an ordered pair.

> [!example] Examples
> 1. Let $A = \{a, b\}$.  
> - All unordered pairs: $aa, ab, bb$  
> - All ordered pairs: $aa, ab, ba, bb$
> 
> 2. Let $A = \{a, b, c\}$.  
> - All unordered pairs: $aa, ab, ac, bb, bc, cc$  
> - All ordered pairs: $aa, ab, ac, ba, bb, bc, ca, cb, cc$

---

# Arrangements

Let $A = \{a_1, \dots, a_n\}$.

> [!note] Definition
> - Unordered tuples $\{a_{i_1}, a_{i_2}, \dots, a_{i_k}\}$  
> - Ordered tuples $(a_{i_1}, a_{i_2}, \dots, a_{i_k})$  
> In Combinatorics, "Tuples" = "Arrangements"

> [!example] Example
> Let $A = \{a, b, c\}$  
> - Unordered arrangements: $aaa, aab, aac, abb, abc, acc, bbc, bbb, ccc$  
> - Ordered: $aaa, aab, aac, \dots, cbb, cbc, cca, ccb, ccc$

---

# Ordered Arrangements

> [!info] Remark
> Ordered arrangements could be with repetitions and without repetitions.

> [!example] Example
> Let $A = \{a, b, c\}$. Ordered arrangements  
> - with repetitions: $aaa, aab, aac, \dots, cbb, cbc, cca, ccb, ccc$  
> - without repetitions: $abc, acb, bac, bca, cab, cba$

---

# Arrangements

Let $A = \{a, b, c\}$.

|                      | without repetitions        | with repetitions                     |
| -------------------- | -------------------------- | ------------------------------------ |
| order matters        | $ab, ba, ac$$, ca, bc, cb$ | $aa, ab, ba, ac, ca, bb, bc, cb, cc$ |
| order doesn’t matter | $ab, ac, bc$               | $aa, ab, ac, bb, bc, cc$             |

---

# Ordered Arrangements with Repetitions

To find the number of $k$ ordered arrangements with repetitions from a set $A$:

> [!note] Generalized Product Rule
> $$|A_1 \times A_2 \times \dots \times A_n| = |A_1| \cdot |A_2| \cdot \dots \cdot |A_n|$$

Thus, the total number of arrangements is:

$$|A^k| = |A|^k$$

---

# Ordered Arrangements without Repetitions

> [!note] Definition
> A **permutation** of a set of distinct objects is an ordered arrangement of these objects.  
> The number of permutations is  
> $$P(n, n) = n \cdot (n - 1) \cdot (n - 2) \cdots 1 = n!$$
> $$P(n, k) = \frac{n!}{(n - k)!}$$


> [!example] Examples
> - Let $S = \{1, 2, 3\}$. There are $3! = 6$ permutations:  
> $(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)$
> 
> - How many words (permutations) can be made from the letters of **LOGIC**? There are $5! = 120$ permutations.

---

# Unordered Arrangements (Without Repetitions)

> [!note] Definition
> Suppose that we have $n$ distinct objects. An $k$-combination of the $n$ objects is a subset consisting of $k$ of the objects.

> [!theorem] Theorem
> The number of $k$-combinations of $n$ objects is  
> $$C(n, k) = \binom{n}{k} = \frac{n!}{k!(n - k)!}$$  
> (We read $\binom{n}{k}$ as "n choose k")

> [!example] Example
> There are 30 students in a group. We need to choose:  
> a) 2 students as volunteers,  
> b) 2 students as a group leader and his assistant.
> 
> a) Unordered arrangements  
> b) Ordered arrangements  
> $$P(30, 2) = 30 \cdot (30 - 1) = 30 \cdot 29 = 870$$

---

# Binomial Coefficients

$\binom{n}{k}$ is also called a **binomial coefficient**.

> [!theorem] Binomial Theorem
> Let $x, y$ be variables, $n \geq 1$ be a natural number. Then  
> $$(x + y)^n = \sum_{j=0}^n \binom{n}{j} x^{n - j} y^j$$
> 
> Expanded form:  
> $$(x + y)^n = \binom{n}{0} x^n + \binom{n}{1} x^{n-1} y + \dots + \binom{n}{n - 1} xy^{n - 1} + \binom{n}{n} y^n$$

---

# Multinomial Coefficients

> [!note] Definition
> We use $\binom{n}{r_1, \dots, r_m}$ to denote the number of arrangements of $n = r_1 + \dots + r_m$ objects, where for each $i$ $(1 \leq i \leq m)$ we have $r_i$ indistinguishable objects of type $i$.  
> $$\binom{n}{r_1, \dots, r_m} = \frac{n!}{r_1! r_2! \dots r_m!}$$

> [!theorem] Multinomial Theorem
> $$(x_1 + x_2 + \dots + x_m)^n = \sum_{k_1 + k_2 + \dots + k_m = n} \binom{n}{k_1, k_2, \dots, k_m} \prod_{1 \leq r \leq m} x_r^{k_r}$$

---

# Unordered Arrangements with Repetitions

> [!theorem] Theorem
> The number of ways of choosing $k$ objects from $n$ types of objects (with replacement or repetition allowed) is
> 
> $$\binom{n + k - 1}{k} = \binom{n + k - 1}{n - 1}$$

---

# Formulas for Counting Arrangements and Combinations

|                     | without repetitions                           | with repetitions                         |
|---------------------|-----------------------------------------------|------------------------------------------|
| **Order matters**   | $$ P(n, k) = \frac{n!}{(n-k)!} $$             | $$ n^k $$                                |
| **Order doesn’t matter** | $$ \binom{n}{k} = \frac{n!}{k!(n-k)!} $$ | $$ \binom{n + k - 1}{k} $$               |

