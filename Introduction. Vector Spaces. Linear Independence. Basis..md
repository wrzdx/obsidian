---
tags:
  - 1stYear
---
# Material:
- [Lecture](2024_AGLA1_Lecture_1.pdf)
# Body:

**Notation:**
- **Points** are capital italic letter - *A, B...*
- **Scalars** are Greek letters - $\alpha,\beta$.., and sometimes
  Latin letters - a,b..
- **Vectors** are **bold** - **a,b..**, and also $\vec{a},\ \vec{b}$..
- $\mathbb{R}$ is the set of **real** numbers
- $\mathbb{C}$ is the set of **complex** numbers
## Points and Vectors.
- **Vector** is all directed line segments sharing the same direction and length.
- The length of a vector - $|\vec{a}|$ 
- *Unit vector* **$\hat{u}$** = $\frac{\vec{V}}{|V|}$
  It's a "mini-vector" with magnitude (length) 1 that needs to represent any vector with same direction as unit vector with some coefficient ^cdc541
- $\begin{bmatrix}3& 4\end{bmatrix}^{\top} = \begin{bmatrix}3\\4\end{bmatrix}$ 
## Vector Addition. Scalar Vector Multiplication.
## Properties of Vector Arithmetic.
## Vector spaces, Subspaces.
- Vector space $V$ over $\mathbb{R}\ (or \ \mathbb{C})$ is a collection of vectors, together with two operations:
	- $a+b$, addition of two vectors and
	- $\lambda a$, multiplication by scalar ($\lambda \in \mathbb{R}$)
	
- A scalar is a number from $\mathbb{R}\ or\ \mathbb{C}$, respectively.
  
- Addition and multiplication SHOULD satisfy following axioms:
	- Addition:
		1. $a + b = b + a$ (commutativity)
		2. $(a + b) + c = a + (b + c)$ (associativity)
		3. There is a vector $0$ (zero vector) such that $a + 0 = a.$ (identity)
		4. For each vector a, there exists a vector (-a) such that $a + (-a) = 0$ (inverse)
	- Multiplication:
		1. $\lambda(a + b) = \lambda a + \lambda b.$
		2. $(\lambda + \mu)a = \lambda a + \mu a.$
		3. $\lambda(\mu a) = (\lambda\mu)a = \mu(\lambda)a$
		4. $1a = a \ (here \ \lambda = 1).$
- $W$ is a subspace of $V$ if:
	1. $W \subset V$ (subset)
	2. $u,v \in W \Rightarrow u + v \in W$ (closure under addition)
	3. $u \in W,\ \lambda \in \mathbb{R} \Rightarrow \lambda u \in W$ (closure under scalar multiplication)
## Span, Linear Independence.
- Vector $w\in V$ is a linear combination of vectors $v_{1}, ... ,v_{n} \in V$ with coefficients $c_{k}\in \mathbb{R};\ (k = 1..n)$ such that: $$w = c_{1}v_{1}+c_{2}v_{2} +\ ...\ + c_{n}v_{n} = \sum^{n}_{k=1}c_{k}v_{k} $$
- Let $S = \{v_{1},\ v_{2},...,\ v_{n}\}\subset V.$ $$span(S) = \{w\in V : w = \sum^{n}_{k=1}c_{k}v_{k}, \ \forall c_{k} \in \mathbb{R}\}$$
- **Linearly independent vectors** in $\mathbb{R}^{n}$, where $n\in\mathbb{N}$
	- Vectors $v_{1},\ v_{2},...,\ v_{n}$ are *linearly independent* if for $\lambda_{1},\ \lambda_{2},...,\ \lambda_{n}\in\mathbb{R},\ \lambda_{1}v_{1} + \lambda_{2}v_{2} +\ ...\ + \lambda_{n}v_{n} = 0$ if and only if $\lambda_{1}=\lambda_2=...=\lambda_{n}=0.$ 
## Vector Bases and Vector Coordinates in Basis.
- **Basis** of a vector space is a set of vectors that spans a vector space and that is *linearly independent*.
- Let $V$ be a vector space over $\mathbb{R}^{n}$ and let $\{e_{1},...,\ e_{n}\}$ be a basis.
  Then each vector $u$ can be identified with its coordinates $\{u_{1}, ...,\ u_{n}\}$ in the basis. $$u = \sum^{n}_{k=1}u_{k}e_{k}$$$$u = \begin{bmatrix}
  u_{1}\\ 
  u_{2}\\
  ...\\
  u_{n}
  \end{bmatrix}$$
## Linear dependency / independency. Basis.
### Lemma: 

^54060e

- For the linear dependency of the vectors $\vec{a_1},\vec{a_2},...\vec{a_n}$ It's sufficient and necessary to have one of them as a linear combination of the others. ^288eaa

**Proof:** ^513663
1. **Necessity:** Let $\vec{a_{1}},...,\ \vec{a_{n}}$ - linearly dependent $\Rightarrow \exists$ the set of scalars $\lambda_{1},...,\lambda_{n}$ not equal to 0 simultaneously such that: $$\sum^{n}_{i=1}d_{i}\vec{a}_{i}=0\Leftrightarrow\lambda_{1}\vec{a}_{1}+\ ...\ + \lambda_{n}\vec{a}_{n}=0$$$$\vec{a}_{1}+\frac{\lambda_{2}}{\lambda_{1}} \vec{a}_{2}+\ ...\ +\frac{\lambda_{n}}{\lambda_{n}} \vec{a}_{n} = 0 \Rightarrow \vec{a}_{1}=\sum^{n}_{k=2}(-\frac{\lambda_{k}}{\lambda_{1}}\vec{a}_{k})\ \blacksquare$$
 >Есть ли один из векторов можно представить суммой остальных, то мы можем получить нулевой вектор без тривиального случая. Значит, эти вектора линейно зависимы.
2. **Sufficiency:** Let $\vec{a}_{1}= \sum^{n}_{i=2}\lambda_{i}\vec{a}_{i}$ then $(-1)\vec{a}_{1} + \lambda_{2}\vec{a}_{2} +\ ...\ + \lambda_{n}\vec{a}_{n}=0$, $|-1| + |\lambda_{2}| +\ ...\ + |\lambda_{n}|>0$ - This is a non-trivial case $\rightarrow$ $\vec{a}_{1}+\ ... \ \vec{a}_{n}$ is linearly dependent.
> Не все $\lambda$ равны 0, значит, это не *тривиальный случай*, а если есть другая комбинация для получения 0, то такие векторы линейно зависимы.
> $|\lambda_{1}|+\ ...\ + |\lambda_{n}| > 0$ is the triviality condition.
### Theorem 1:
- Given the basis {$\vec{g_{1}},\ \vec{g_{2}}, \ \vec{g_3}$}, then any vector $\vec{x}$ can be represented by $\vec{x} = \xi_1\vec{g_{1}} + \xi_2\vec{g_{2}}+\xi_3\vec{g_3}$ , where $\xi_{1}, \xi_{2}, \xi_3$ - scalars, moreover - uniquely.
**Proof:** 
![Proof|360](Pasted%20image%2020240908203938.png)
Let us first **prove the existence** of such numbers.
Let $\vec{x} = \vec{z}+\vec{y}$, then $\vec{z}||\vec{g}_{3}\Rightarrow\vec{z}=\xi_{3}\vec{g}_{3}$
$\vec{y}=\xi_{1}\vec{g}_{1}+\xi_2\vec{g}_{2}$
$\vec{z}+\vec{y}=\xi_{1}\vec{g}_{1}+\xi_2\vec{g}_{2}+\xi_{3}\vec{g}_{3}\ \blacksquare$ 
**Uniqueness:**
Let $\vec{x} = \xi_1\vec{g_1}+\xi_3\vec{g_3}+\xi_3\vec{g_3}$
Assume that there exist $\xi'_{1}\neq\xi_{1}\neq0,\ \xi'_{2}\neq\xi_{2}\neq0,\ \xi'_3\neq\xi_{3}\neq0$: $\vec{x} = \xi'_{1}\vec{g_{1}}+\xi'_{2}\vec{g_{2}}+\xi'_{3}\vec{g_{3}}$
Then, $\vec{x} - \vec{x} = 0 = (\xi_{1} - \xi'_{1})\vec{g_1}+(\xi_{2} - \xi'_{2})\vec{g_2}+(\xi_{3} - \xi'_{3})\vec{g_{3}}$$\Rightarrow |\xi_{1} - \xi'_{1}|+|\xi_{2} - \xi'_{2}|+|\xi_{3} - \xi'_{3}|>0$ - not trivial case, basis vectors are linear dependent. *Contradiction!*
### Task 1: Prove that for any $\vec{a}, \vec{b}, \vec{c}$ and any scalars $\alpha, \beta, \gamma$ the vectors $\alpha\vec{a} - \beta\vec{b}$, $\gamma\vec{b} - \alpha\vec{c}$, $\beta\vec{c} - \gamma\vec{a}$ - linearly dependent.
**Proof:**
$\vec{a}, \vec{b}, \vec{c} - basis \ \ \ \ \ \ \ \ \alpha\vec{a} - \beta\vec{b}$ = $\begin{psmallmatrix}\alpha\\-\beta\\0 \end{psmallmatrix}$
$\gamma\vec{b} - \alpha\vec{c} = \begin{psmallmatrix}0\\ \gamma\\-\alpha\end{psmallmatrix} \ \ \ \ \ \ \ \ \beta\vec{c} - \gamma\vec{a} = \begin{psmallmatrix}-\gamma \\ 0 \\ \beta\end{psmallmatrix}$ 
We need to prove that there exist u, v, w:
$u \begin{psmallmatrix}0\\\gamma\\-\alpha\end{psmallmatrix} + v\begin{psmallmatrix}\alpha\\-\beta\\0\end{psmallmatrix} + w\begin{psmallmatrix}-\gamma\\0\\\beta\end{psmallmatrix} = 0 = \begin{psmallmatrix}0\\0\\0\end{psmallmatrix}$
$$\begin{cases}\alpha v - \gamma w = 0  \rightarrow  \alpha v = \gamma w  ,\ v = \frac{\gamma}{\alpha}w \\
u\gamma - \beta b = 0 \rightarrow u\gamma = \beta v = \beta*\frac{\gamma}{\alpha}w \rightarrow u = \frac{\beta}{\alpha}w \\
-\alpha u + \beta w = 0 \rightarrow -\alpha*\frac{\beta}{\alpha}w + \beta w = 0 
\end{cases}$$
$\blacksquare$
### Task 2: Check that $\vec{a}(-5,-1),\ \vec{b}(-1,3)$ form a basis in the plane. Find the coordinates of $\vec{e}(-1,2), \ \vec{l}(2,-6)$(homework) in this basis.
1. Check the collinearity: $\vec{a} = k\vec{b}$
$\begin{pmatrix}-5\\-1\end{pmatrix}= {\begin{pmatrix}-1*k\\3*k\end{pmatrix}}\Rightarrow \nexists \ k \Rightarrow basis$. 
2. $\vec{e} = \alpha\vec{a} +\beta\vec{b}\Leftrightarrow \begin{pmatrix}-1\\2\end{pmatrix} = \alpha\begin{pmatrix}-5\\-1\end{pmatrix}+\beta{\begin{pmatrix}-1\\3\end{pmatrix}}$ 
   ${\begin{cases}-5\alpha-\beta=-1\\-\alpha+3\beta=2\end{cases}}$ $\Rightarrow \beta=\frac{11}{16}; \ \alpha=\frac{1}{16}$ 
3. $\vec{l}=\lambda\vec{a}+\beta\vec{b}\Leftrightarrow{\begin{pmatrix}2\\-6\end{pmatrix}}= \alpha\begin{pmatrix}-5\\-1\end{pmatrix}+\beta{\begin{pmatrix}-1\\3\end{pmatrix}}$ 
   $\begin{cases}-5\alpha-\beta=2\\-\alpha+3\beta=-6\end{cases}$ $\Rightarrow \alpha=0; \ \beta=-2$  
### Task 3: $\displaylines{ABCD - \texttt{Trapeziod},\ \frac{|AD|}{|BC|}=\frac{4}{1},\ M -\texttt{diagonals' intersection},\\ P-\texttt{intersection of extensions of the side edges.}\\ \overline{AD}\ \&\ \overline{AB}-\texttt{basis},\ \texttt{Find}\ M-?,\ P-?}$
**Solution:**

# Assignments:
- Read the topics of lecture: [Аналитическая Геометрия и Линейная Алгебра](Analiticheskaya_geometria_i_lineynaya_algebra_2020_Umnov.pdf)
- Watch the topics of lecture: [Linear Algebra](https://www.3blue1brown.com/topics/linear-algebra)