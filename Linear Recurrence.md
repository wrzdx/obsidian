---
tags:
  - 1stYear
---
# Introduction

> [!definition] Definition (in general)
> **Recursion** or **recurrence** occurs when the definition of a concept or process depends on a simpler version of itself.

$$
F(n) = F(n - 1) + F(n - 2)
$$

$$
F(n + 2) = F(n + 1) + F(n)
$$

---
# Sequences

> [!definition] Definition
> A **sequence** is a function from a subset of the set of natural numbers (typically the set $\{0,1,2,\dots\}$ or the set $\{1,2,3,\dots\}$) to a set.![|500](Pasted%20image%2020241031150505.png)

> [!example] Examples
> 1. $a_n=(-1)^n$, where $n \in \{1,2,3,\dots\}$:
>    Sequence: $-1,1,-1,1,-1,1,\dots$
> --- 
> 2. $a_n=2^n$, where $n \in \mathbb{N} = \{0,1,2,\dots\}$:
>    Sequence: $1,2,4,8,16,32,\dots$

---
## Arithmetic Progression

> [!definition] Definition
> An **arithmetic progression** is a sequence of the form
> 
> $a_0, a_0 + d, a_0 + 2d, \dots, a_0 + nd, \dots$
>$$
a_n = a_0 + nd, \; n \in \mathbb{N}
$$

> [!example] Example
> - $a_n = -10 + 5n$
> 
>   Sequence: $-10, -5, 0, 5, 10, 15, \dots$

---
## Geometric Progression

> [!definition] Definition
> A **geometric progression** is a sequence of the form
> 
> $a_0, a_0 \cdot t, a_0 \cdot t^2, \dots, a_0 \cdot t^n, \dots$

$$
a_n = a_0 \cdot t^n, \; n \in \mathbb{N}
$$

> [!example] Example
> - $a_n = (-2)^n$
> 
>   Sequence: $1, -2, 4, -8, 16, -32, \dots$

---
## Recursively Defined Sequences

> [!definition] Definition
> Say that the $n$-th element of the sequence $\{a_n\}$ is defined **recursively** in terms of the previous elements of the sequence and the initial elements of the sequence.

> [!example] Example
> - Recursively: $a_0 = 1$, $a_{n+1} = a_n + 2$
> - List: $1, 3, 5, 7, \dots$
> - Non-recursively: $a_n = 1 + 2n$

> [!info] Multiplication of the Terms of a Sequence
> 
> $$
> P(n) = \prod_{i=m}^{n} a_i = a_m \cdot a_{m+1} \cdot \dots \cdot a_n
> $$
> 
> The variable $i$ is referred to as the index of summation.
> - $m$ is the **lower limit**,
> - $n$ is the **upper limit**.

> [!note] Recursively
> - $P(m) = a_m$
> - $P(n + 1) = a_m \cdot a_{m+1} \cdot \dots \cdot a_n \cdot a_{n+1} = P(n) \cdot a_{n+1}$

---
# Arithmetic Series

> [!definition] Definition
> The sum of the terms of the arithmetic progression
> 
> $a_0, a_0 + d, a_0 + 2d, \dots, a_0 + nd$
> 
> is called an **arithmetic series**.

> [!theorem] Theorem
> $$
> \sum_{i=0}^{n} (a_0 + id) = n a_0 + d \frac{n(n + 1)}{2}
> $$

---
# Geometric Series

> [!definition] Definition
> The sum of the terms of the geometric progression
> 
> $a_0, a_0 t, a_0 t^2, \dots, a_0 t^n$
> 
> is called a **geometric series**.

> [!theorem] Theorem
> $$
> \sum_{i=0}^{n} (a_0 t^i) = a_0 \frac{t^{n+1} - 1}{t - 1}
> $$

----
# Linear Recurrence Sequences

> [!definition] Definition
> A sequence $a_0, a_1, a_2, \dots$ is called a **linear recurrence (recursive) sequence** (of order $k$), if
> 
> $$
> a_{n+k} = t_1 \cdot a_{n+k-1} + \dots + t_k \cdot a_n = \sum_{i=1}^{k} t_i \cdot a_{n+k-i},
> $$
> 
> where all $t_i$ are fixed coefficients.

> [!example] Example
> $$
> a_{n+2} = a_{n+1} + a_n
> $$


> [!definition] Definition
> A sequence $x_0, x_1, x_2, \dots$ is a (partial) solution of a linear recurrence sequence
> 
> $$
> a_{n+k} = t_1 \cdot a_{n+k-1} + \dots + t_k \cdot a_n,
> $$
> 
> if the recursion holds for $a_n = x_n$.

> [!example] Example
> $$
> a_{n+2} = a_{n+1} + a_n
> $$
> 
> $0, 1, 1, 2, 3, 5, 8, 13, \dots$
> 
> $7, 3, 10, 13, 23, 36, \dots$


> [!definition] Definition
> Let $a_{n+k} = t_1 \cdot a_{n+k-1} + \dots + t_k \cdot a_n$ be a linear recurrence sequence.  
> That is, $a_{n+k} - t_1 \cdot a_{n+k-1} - \dots - t_k \cdot a_n = 0$.  
> Then the character of it is  
> $$
> \chi(\lambda) = \lambda^k - t_1 \lambda^{k-1} - t_2 \lambda^{k-2} - \dots - t_{k-1} \lambda^1 - t_k.
> $$

> [!example] Example
> $$
> a_{n+2} = a_{n+1} + a_n
> $$  
> which leads to  
> $$
> a_{n+2} - a_{n+1} - a_n = 0
> $$  
> The character of this sequence is  
> $$
> \chi(\lambda) = \lambda^2 - \lambda - 1.
> $$


> [!lemma] Lemma
> Let $a_{n+k} = t_1 \cdot a_{n+k-1} + \dots + t_k \cdot a_n$ be a linear recurrence sequence, $\chi(\lambda)$ be its character, and $p$ be a root of $\chi(\lambda)$. Then the sequence  
> $$
> 1, p, p^2, \dots, p^n, \dots
> $$  
> is a solution.

> [!proof] Proof
> Since $p$ is a root of $\chi$, $\chi(p) = 0$, and we have  
> $$
> p^{n+k} - \sum_{i=1}^{k} t_i p^{n+k-i} = p^n \left( p^k - \sum_{i=1}^{k} t_i p^{k-i} \right) = p^n \chi(p) = 0
> $$  
> Therefore,  
> $$
> p^{n+k} = \sum_{i=1}^{k} t_i p^{n+k-i},
> $$  
> i.e., $p^n$ is a solution of the given linear recurrence sequence.

> [!lemma] Lemma
> If sequences $x_0, x_1, x_2, \dots$ and $y_0, y_1, y_2, \dots$ are solutions of a linear recurrence sequence, then  
> $$
> \alpha x_0 + \beta y_0, \alpha x_1 + \beta y_1, \alpha x_2 + \beta y_2, \dots
> $$  
> is also a solution of the linear recurrence sequence.

> [!theorem] Theorem (general solution)
> Let $a_{n+2} = t_1 \cdot a_{n+1} + t_2 \cdot a_n$ and $t_1^2 + t_2 \neq 0$, and $p_1, p_2$ are roots of the character $\chi(\lambda)$. Then
> 
> 1. If $p_1 \neq p_2$ then any solution is $x_n = \alpha \cdot p_1^n + \beta \cdot p_2^n$;
> 2. If $p_1 = p_2$ then any solution is $x_n = (\alpha \cdot n + \beta) \cdot p_1^n$.

> [!example] Example
> For $a_{n+2} = a_{n+1} + a_n$, the character $\chi(\lambda) = \lambda^2 - \lambda - 1$, with roots  
> $$
> p_1 = \frac{1 + \sqrt{5}}{2} \quad \text{and} \quad p_2 = \frac{1 - \sqrt{5}}{2}.
> $$
> Then the general solution is
> $$
> a_n = \alpha \left( \frac{1 + \sqrt{5}}{2} \right)^n + \beta \left( \frac{1 - \sqrt{5}}{2} \right)^n.
> $$

> [!algorithm] Algorithm
> Given the linear recurrence sequence $a_{n+2} = t_1 \cdot a_{n+1} + t_2 \cdot a_n$:
> 
> 1. **Find the character** of the sequence by replacing $a_{n+i} \rightarrow \lambda^i$:
>    $$
>    \chi(\lambda) = \lambda^2 - t_1 \lambda^1 - t_2.
>    $$
> 
> 2. **Find the roots**: $p_1$ and $p_2$.
> 
> 3. **Determine the solution** based on the roots:
>    - If $p_1 \neq p_2$, the solution is $a_n = c_1 \cdot p_1^n + c_2 \cdot p_2^n$.
>    - If $p_1 = p_2$, the solution is $a_n = (c_1 \cdot n + c_2) \cdot p_1^n$.
> 
> 4. **Solve for $c_1$ and $c_2$** using the initial values $a_0$ and $a_1$.

