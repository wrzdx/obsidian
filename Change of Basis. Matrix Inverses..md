---
tags:
  - 1stYear
---
# Material: 

- [2024_AGLA1_Lecture_4](2024_AGLA1_Lecture_4.pdf)

# Change of basis and coordinates:
---
**Notations:**
- $(O, \overline{e}_{1},\overline{e}_{2},\overline{e}_{3})$ – is coordinates system ($\overline{e}_{1},\overline{e}_{2},\overline{e}_{3}$ - basis).
- $\overline{v} = x_{1}\overline{e}_{1}+x_{2}\overline{e}_{2}+x_{3}\overline{e}_{3} = \begin{bsmallmatrix}x_{1}\\ x_{2}\\ x_{3}\end{bsmallmatrix}$
---
Let $(O, \overline{e}_{1},\overline{e}_{2},\overline{e}_{3})$ is old coordinates system, and $(O', \overline{e'}_{1},\overline{e'}_{2},\overline{e'}_{3})$ is new coordinates system.
N – is arbitrary point in space.
Then,

![|600](Pasted%20image%2020240923093732.png)
$$\displaylines{ON = OO'+O'N \\
ON = x_{1}e_{1}+x_{2}e_{2}+x_{3}e_{3}\\
O'N = x_{1}'e_{1}'+x_{2}'e_{2}'+x_{3}'e_{3}'\\
OO' = b_{1}e_{1}+b_{2}e_{2}+b_{3}e_{3}
}$$
We can express the new basis through the old one.
$$\displaylines{
e_{1}' = \alpha_{11}e_{1} + \alpha_{21}e_{2}+\alpha_{31}e_{3}\\
e_{1}' = \alpha_{12}e_{1} + \alpha_{22}e_{2}+\alpha_{32}e_{3}\\
e_{1}' = \alpha_{13}e_{1} + \alpha_{23}e_{2}+\alpha_{33}e_{3}}$$
Hence, we will get the transition matrix [^1]
$$A=\begin{bmatrix}
\alpha_{11}&\alpha_{12}&\alpha_{13}\\ \alpha_{21}&\alpha_{22}&\alpha_{23}\\ 
\alpha_{31}&\alpha_{32}&\alpha_{33}\\
\end{bmatrix}$$
Next, we substitute all of we got to initial expression.
$$\displaylines{ON = OO'+O'N = \\b_{1}e_{1}+b_{2}e_{2}+b_{3}e_{3} + \\ x_{1}'(\alpha_{11}e_{1} + \alpha_{21}e_{2}+\alpha_{31}e_{3})+\\
x_{2}'(\alpha_{12}e_{1} + \alpha_{22}e_{2}+\alpha_{32}e_{3} + \\
x_{3}'(\alpha_{13}e_{1} + \alpha_{23}e_{2}+\alpha_{33}e_{3}) =\\
(b_{1}+ x_{1}' \alpha_{11}+x_{2}'\alpha_{12}+x_{3}'\alpha_{13})e_{1}+\\
(b_{2}+ x_{1}' \alpha_{21}+x_{2}'\alpha_{22}+x_{3}'\alpha_{23})e_{2}+\\
(b_{3}+ x_{1}' \alpha_{31}+x_{2}'\alpha_{32}+x_{3}'\alpha_{33})e_{3}
}$$
This expression can be represented by the transition matrix:
$$\displaylines{
\begin{bmatrix}
x_{1} \\ x_{2} \\ x_{3}
\end{bmatrix} = \begin{bmatrix}
b_{1} \\ b_{2}\\b_{3}
\end{bmatrix} + \begin{bmatrix}
\alpha_{11}&\alpha_{12}&\alpha_{13}\\ \alpha_{21}&\alpha_{22}&\alpha_{23}\\ 
\alpha_{31}&\alpha_{32}&\alpha_{33}\\
\end{bmatrix} \begin{bmatrix}
x_{1}' \\ x_{2}' \\ x_{3}'
\end{bmatrix} \\ x = b + Ax'
}$$

^78c141

# Matrix rotating:

- Let $v$ be a vector with coordinates $\begin{bmatrix}x\\y\end{bmatrix}$.
- Let $v'$ be the vector with new coordinates $\begin{bmatrix}x'\\y'\end{bmatrix}$ obtained by rotating $v$ by angle an $\theta$.

![|400](Pasted%20image%2020240923102734.png)

-  The new coordinates $\begin{bmatrix}x'\\y'\end{bmatrix}$ can be found using the following matrix:
$$\displaylines{
\begin{bmatrix}
x' \\ y'
\end{bmatrix} = R(\theta)\begin{bmatrix}
x \\ y
\end{bmatrix} = \begin{bmatrix}
\cos\theta & -\sin\theta \\ \sin\theta & \cos\theta 
\end{bmatrix}\begin{bmatrix}
x \\ y
\end{bmatrix}
}$$
# Matrix Inverses:

> [!abstract] Definition
> Matrix $B$ is called inverse of a square matrix $A$ if
> $$AB = BA = I$$
> **Notation:** 
> - $B=A^{-1}$
> - $AA^{-1}= A^{-1}A = I$
> **Example:**
> ![](Pasted%20image%2020240923105422.png)

^935ff3

> [!abstract] Left inverse
> Consider an $m\times n$ matrix $A$ and $n\times m$ matrix $B$. 
> If $BA = I$, then we say $B$ is the **left inverse** of $A$.

>[!abstract] Right inverse 
>Consider an $m\times n$ matrix $A$ and $n\times m$ matrix $C$.
>If $AC = I$, then we say $C$ is the **right inverse** of $A$.

>[!abstract] Invertabilty
>- If $A$ has an inverse, then $A$ is **invertible** (== nonsingular).
>- If $A$ and $B$ are invertible and $AB$ is invertible, then
>  $$(AB)^{-1}=B^{-1}A^{-1}$$
>
>- For an $n\times n$ matrix $A$ the following statements are equivalent:
>	- $A$ is invertible
>	- The determinant of matrix $A$ is nonzero $det(A)\neq 0$
>	- The columns of matrix $A$ form a basis for $\mathbb{R}^{n}$
>	- The [rank](Change%20of%20Basis.%20Matrix%20Inverses..md#^4c6197) of the matrix $A$ is $n$
>	- $A^{\top}$ is invertible
>	- The rows of matrix $A$ form a basis for $\mathbb{R}^{n}$
>	- $Ax=b$ has exactly one solution $(x=A^{-1}b)$
>	- $Ax=0$ has only a *trivial* solution ($x=0,$ zero vector)

## Ways to find the inverse matrix:

> [!example]  Minor Method (using cofactors)
> 1. Find the determinant of matrix $A$.
> 2. Find the minors:
> 	- **Minor** is the determinant of the smaller matrix you get by deleting the row and column of that element.
> 	- For each element of the matrix, you find a **minor** and write it to another matrix in the appropriate position. 
> 3. Find cofactors:
>	- For each element of the obtained matrix we apply a sign pattern: $(-1)^{i+j}$, where $i$ and $j$ are the row and column numbers of the element.
>	- This gives you the cofactor matrix.
>4. Transpose[^2] the cofactor matrix.
>5. Find the inverse:
>	- $A^{-1} = \frac{1}{det(A)}\times \texttt{(Transposed cofactor matrix)}$.

> [!example] Gauss-Jordan Method
> 1. Set up an augmented matrix.
> 	- You take your matrix $A$ and put it next to identity matrix[^3] $I$. $$[A|I]$$ 
> 2. Perform row operations:
> 	- The goal is to use elementary row operations[^4] to turn the left side (matrix $A$) into the identity matrix.
> 3. Get the inverse:
> 	- When the left side becomes the identity matrix, the right side will have turned into the inverse of matrix $A$. $$[I|A^{-1}]$$

>[!example] Important case: Orthogonal matrix
>- Orthogonal matrix - square matrix whose columns and rows are orthonormal vectors[^5].
>- $A^{-1} = A^{\top}$
>- $AA^{\top}=A^{\top}A=I$

# Matrix rank:

^4c6197

- ***The Column rank*** of a matrix is the largest number of linearly independent columns.  
- ***The Row rank*** of a matrix is the largest number of linearly independent rows.

>[!abstract] Theorem
>For ANY $m\times n$ matrix the column rank equals to row rank
>So, there is only **one** matrix rank. $rank(A)=rank(A^{\top})$

>[!example] Import properties of rank
>- **maximum** possible rank of $A$ equals $min(m,n)$.
>  so $rank(A)\leq min(m,n)$ If matrix has a maximum possible rank, it is called a **full rank matrix**.
>- $rank(A+B)\leq rank(A) + rank(B)$
>- $rank(AB)\leq min(rank(A),rank(B))$
>- $rank(A)=rank(AA^{\top})=rank(A^{\top}A) = rank(A^\top)$

---
# Trace of a matrix:

>[!abstract] Trace of a square matrix $A$
>$$Tr(A) = \sum^{m}_{i=1}a_{ii}$$
>
>$$Tr(A+B) = Tr(A)+Tr(B)$$
>$$\forall \lambda \in \mathbb{R},\ Tr(\lambda A) = \lambda Tr(A)$$


---
# Graphs and Matrices:

- Given a graph you can define its adjacency matrix, $A$
  ![](Pasted%20image%2020240923232547.png)
  *Matrix represents paths of length 1 (e.g. one 'hops' between 4 and 1)*
- Given an adjacency matrix, $A$ you can find its power ($A^{2}=AA$)
  ![](Pasted%20image%2020240923233543.png)
  
  *Matrix represents paths of length 2 (e.g. two 'hops' to reach 5 from 1)*

# Neural Networks and Matrices:
![](Pasted%20image%2020240923234045.png)

[^1]: Matrix that converts coordinates from one basis to another
[^2]: Transpose is flipping rows and columns.
[^3]: Matrix which has 1's on the diagonal and 0's everywhere else. For example, $\begin{bsmallmatrix}1&0\\0&1\end{bsmallmatrix}$ 
[^4]: swapping rows, multiplying a row by a non-zero element, adding/subtracting one row to/from another row 
[^5]: Vectors that are perpendicular to each other and have length of 1.