---
tags:
  - 1stYear
---
$M$ – is a individual number that is equal to sum of the number of your birth day and number of your birth month (i.e., "day" + "month").
# 1) What does Mathematical Analysis study? (Compare with high school algebra.) How do you understand terms “first-order theory” and “second-order theory”? Give examples of the first-, second- and (optionally) third-order statements in Mathematical Analysis.
---
## Mathematical Analysis vs. High School Algebra:

_Mathematical Analysis_ is a branch of mathematics that deals with limits, derivatives, integrals, sequences, and functions. It focuses on understanding the properties of real and complex numbers, exploring how these numbers behave when undergoing operations such as differentiation or integration. Analysis also includes concepts of continuity, convergence, and infinite series. It's essentially the rigorous framework behind calculus, providing the theoretical foundation to explain why various calculus techniques work.

_High School Algebra_, on the other hand, deals with manipulating algebraic expressions and solving equations. It covers topics like polynomials, linear and quadratic equations, systems of equations, and basic properties of numbers. While algebra is more about finding solutions to given problems, analysis goes deeper into understanding the underlying behaviors and theoretical underpinnings.

In short, algebra helps solve equations, whereas analysis helps understand how those solutions behave as part of a broader system, often dealing with infinite processes.

---
## First-order and Second-order Theory:

- A **_first-order theory_** deals with quantifying over elements of a set. In first-order logic, you use quantifiers like "for all" (∀) and "there exists" (∃) to refer to specific elements within a domain. In Mathematical Analysis, first-order theories can be used to describe properties of numbers, sequences, and functions without referring to sets of sets or functions of functions.
---
- A ***second-order theory*** allows quantification over sets, functions, or relations. This means that second-order logic can make statements about properties of entire sets or functions, not just individual elements. It’s more expressive than first-order logic, which allows it to define concepts like completeness in real numbers more formally.
---

**Examples in Mathematical Analysis**:

1. **First-order Statement**:
    
    - $\forall x\in \mathbb{R},\ \exists y\in \mathbb{R}: y>x$
    - This is first-order because it quantifies over individual real numbers.
2. **Second-order Statement**:
    
    - $\forall A\subseteq \mathbb{R},\ (\emptyset \neq A \wedge \exists M\in \mathbb{R},\ \forall a\in A,\ (a\leq M)) \Rightarrow$$\exists \sup A\in \mathbb{R},\ \forall u\in A, (u\leq \sup A)$
    - This is a second-order statement since it talks about properties of sets of real numbers, not just individual elements.
3. **Third-order Statement** (optional):
    
    - Third-order logic would involve quantifying over sets of sets or similar more complex constructions, but in mathematical analysis, such constructs are rarely used directly. An example could be:
    - $\exists A,\ A\subseteq \mathcal{P},\ \exists S \in A,\ (\exists a \in S,\ \exists n \in \mathbb{N},\ (a>n))$
    - Such statements are more abstract and less common, but they push the idea of quantification even further.

---
# 2) Write your own opinion why you as a student of IT-University should/shouldn’t learn/study the second order theory of real numbers? What do you think about a need of theory of limits in IT, Software Engineering, Computer Science, Robotics, and/or Data Science? – Proof a need by example(s) but refute a need with a comprehensive proof.
---
Studying the **second-order theory of real numbers** might seem very complicated and distant from what you usually do in IT, especially in your first year. For most programming or IT tasks, you probably won't need to understand this theory. It's more about **really advanced math** or situations where you need to **prove that a program is 100% correct**, which is not something you often do in regular programming.

However, if you're interested in areas like **robotics** or **machine learning**, where precise calculations and system control are important, these concepts can be useful. In those fields, understanding more abstract ideas helps to figure out how and why certain systems work mathematically.

---

Now, about the **theory of limits** — this is something that's definitely useful in many areas of IT:

1. In **programming** and **algorithms**, you often need to understand how a program behaves when it processes more and more data. Limits help you figure out how fast the program will run as it scales up.

2. In **machine learning**, limits help you understand how algorithms learn from data — they show when the learning process "finishes" and you get the best possible result.

3. In **robotics**, limits are used to calculate how robots move and make sure their movements are stable.
---
**My conclusion:**

- **Studying second-order theory** is only useful if you're planning to get into really complex fields like program correctness proofs or advanced mathematical modeling.
- **Studying limits** is important for everyone because it applies to a lot of IT fields, especially in tasks involving calculations and analyzing algorithms.
---
# 3) What is naïve set theory and why we need to learn it in Mathematical Analysis? Could you please present 2-3 its postulates and explain? Is any collection a set (according to the naïve set theory)? Prove that union and intersection of any three sets is a set again. Can you prove that Cartesian product of any two sets is a set too? – If you cannot, then try to prove that Cartesian product of any two finite sets is a set.
---
## What is Naive Set Theory and Why do we need to learn it in Mathematical Analysis?

**Naïve set theory** is a simple, intuitive way to think about sets — collections of objects, like numbers or other elements. It doesn’t involve the more complex and abstract formalizations you’ll find in advanced set theory, making it easier for beginners to grasp. In mathematical analysis, **sets** are fundamental because they help define almost everything: functions, sequences, numbers, and more. By understanding how sets work, you can better understand more advanced topics like limits, continuity, and convergence.

---
## 2-3 Postulates of Naive Set Theory:

1) **Existence of Sets:**
   - Any collection of distinct objects can form a set. For example, the set of natural numbers $\{1,2,3,4,...\}$ is a collection of numbers.
2) **Extensionality:**
   - Two sets are equal iff they have the same elements. For example, $\{1,2,3\}$ is the same as $\{3,2,1\}$ because they contain the same elements.
3) **Union and Intersection:**
   - The **union** of two or more sets is a set that contains all elements from those sets.
   - The **intersection** of two or more sets is a set that contains only the elements that are in all of the sets.
---
## Is any collection a set in Naive Set Theory?

In **naïve set theory**, we typically assume that any collection of objects can be considered a set. However, this assumption leads to certain paradoxes, like Russell's Paradox, where a set can end up "containing itself."

### The Rassell's Paradox:

In naïve set theory, we assume that **any collection of objects can be a set**. Russell’s paradox arises when we try to define a set in a way that leads to a contradiction.

Let’s consider the following:

1. Suppose there is a set **R** that contains all sets that **do not contain themselves**. In symbols:
   $$R=\{X\ | \ X\not \in X\}$$
   This means that $R$ contains all sets $x$ such that $x$ is **not a member of itself**.
2. Now, the paradoxical question is: **Is $R$ a member of itself?**
   - If $R\in R$, then by definition of $R$, it should not contain itself. So, $R\not \in R$.
   - But if $R \not \in R$, then by the same definition, it must contain itself, meaning $R\in R$.

This creates a **contradiction:** both possibilities lead to a contradiction, meaning $R\in R$ and $R\not \in R$ are both false and true at the same time, which is logically impossible.

---
## Proof: Union and Intersection of Three Sets is a Set

Let's prove that the **union** and **intersection** of three sets is still a set.

**Union:**
	Given three sets $A,B$ and $C$, the union is the set of elements that belongs to at least one of the sets:
	$$A\cup B\cup C = \{x\ | \ x\in A \vee x\in B\vee x\in C\}$$
	Since each of the sets $A,B$ and $C$ is a set, their union is   also a set according to the union postulate in Naive Set Theory.

**Intersection:**
	Similarly, the intersection of three sets $A,B$ and $C$ is the set of elements that belong to all three sets:
	$$A\cap B \cap C = \{x\ |\ x\in A \wedge x\in B \wedge x \in C\}$$
	The result is also a set, as intersection preserves the "setness" of the elements involved.

---
## Cartesian Product of two sets is a set:

The Cartesian Product of two sets $A$ and $B$ is the set of all ordered pairs $(a,b)$, where $a \in A$ and $b\in B$. We need to show that this Cartesian Product is also a set.

Formally, the Cartesian product is defined as:
$$A\times B = \{(a,b) \ | \ a\in A,\ b\in B\}$$
Since both $A$ and $B$ are sets, and each pair $(a,b)$ is defined by elements of $A$ and $B$, the Cartesian product is a well-defined collection of these pairs, and according to naive set theory, it is also a set.

## Cartesian Product of Finite Sets

If $A$ and $B$ are finite sets, their Cartesian product is even easier to prove as a set because there is a finite number of ordered pairs, and a finite collection of things can always be considered a set in Naive Set Theory.

For example, if $A = \{1,2\}$ and $B=\{a,b\}$, the Cartesian product is:
$$A\times B = \{(1,a),(1,b),(2,a),(2,b)\}$$
This is clearly a finite set with four elements, which is always a set in naive set theory.

---
## Conclusion:

Naive set theory provides a simple framework to understand collections of objects and how they interact. While it's not free of logical issues (like Russell's Paradox), it's still an essential tool in mathematical analysis. The union, intersection, and Cartesian products of sets are all basic operations that are key to defining more complex mathematical structures in fields like IT, computer science, and robotics.

---

# 4) Construct the set representation for natural numbers $0,1,2,3$ and prove by construction that these representations are sets indeed. Prove that set-theoretic representation $S$ of your individual number $M$ is a set indeed. What is cardinality of $S$? What is cardinality of $2^S$?
---
## Set-Theoretic Representation of Natural Numbers

We can define each natural number $n$ as:
$$n=\{n-1,\{n-1\}\}$$
where $n-1$ is the previous number.

Let's construct the first few natural numbers using this method:
1. $0$ (the vase case):
   $$0=\emptyset$$
2. $1$:
   $$1=\{0,\{0\}\} = \{\emptyset , \{\emptyset\}\}$$
3. $2$:
   $$2 = \{1,\{1\}\} = \{\{\emptyset , \{\emptyset\}\},\{\{\emptyset , \{\emptyset\}\}\}\}$$
4. 3:
   $$3 = \{2,\{2\}\} = \{\{1,\{1\}\},\{\{1,\{1\}\}\}\}$$
### Prove These Representations Are Sets:

According to naive set theory, any collection of sets is itself a set. We know that the empty set $\emptyset$ is a valid set. Since each subsequent number is built from previously defined sets, each natural number is indeed a set.

By **induction**:
- Base case: $0=\emptyset$ is a set by definition.
- Inductive step: If $n-1$ is a set, then $n=\{n-1,\{n-1\}\}$ is also a set, because it's the union of two sets (the previous number and a set containing the previous number).

Thus, each natural number $n$ constructed in this way is indeed a set.

---
## Set-Theoretical Representation of $M$

In my case, $M$ is equal to $24 + 10 =34$. So, according to the given method, $M=34$ is built recursively from $33$ down to $0$.
$$34 = \{33,\{33\}\}$$
This means that $34$ is a set containing two elements: the set representation of $33$, and the set that contains $33$.

---
## Cardinality of $S$

The cardinality of a set is the number of elements it contains. Since every number $n$ in this construction has exactly two elements – its predecessor (previous element) and the set containing its predecessir – the cardinality of $S$, where $S = 34$, is $2$.

---
## Cardinality of $2^S$ (Power Set of $S$)

The power set $2^{S}$ is the set of all subset of $S$. If a set has $n$ elements, its power set contains $2^{S}$ subsets.

Since $S = 34$ has $2$ elements, the power set $2^S$ has:
$$|2^S | = 2^2 = 4$$
Thus, the cardinality of $2^S$ is $4$.

---
## Conclusion:

We can represented natural numbers as sets with exactly two elements, providing that these representations are indeed sets. The set $S =34$ has a cardinality of $2$, and its power set $2^{S}$ has a cardinality of $4$.

---
# 5) Find the largest number $m\in \mathbb{N}$ that is not greater than $(M+24)$ such that $\sqrt{m}$ is irrational (and prove the irrationality).
---
## Step 1: Compute $M+24$

Given that $M=34$, we calculate:
$$M+24 = 34 + 24 = 58$$
So, we are looking for the largest $m\in \mathbb{N}$ such that $m\leq 58$ and $\sqrt{m}$ is irrational.

---
## Step 2: Identify Perfect Squares Less Than or Equal to $58$:

To determine which numbers have irrational square root, we first list the perfect squares less than or equal to $58$. The perfect squares are:
$$1^2 = 1,\ 2^2 = 4,\ 3^2 = 9,\ 4^2 = 16,\ 5^2 = 25,\ 6^2 = 36, \ 7^2 = 49$$
These numbers have rational square roots because the square root of a perfect square is always a natural number.

---
## Step 3: Find the Largest Non-Perfect Square $m\leq 58$

Now, we search for the largest $m$ such that $\sqrt{m}$ is irrational. Irrational square roots occur whem $m$ is not a perfect square. The perfect squares less than or equal to $58$ are:
$$1,\ 4,\ 9,\ 16,\ 25,\ 36,\ 49$$
The largest number less than or equal to 58 that is not a perfect square is:
$$m = 58$$
---
## Step 4: Prove the Irrationality of $\sqrt{58}$

To prove that $\sqrt{58}$ us irrational, we use a common method: the **contradiction approach**.

### Proof by Contradiction:

1. Assume that $\sqrt{58}$ is rational. By definition, this means we can write:
   $$\sqrt{58} = \frac{p}{q}$$
   where $p$ and $q$ are coprime integers (i.e., their greatest common divisor is $1$), and $q\neq 0$.
   ---
2. Squaring both sides gives:
   $$58 = \frac{p^2}{q^2}$$
   Multiplying both sides by $q^{2}$ gives:
   $$58q^2 =p^2 $$
   This equation states that $p^{2}$ is divisible by $58$. Therefore, $p$ must also be divisible by $58$ (because if a prime number divides $p^{2}$, it must divide $p$).
---
3. Let $p = 58k$ for some integer $k$. Substituting this back into the equation gives:
   $$58q^2 = (58k)^2 = 58^2k^2$$
   Dividing both sides by $58$ gives:
   $$q^2 = 58k^2$$
   This equation implies that $q^{2}$ is divisible by $58$, and thus $q$ must also be divisible by $58$.
   ---
4. But if both $p$ and $q$ are divisible by $58$, this contradicts out assumption that $p$ and $q$ are copime (i.e., their greatest common divisor is $1$).

Thus, our original assumption that $\sqrt{58}$ is rational must be false. Therefore, $\sqrt{58}$ is irrational.

---
## Final Answer:

The largest number $m \leq 58$ such that $\sqrt{m}$ is irrational is $58$.

---
# 6) Using Tarski axiomatization for reals, find the first 5 digits in binary representation of a rational number corresponding to ratio $\displaystyle \frac{M}{46}$. (Explain your answer!)
---
I didn't get this question.

---
# 7) Does $\displaystyle (2+ \frac{(-1)^{n}M}{\sqrt{n+1}})_{n\in \mathbb{N}}$ has a limit? Prove your answer using the definition of the sequence's limit.
---
## Step 1: Analyze the General Behavior of the Sequence 

The sequence has two main parts:

1. The constant $2$.
2. The term $\frac{(-1)^{n}M}{\sqrt{n+1}}$

Let's break down the second term $\frac{(-1)^{n}M}{\sqrt{n+1}}$:
- $(-1)^{n}$ alternates between $1$ and $-1$, depending on whether $n$ is even or odd.
- $\frac{M}{\sqrt{n+1}}$ is a fraction where the numerator is the constant $M=34$ and the denominator $\sqrt{n+1}$ grows larger as $n$ increases.

As $n\to \infty$, $\sqrt{n+1}\to \infty$, so $\frac{M}{\sqrt{n+1}}\to 0$. This means that the magnitude of the term $\frac{(-1)^{n}M}{\sqrt{n+1}}$ gets smaller and smaller as $n$ increases, approaching $0$, but the sign alternates.

---
## Step 2: Determine the Limit

Now, using the above analysis, we can conclude the following:

- As $n\to \infty$, the term $\frac{(-1)^{n}M}{\sqrt{n+1}}$ approaches $0$.
- The constant $2$ remains unaffected by $n$.

Thus, the sequence behaves like $2+0 = 2$ as $n \to \infty$.

---
## Step 3: Prove using the definition of a sequence's limit

The definition of the limit of a sequence says that a sequence $a_{n}$ converges to a limit $L$ if, for every $\varepsilon>0$, there exists an $m\in \mathbb{N}$ such that for all $n \geq m$, we have:
$$|a_n - L| < \varepsilon$$
We claim that the sequence $a_{n}$ converges to $2$, so we will use $L = 2$.

We need to show that for every $\varepsilon>0$, there exists an $m$ such that for all $n \geq m$, the difference berween $a_{n}$ and $2$ is 
less than $\varepsilon$:
$$|a_n -2 | = |2+ \frac{(-1)^n M}{\sqrt{n+1}}-2| = |\frac{(-1)^n M}{\sqrt{n+1}}|$$
We know that:
$$\frac{(-1)^n M}{\sqrt{n+1}} = \frac{M}{\sqrt{n+1}} = \frac{34}{\sqrt{n+1}}$$
As $n\to \infty$, $\frac{34}{\sqrt{n+1}}\to 0$, so for any $\varepsilon>0$, we need to find $m$ such that:
$$\frac{34}{n+1}< \varepsilon$$
This is equivalent to:
$$\sqrt{n+1}> \frac{34}{\varepsilon}$$
Squaring both sides:
$$n+1 > \frac{1156}{\varepsilon^{2}}$$
Thus, we need:
$$n> \frac{1156}{\varepsilon^{2}} - 1$$
Let $m = \lceil \frac{1156}{\varepsilon^{2}}\rceil-1\ (\lceil\rceil$ – ceiling$)$. Then, for all $n \geq m$, we have:
$$|a_{n}-2| < \varepsilon$$
---
## Conclusion

By the definition of the limit of a sequence, we have shown that $\displaystyle \lim_{n\to \infty}a_{n}=2$. Therefore, the sequence
$$a_{n} = 2 + \frac{(-1)^{n}M}{\sqrt{n+1}}$$
converges to $2$.

---
# 8) Does $\displaystyle(n- \frac{M}{n+1})_{n\in \mathbb{N}}$ has a real limit? – Prove your answer using Cauchy's test. Does the sequence have a limit? – Prove your answer using the appropriate definition.
---
Let’s consider the sequence $a_n = n - \frac{M}{n+1}$, where $M = 34$.

## Prove using Cauchy's test

To apply **Cauchy's criterion**, we need to check if, for any $\epsilon > 0$, there exists $N \in \mathbb{N}$ such that for all $n, m > N$, the following holds:

$$
|a_n - a_m| < \epsilon.
$$

Let’s calculate the difference between two terms of the sequence $a_n$ and $a_m$:

$$
|a_n - a_m| = \left| \left( n - \frac{34}{n+1} \right) - \left( m - \frac{34}{m+1} \right) \right|.
$$

As $n$ and $m \to \infty$, the terms $\frac{34}{n+1}$ and $\frac{34}{m+1}$ approach 0, so for large $n$ and $m$, this difference simplifies to:

$$
|a_n - a_m| \approx |n - m|.
$$

Clearly, $|n - m|$ can grow large as $n$ and $m$ increase. Therefore, the sequence **fails Cauchy's criterion** because the difference between terms does **not** become arbitrarily small.

### Conclusion (Cauchy's Test):
The sequence **does not satisfy Cauchy's criterion**, so it does not converge.

---

## Prove using the definition of the sequence's limit

Let’s consider the sequence $a_n = n - \frac{M}{n+1}$, where $M = 34$.

### Formal Definition of a Limit

A sequence $(a_n)$ converges to a real number $L$ if, for every $\epsilon > 0$, there exists an $N \in \mathbb{N}$ such that for all $n > N$, the following holds:

$$
|a_n - L| < \epsilon.
$$

In our case, we want to show that the sequence $a_n = n - \frac{34}{n+1}$ does **not** converge to any real number $K$.

---

### Step 1: Assume the sequence converges to a limit $K$

Suppose that the sequence $\left( n - \frac{34}{n+1} \right)$ converges to some real number $K$. This means that for every $\epsilon > 0$, there exists $N \in \mathbb{N}$ such that for all $n > N$, we have:

$$
\left| n - \frac{34}{n+1} - K \right| < \epsilon.
$$

---

### Step 2: Analyze the behavior of $a_n$

Let’s rewrite the sequence $a_n = n - \frac{34}{n+1}$ in a simplified form for large $n$. As $n \to \infty$, $\frac{34}{n+1} \to 0$, so for large $n$, the sequence behaves like:

$$
a_n \approx n.
$$

This implies that for large $n$, the sequence grows without bound.

---

### Step 3: Proof by contradiction

Since the sequence behaves like $n$ for large $n$, we can make the difference $|a_n - K|$ arbitrarily large by choosing sufficiently large $n$. Specifically, for any $K$, we can choose $n$ such that:

$$
\left| n - K \right| > \epsilon.
$$

Thus, for any $K \in \mathbb{R}$ and for any fixed $\epsilon > 0$, there exists an $n$ such that:

$$
|a_n - K| = \left| n - \frac{34}{n+1} - K \right| \geq |n - K| > \epsilon.
$$

This violates the formal definition of convergence, which requires $|a_n - K| < \epsilon$ for all $n > N$ and some $N \in \mathbb{N}$.

---

### Conclusion

Since for any $K \in \mathbb{R}$, we can find a large enough $n$ such that $|a_n - K|$ exceeds $\epsilon$, the sequence $\left( n - \frac{M}{n+1} \right)$ does **not** converge to any real number $K$.

Therefore, the sequence **does not have a real limit** and diverges to infinity.

---
# 9) Given any real sequence $(a_{n})_{n\in \mathbb{N}}$, we knowing that $\displaystyle \lim_{n\to \infty} \frac{a_{n}-M}{a_{n}+M}=0$, prove or disprove convergence of the sequence (and find $\displaystyle \lim_{n\to \infty}a_{n}$ in case of convergence).
---
## Proof
1. **From the condition:** Since 
$$
\lim_{n \to \infty} \frac{a_n - M}{a_n + M} = 0,
$$ 
it means that for any $\epsilon > 0$, there exists an $N \in \mathbb{N}$ such that for all $n > N$ we have 
$$
\left| \frac{a_n - M}{a_n + M} \right| < \epsilon.
$$

2. **Expand the modulus:** From the above inequality, we get 
$$
|a_n - M| < \epsilon |a_n + M|.
$$ 
This inequality indicates that the numerator $a_n - M$ approaches zero faster than the denominator $a_n + M$ increases.

3. **Denominator is not zero:** We know that for sufficiently large $n$, the value $a_n + M$ is not equal to zero, since the limit condition implies that $a_n + M$ remains positive (or negative) and cannot approach zero. This means there exists a constant $c > 0$ such that for all $n > N$: 
$$
|a_n + M| > c.
$$

4. **Upper bound for the numerator:** Thus, from the previous inequality, we can write:
$$
|a_n - M| < \epsilon |a_n + M| < \epsilon c,
$$
where $c$ is a positive constant and $\epsilon$ is any positive number.

5. **Conclusion:** Since $\epsilon$ can be made arbitrarily small, this implies that $|a_n - M|$ approaches zero, or:
$$
\lim_{n \to \infty} a_n = M.
$$

6. **Final remark:** Therefore, we have proven that the sequence $(a_n)_{n \in \mathbb{N}}$ converges to $M$.
---
# 10) Let $a_{0}=1,\ a_{1}= 2$ and $a_{n+2} = \frac{a_{n}+(M-1)\times a_{n+1}}{M}$ for all natural $n$. Is this sequence monotone, antimonotone, converging? Prove your answer using any theory covered in the lectures.
---
### Proof Using Cauchy Criterion

To use the Cauchy criterion, we need to show that for any $\varepsilon > 0$ there exists $N \in \mathbb{N}$ such that for all $m, n > N$ the following holds:
$$
|a_m - a_n| < \varepsilon.
$$

Consider the sequence $a_n$, defined by the recurrence relation:
$$
a_{n+2} = \frac{a_n + (M - 1)a_{n+1}}{M}.
$$

#### Step 1: Show the Difference Between Consecutive Terms

First, we can express the difference between consecutive terms of the sequence:
$$
d_n = a_{n+1} - a_n.
$$
Using the recurrence relation, we have:
$$
d_{n+1} = a_{n+2} - a_{n+1} = \frac{a_n + (M - 1)a_{n+1}}{M} - a_{n+1}.
$$

This can be simplified to:
$$
d_{n+1} = \frac{a_n + (M - 1)a_{n+1} - Ma_{n+1}}{M} = \frac{a_n - a_{n+1}}{M}.
$$
Thus, we have:
$$
d_{n+1} = \frac{d_n}{M}.
$$

#### Step 2: Analyze the Sequence of Differences

Starting from the initial conditions, we see that:
- $d_0 = a_1 - a_0 = 2 - 1 = 1$.
- $d_1 = a_2 - a_1 = \frac{1 + (34 - 1) \cdot 2}{34} - 2$ (using $M = 34$).

By continuing this process, we can see that:
$$
d_n = \frac{d_0}{M^n} = \frac{1}{M^n}.
$$

#### Step 3: Show that $d_n \to 0$

As $n \to \infty$, $d_n = \frac{1}{M^n} \to 0$ because $M^n$ grows without bound. This shows that the difference between consecutive terms approaches zero:
$$
a_{n+1} - a_n \to 0 \text{ as } n \to \infty.
$$

#### Step 4: Generalize to Arbitrary Terms

Now, for arbitrary terms $a_n$ and $a_{n+k}$, we can express the difference as:
$$
a_{n+k} - a_n = (a_{n+k} - a_{n+k-1}) + (a_{n+k-1} - a_{n+k-2}) + \ldots + (a_{n+1} - a_n).
$$

As $n \to \infty$, each of these differences tends to zero. Therefore:
$$
|a_{n+k} - a_n| < \varepsilon \text{ for sufficiently large } n.
$$

#### Conclusion

Thus, we can conclude that for any $\varepsilon > 0$, there exists an $N$ such that for all $m, n > N$:
$$
|a_m - a_n| < \varepsilon.
$$

Therefore, by the Cauchy criterion, the sequence $(a_n)$ is convergent.

---
# 11) An open set of reals is any set that contains a neighborhood of each of its points. A closed set is the set-theoretic complement in $\mathbb{R}$ of an open set. Draw (sketch) on the real axis the following sets: a) $|x+M| <2$ b) $|2x-2|\geq M$ c) $M-1 \leq |x+M| < M$. Which of these sets are open, close or are neither open nor closes? Prove your answer.
---
1. **a) $|x + M| < 2$**

This inequality can be rewritten as:

$$-M - 2 < x < 2-M$$

This represents the open interval $(-M - 2, - M + 2)$, where all points within this interval are less than 2 units away from $M$.

![](Pasted%20image%2020241006115845.png)

**Classification**:  
- This set is **open** because for any point $x \in (-M - 2, -M + 2)$, we can find a small neighborhood around $x$ that still lies within the interval. By definition, open intervals are open sets.

---

2. **b) $|2x - 2| \geq M$**

Rewriting this inequality gives:

$$|2(x - 1)| \geq M \quad \Rightarrow \quad |x - 1| \geq \frac{M}{2}$$

This means $x$ is at least $\frac{M}{2}$ units away from $1$, leading to two cases:

$$x \leq 1 - \frac{M}{2} \quad \text{or} \quad x \geq 1 + \frac{M}{2}$$

This represents the union of two **closed** intervals: $(-\infty, 1 - \frac{M}{2}] \cup [1 + \frac{M}{2}, \infty)$.

![](Pasted%20image%2020241006120618.png)
**Classification**:  
- This set is **closed** because it is the complement of the open interval $(1 - \frac{M}{2}, 1 + \frac{M}{2})$. 

---

3. **c) $M - 1 \leq |x + M| < M$**

This inequality can be broken into two parts:

1. $M - 1 \leq |x + M|$ gives two cases:
   - $x + M \geq M - 1$ or $x + M \leq -(M - 1)$, which simplifies to:
     $$x \geq -1 \quad \text{or} \quad x \leq -2M + 1$$
     This gives the set $(-\infty, -2M + 1] \cup [-1, \infty)$.
   
2. $|x + M| < M$ also gives two cases:
   - $-M < x + M < M$, which simplifies to:
     $$-2M < x < 0$$
     This gives the interval $(-2M, 0)$.

Combining both parts, the final set is $(-2M, -2M + 1] \cup [-1, 0)$.
![](Pasted%20image%2020241006123050.png)

**Classification**:  
- This set is **neither open nor closed** because it includes a combination of open and closed intervals. Specifically, $(-2M, -2M + 1]$ is closed at one end and open at the other, while $[-1, 0)$ is similarly a mix of open and closed.

---

**Summary of Results**:

1. **a) $|x - M| < 2$**: **Open** set.
2. **b) $|2x - 2| \geq M$**: **Closed** set.
3. **c) $M - 1 \leq |x + M| < M$**: **Neither open nor closed**.

---
# 12) Indicate which of the following sequence does converge and what is the limit in this case? Prove your answer for these sequences using any theory covered in the lectures.
---
a. $\displaystyle ((1+ \frac{1}{n/M})^n)_{n\in \mathbb{N}, n>0}$
b. $\displaystyle ((1+ \frac{1}{n})^{n/M})_{n\in \mathbb{N}, n>0}$
c. $\displaystyle ((1+ \frac{1}{Mn})^{n^2})_{n\in \mathbb{N}, n>0}$

---
### a. $((1 + \frac{1}{\frac{n}{M}})^{n})_{n \in \mathbb{N}, n > 0}$

We can start by rewriting the sequence as:

$$
(1 + \frac{1}{n/M})^n.
$$ 

Now, we can express this as:

$$
\left(1 + \frac{1}{n/M}\right)^n = \left[\left(1 + \frac{1}{n/M}\right)^{n/M}\right]^M.
$$ 

As \(n\) approaches infinity, the inner expression approaches the well-known limit:

$$
\lim_{n \to \infty} \left(1 + \frac{1}{n}\right)^{n} = e.
$$ 

Thus, we conclude that:

$$
\lim_{n \to \infty} \left(1 + \frac{1}{n/M}\right)^{n} = e^M.
$$

**Limit**: $e^{M}$.

---

### b. $((1 + \frac{1}{n})^{\frac{n}{M}})_{n \in \mathbb{N}, n > 0}$

Next, we analyze the sequence:

$$
\left(1 + \frac{1}{n}\right)^{\frac{n}{M}}.
$$ 

This can be rewritten as:

$$
\left[\left(1 + \frac{1}{n}\right)^{n}\right]^{\frac{1}{M}}.
$$ 

Again, as \(n\) approaches infinity, we recognize:

$$
\lim_{n \to \infty} \left(1 + \frac{1}{n}\right)^{n} = e.
$$ 

This leads us to:

$$
\lim_{n \to \infty} \left(1 + \frac{1}{n}\right)^{\frac{n}{M}} = e^{\frac{1}{M}}.
$$ 

We see that the limit here is dependent on \(M\), illustrating how the exponent influences the convergence.

**Limit**: $e^{\frac{1}{M}}$.

---

### c. $((1 + \frac{1}{Mn})^{n^2})_{n \in \mathbb{N}, n > 0}$

Finally, we examine the sequence:

$$
\left(1 + \frac{1}{Mn}\right)^{n^2}. 
$$ 

We can rewrite it as:

$$
\left[\left(1 + \frac{1}{Mn}\right)^{Mn}\right]^{\frac{n^2}{Mn}}.
$$ 

As \(n\) approaches infinity, we utilize the limit:

$$
\lim_{n \to \infty} \left(1 + \frac{1}{Mn}\right)^{Mn} = e.
$$ 

However, we must also consider the exponent:

$$
\frac{n^2}{Mn} = \frac{n}{M}.
$$ 

As \(n\) grows large, this exponent tends to infinity:

$$
\lim_{n \to \infty} e^{\frac{n}{M}} \to \infty.
$$ 

Thus, this sequence diverges.

**Limit**: $\infty$.

---

### Summary of Convergence and Limits

- **Sequence a**: Converges to \(e^{M}\).
- **Sequence b**: Converges to \(e^{\frac{1}{M}}\).
- **Sequence c**: Diverges to \(\infty\).
