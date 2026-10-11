---
tags:
  - 1stYear
---
# Basic Elements:

> [!abstract] Set
> An unordered  collection of things (not counting multiplicities), its elements.
> **Descriptions:**
> *List* $X = \{x_{1},x_{2},...,x_{n}\}$
> *Rule* $X= \{x|$ some condition on $x$ holds$\}$

> [!abstract] Membership
> $a\in X$ – "$a$ is an element of $X$"
> $\neg(a\in X)\rightleftharpoons a \notin X$
> 
> *$\rightleftharpoons$ means "by definition" 

>[!abstract] Proposition
>A sentence (that declares a fact) that is either *true* or *false*, but not both.

>[!abstract] Predicate $P\{x_1,...,x_{n}\}$
>A sentence with parameters $x_{1} \in D_{1},...,x_{n}\in D_{n}$ (its truth depends on $x_1,...,x_n$)
>
>The set $D_{1}\times ... \times D_{n}$ is called the ***domain*** of $P$

>[!abstract] Quantifiers (some denotions)
>The universal quantifiers|The existential quantifier
>--|--
>"for Any", "for All"|"Exists" 
>$\forall x\ P(x)$|$\exists x \ P(x)$

>[!abstract] Bound and Free occurrence
>- Every occurrence of a variable $x$ in a formula of the form $\exists x \ P(x)$ or of the form $\forall x \ P(x)$ is called a ***bound*** occurrence.
>- Occurrences which are not *bound* are called ***free***.  
>  
>  **Example:**
>  $$P(z)=\exists x ((z\neq x)\rightarrow \forall y((y=z)\vee (y=x)))$$ 
>  Bound: $x,y$
>  Free: $z$

>[!info] Fact
>If a formula does not contain free variables then it becomes a *proposition*. (Its truth still depends on the domain.)

> [!abstract] Interpretation
> An (positive) ***interpretation*** for a formula of predicate logic is possible meanings for domain, predicates and variables such that a truth value of the formula becomes *TRUE*.
> 
> **Example:**
> Let the domain consist of all natural numbers.
> $P(x)=$ "$x$ is even"
> Therefore, $\exists x \ P(x) =$ "There is an even number"  
> 
> Let the domain consist of all natural numbers dividing by 4.
> $P(x) =$ "$x$ is even"
> Therefore, $\forall x\ P(x) =$ "Any natural number dividing by 4 is divided by 2"
> 

>[!abstract] Counterexample
>A counterexample for a formula of predicate logic is possible meanings for domain, predicates and variables such that a truth value of the formula becomes *FALSE*.
>
>**Example:**
>Let the domain consist of all people.
>$P(x) =$ "$x$ can fly"
>Therefore, $\forall x \ P(x) =$ "Anyone can fly"

# De Morgan's Laws:

>[!abstract] Definition by quantifiers
>$\neg \forall x \ P(x)\equiv \exists x \neg P(x)$
>$\neg \exists x \ P(x) \equiv \forall x \neq P(x)$

>[!check]  Interpretation $\neg \forall x \ P(x)\equiv\exists x \neg P(x)$
>Let the domain consist of all natural numbers and $P(x) =$ "$x$ is even".
>$$\forall x\ P(x) = \text{"any natural number is even"}$$ 
>$$\neg \forall x \ P(x) = \text{"not any natural number is even}$$
>$$\exists x \neg P(x) = \text{"there exists a natural number which is not even"}$$
>
>Let the domain consists of all people and $P(x)=\text{"x is a woman"}$
>$$\forall x \ P(x)=\text{"everyone is a woman"}$$
>$$\neg \forall x \ P(x)=\text{"not everyone is a woman"}$$
>$$\exists x \neg P(x)=\text{"there is a person who is not a woman"}$$

>[!check] Interpretation $\neg \forall x \ P(x)\equiv \exists x \neg P(x)$
>Let the domain consists of all natural numbers and $P(x) = \text{"x is a prime number"}$
>$$\exists x\ P(x)=\text{"there exists a prime number"}$$
>$$\neg \exists x \ P(x)=\text{"there does not exist a prime number"}$$
>$$\forall x \neg P(x) = \text{"every natural number is not prime"}$$
>
>Let the domain consists of all people and $P(x)=\text{"x is a rich"}$
>$$\exists x \ P(x)=\text{"Rich people exist"}$$
>$$\neg \exists x \ P(x)=\text{"Rich people do not exist"}$$
>$$\forall x \neg P(x)=\text{"Everyone is not rich"}$$

> [!abstract] Definition by another way
> $\begin{cases}\neg (A \wedge B)\equiv \neg A \vee \neg B  \\
 \neg (A\vee B)\equiv \neg A \wedge \neg B\end{cases}$

# Properties:
> [!example] Some Equivalence and Inequivalence
> $$\forall x\ (P_{1}(x)\wedge P_{2}(x)) \equiv \forall x \ P_{1}(x) \wedge \forall x \ P_{2}(x)$$
> $$\forall x \ (P_{1}(x)\vee P_{2}(x)\not\equiv \forall x \ P_{1}(x) \vee \forall x \ P_{2}(x)$$
> $$\exists x \ (P_{1}(x)\vee P_{2}(x))\equiv \exists x \ P_{1}(x) \vee \exists x \ P_{2}(x)$$
> $$\exists x \ (P_{1}(x)\wedge P_{2}(x))\not\equiv \exists x\ P_{1}(x)\wedge P_{2}(x)$$

# Nested Quantifiers
>[!example] Properties
>$$\forall x\ \forall y \ P(x,y)\equiv \forall y\ \forall x \ P(x,y)$$
>$$\exists x\ \exists y \ P(x,y)\equiv \exists y\ \exists x \ P(x,y)$$
>$$\exists x\ \forall y \ P(x,y)\not \equiv \forall y \ \exists x \ P(x,y)$$ 
>**Explanation:** Left side means that there is at least one $x$ for any $y$, and right side says for any $y$ there is at least one $x$ maybe own for each $y$ or shared for some $y$ in the same time 
>**Example:**
>Let the domain consist of all natural numbers and $$P(x,y)=\textit{"x = y"}$$
>$$\exists x\ \forall y \ P(x,y)=0$$
>$$\forall y\ \exists x \ P(x,y)=1$$

# Special Cases:
>[!abstract] Uniqueness quantifier
>$$\displaylines{\exists !x\ P(x)\rightleftharpoons \ \textit{"there exists a unique x such that P(x)"}=\\\exists x\ \forall y\ [P(x)\wedge (P(y)\rightarrow(y=x))]}$$ 
>**Example:**
>$$\displaylines{\exists ! x \ ((x>0)\wedge (x^{2}=16))=\\
>\exists x \ \forall y [(x>0)\wedge (x^{2}=16) \wedge ((y>0 \wedge y^{2}=16)\rightarrow(y=x))]}$$

>[!abstract] Restricted universal quantifier
>$$\displaylines{\forall  n \ (R(n)) \ P(n)\rightleftharpoons \textit{P(n) for any n such that R(n)}=\\
>\forall n \ (R(n)\rightarrow P(n))}$$
>**Examples:** 
>- $\forall n \leq 5 \ P(n) = \forall n \ (n\leq 5 \rightarrow P(n))$
>- $\forall \epsilon > 0 \ P(\epsilon) = \forall\epsilon\ (\epsilon > 0 \rightarrow P(\epsilon))$
>- $\forall i \in \{1,...,10\} \ P(i)=\forall i \ (i\in \{1,...,10\} \rightarrow P(i))$

>[!abstract] Restricted existential quantifier
>$$\displaylines{\exists n \ (R(n)) \ P(n)\rightleftharpoons \textit{there exists n with R(n) such that P(n)}=\\
>\exists n \ (R(n)\wedge P(n))}$$
>**Examples:**
>- $\exists n \geq 7 \ P(n)$
>- $\exists \delta > 0\ P(\delta)$
>- $\exists i \in \mathbb{N} \ P(i)$