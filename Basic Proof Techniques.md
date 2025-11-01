---
tags:
  - 1stYear
---

# Theorems:
>[!abstract] Theorem $A\to B$ 
>$A$ is called a *sufficient condition* for $B$,
>$B$ is called a *necessary condition* for $A$.

>[!abstract] Theorem $A\leftrightarrow B$ 
>$A$ is called a *sufficient and necessary condition* for $B$.
>$A\leftrightarrow B \equiv (A\to B) \wedge (B\to A)$

---
# Direct proof:

**Basic proof techniques:**
![](Pasted%20image%2020240928231940.png)

>[!abstract] Argument
>A list (series) of sentences (statements) which give reasons for one's conclusion via explanation.
>**Denotions:**
>$$\frac{\phi_{1}, \phi_{2},...,\phi_{n}}{\psi}$$
>$$\phi_{1}, \phi_{2},..., \phi_{n} \models \psi$$
>$\phi_{1},\phi_{2},...,\phi_{n}$ are called *premises*.
>$\psi$ is called a *conclusion*.

>[!abstract] Direct proof
>Given propositions $P_{1}, P_{2}, ..., P_{n}$ we prove $P_{0}$.
>- $P_{1}$  – **Premise**
>$...$
>- $P_{n}$ – **Premise**
>- $P_{n+1}$ (it logically follows from $P_{i_{1}}$ and $P_{j_{1}}$) – **Some method**
>- $P_{n+2}$ (it logically follows from $P_{i_{2}}$ and
>- $P_{j_{2}}$) – **Some method**
>$...$
>---
>- $P_{0}$ (it logically follows from $P_{i_{k}}$ and $P_{j_k}$) – **Conclusion**

**Rules of Inference:**

>[!abstract] Rules Ponens (Law of Detachment)
>- $P\to Q$
>- $P$
>- $Q$

> [!abstract] Contrapositive 
> $\neg Q \to \neg P$
> $P\to Q$

>[!abstract] Hypothetical Syllogism
>$P\to Q$
>$Q \to R$
>$P\to R$

>[!abstract] $\forall$ and $\exists$-rules
>$\forall x P(x)$ – *$\forall$-rule of instantiation*
>$P(c)$ for any $c$
>$P(c)$ for any $c$ – *$\forall$ of generalization*
>$\forall x P(x)$
>$\exists xP(x)$ – *$\exists$-rule of instantiantion*
>$P(c)$ for some $c$
>$P(c)$ for some $c$ – $\exists$-rule of generalization
>$\exists xP(x)$

---
# Contradiction:

$$\frac{(P\wedge \neg Q) \to (X), (P\wedge \neg Q) \to \neg X}{P\to Q}$$
- --
# Induction:

- *Induction Basis / Initial step* $n=n_{0}$
  Prove $P(n_{0})$
  <br>
- *Induction / Inductive Hypothesis*
  Suppose that $P(k)$, $k>n_{0}$
  <br>
- *Induction / Inductive step*
  Prove $P(k+1)$
  <br>
- *Conclusion*
  Therefore, by the Principle of Mathematical Induction, 
  $P(n)$ holds for any $n\geq n_{0}$

>[!abstract] Induction
$$\frac{P(n_{0});\forall k\geq n_{0}\ [P(k) \to P(k+1)]}{\forall n \geq n_{0}\ P(n)}$$


