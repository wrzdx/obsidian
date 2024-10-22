# Theory:

## 1. Definition, simple proofs:

### Let $V = \{v_{1},v_{2},...,v_{n}\}$ be a set of vectors. Give a definition of a span $S(V)$:

The **span** of a set of vectors $S = \{v_{1},v_{2},...,v_{n}\} \subseteq V$ is the set of all possible linear combinations of the vectors in $S$:
$$\text{span}(S) = \left\{w \in V:w=\sum^{n}_{k=1}c_{k},v_{k},\ \forall c_{k} \in \mathbb{R}\right\}.$$
In this context, any vector $w \in \text{span}(S)$ can ve expressed as a linear combination of the vectors $v_{1},v_{2},...,v_{n}$, where the coefficients $c_{k}$ are real numbers.

---
### What is the geometrical interpretation of the magnitude of $a \times b$?

The magnitude of the cross product $|a \times b|$ represents two things geometrically:

1. The area of the parallelogramm spanned by vectors $a$ and $b$: $|a||b||\sin \theta|$
2. The length of the vector that is perpendicular to both $a$ and $b$, as $a \times b$ itself is a vector that is orthogonal to both $a$ and $b$.

So, $|a \times b|$ gives the length of the vector normal to the plane defined by $a$ and $b$, and this length corresponds to the area of the parallelogram.

---
### Given that $BC$ and $CB$ are valid, prove that $Tr(BC) = Tr(CB)$:

1.  **Definition of Trace:** The trace of a matrix is the sum of its diagonal elements. For any $n \times n$ matrix $A$, we have:$$Tr(A) = \sum^{n}_{i=1}A_{ii}$$where $A_{ii}$ represents the $i$-th diagonal element of matrix $A$.
2. **Trace of a Product:** Let $B$ and $C$ be two $n \times n$ matrices such that both $BC$ and $CB$ are valid matrix multiplication.
   
   The $(i,i)$-th element of the matrix $BC$ is: $$(BC)_{ii} = \sum^{n}_{j=1}B_{ij}C_{ji}$$Therefore, the trace of $BC$ is:$$Tr(BC) = \sum^{n}_{i=1}(BC)_{ii} = \sum^{n}_{i=1}\sum^{n}_{j=1}B_{ij}C_{ji}$$
3. **Symmetry:** Now, consider the matrix $CB$. The $(i,i)$-th element of the matrix $CB$ is:$$(CB)_{ii} = \sum^{n}_{j=1}C_{ij}B_{ji}$$So the trace of $CB$ is:$$Tr(CB) = \sum^{n}_{i=1}(CB)_{ii} = \sum^{n}_{i=1}\sum^{n}_{j=1}C_{ij}B_{ji}$$
4. **Interchanging the Summation Using Commutativity:** Notice that in both expression $\sum^{n}_{i=1}\sum^{n}_{j=1}B_{ij}C_{ji}$ and $\sum^{n}_{i=1}\sum^{n}_{j=1}C_{ij}B_{ji}$, we are multiplying two scalars: $B_{ij}$ and $C_{ji}$ in one case, and $C_{ij}$ and $B_{ji}$ in the other. Since scalar multiplication is **commutative**, we have:$$B_{ij}C_{ji} = C_{ji}B_{ij}$$Therefore, the terms in both summations are identical, meaning:$$\sum^{n}_{i=1}\sum^{n}_{j=1}B_{ij}C_{ji}=\sum^{n}_{i=1}\sum^{n}_{j=1}C_{ji}B_{ij}=\sum^{n}_{i=1}\sum^{n}_{j=1}C_{ij}B_{ji}$$
5. **Conclusion:** Since the two summations are equal, it follows that:$$Tr(BC) = Tr(CB).$$
---
# Practice:

## 1. Vector operations / Matrices:

### Find the determinant of matrix:$\begin{bmatrix}1&-2&2\\2&1&-1\\4&-3&5\end{bmatrix}$

$$\begin{vmatrix}1&-2&2\\2&1&-1\\4&-3&5\end{vmatrix} = 2 + 2*14 -2*10 = 10$$
---
### Find a vector that is orthogonal to both $v_{1} = (1,-1,1)$ and $v_{2} = (6,-3,0)$ and which dot product with a vector $v_{3}= (3,2,3)$ equals to 10:

**First Solution:**

Find the orthogonal vector $q$ to both $v_1$ and $v_{2}$ using cross product:
$$v_{1}\times v_{2} = \begin{vmatrix}
i & j&k \\ 1&-1&1 \\ 6&-3&0
\end{vmatrix} = 3i+6j+3k = \begin{bmatrix}
3 \\ 6 \\ 3
\end{bmatrix}$$
We know that dot product of collinear vector to $q$ and $v_{3}$ is 10:
$$\lambda q \cdot v_{3} = 10$$
Let us define $\lambda$:
$$3\lambda *3 + 6\lambda*2 +3\lambda * 3 = 10$$
$$\lambda = \frac{1}{3} \Rightarrow \text{Answer:} \begin{bmatrix}
1 \\ 2 \\ 1
\end{bmatrix}$$
**Second Solution:**

Let the vector that we want to find be $q = (x,y,z)$, then, since it is orthogonal to both $v_{1}$ and $v_{2}$, we can conclude: $q \cdot v_{1} = 0$ and $q \cdot v_{2} = 0$

Also, we know that $q \cdot v_{3} = 10$, so we have the system of equations:
$$\begin{cases}
q \cdot v_{1}= x - y + z =0 \\
q \cdot v_{2} = 6x -3y = 0 \\
q \cdot v_{3} = 3x + 2y + 3z = 10
\end{cases}\Rightarrow \begin{cases}
x=z \\
y=2z \\
3z + 4z + 3z = 10
\end{cases} \Rightarrow \begin{cases}
x=1 \\
y=2 \\
z=1 \\
\end{cases}$$
Answer: $\begin{bmatrix}1 \\ 2 \\ 1\end{bmatrix}$

---
## Lines / Planes:

### Find the angle between the planes $x+y-4z = 8$, $4x + y -z = 8$:

The angle between two planes is equal to the angle between their normal vectors. The angle between vectors:
$$\cos \theta = \frac{a \cdot b}{|a||b|}$$
The normal vector of our planes:
$$n_{1}= \begin{bmatrix}
1 \\ 1 \\ -4
\end{bmatrix}, \ \ n_{2}= \begin{bmatrix}
4 \\ 1 \\ -1
\end{bmatrix}$$
Hence,
$$\cos \theta = \frac{4+1+4}{\sqrt{18}\sqrt{18}} = \frac{9}{18} = \frac{1}{2}$$
**Answer:** $60^\circ$

---
### What is the general equation of the plane which contains the following two parallel lines: $\frac{x-1}{5}=\frac{y+2}{3}=z$ and $\frac{x+3}{5}=\frac{y-4}{3}=z-1$:

To find the equation of a plane we should first find the normal vector of this plane. It can be finded by cross product of non-parallel vector in this plane.

Let the first vector be the direction vector of our parallel lines, its coordinates are denominators of the canonical equation:
$$q = \begin{bmatrix}
5 \\ 3 \\ 1
\end{bmatrix}$$
Let us find 2 point for the second vector $p$ from each line:

Let $z=0$:
$$x=1,\ \  y=-2$$
Let $z = 1$: 
$$x=-3, \ \ y = 4$$
Hence, our second vector is $p=\begin{bmatrix}1-(-3) \\ -2-4 \\ 0-1\end{bmatrix} = \begin{bmatrix}4 \\ -6 \\ -1\end{bmatrix}$
Let us find the orthogonal vector to both these vectors:
$$q \times p =\begin{bmatrix}
5 \\ 3 \\ 1
\end{bmatrix} \times\begin{bmatrix}4 \\ -6 \\ -1\end{bmatrix}=\begin{bmatrix}
3 \\ 9 \\ -42
\end{bmatrix}$$
So, general equation of a plane:
$$3x+9y-42z+D=0$$
Now, we should find $D$ substituting some point from our lines, let it be $(1,-2,0)$:
$$3\cdot1+9 \cdot(-2) - 42\cdot0+ D = 0$$
$$D = 15$$
Thus, answer is:
$$3x+9y-42z+15=0$$
or 
$$x + 3 y - 14z + 5=0$$
---

## Find the distance from the point $(1,1,-1)$ to the line of intersection of the planes $x+y+z = 1$ and $2x-y-5z=1$:

Let us find the equation of the intersection line. To do that, we should find two point on this:

Let $z=0$:
$$\begin{cases}
x+y = 1 \\
2x-y = 1
\end{cases} \begin{cases}
x = \frac{2}{3} \\
y=\frac{1}{3}
\end{cases}$$
Let $z=1$:
$$\begin{cases}
x+y = 0 \\
2x-y =6
\end{cases} \begin{cases}
x = 2 \\
y=-2
\end{cases}$$
Now, we can find canonical equation of line via two points:
![](Straight%20line%20in%202D%20plane%20and%203D%20space.%20Equations%20of%20a%20line%20in%20plane..md#^522015)

$$\frac{x- \frac{2}{3}}{\frac{4}{3}} = \frac{y-\frac{1}{3}}{-\frac{7}{3}}=z$$
We can also define the vector connecting points $(2,-2,1)$ and $(1,1,-1)$, let it be $p=\begin{bmatrix}1 \\ -3 \\ 2\end{bmatrix}$.

Let us find direction vector of our line by denominators of canonical equation, and since it is just direction vector we can muliply it by some scalar: $q = 3 \cdot \begin{bmatrix} \frac{4}{3} \\ -\frac{7}{3} \\ 1\end{bmatrix} = \begin{bmatrix}4 \\ -7 \\ 3\end{bmatrix}$
So, we can define distance between point and line from area:

$$S =|p \times q| = \left|\begin{bmatrix}1 \\ -3 \\ 2\end{bmatrix} \times \begin{bmatrix}
4 \\ -7 \\ 3
\end{bmatrix}\right| = \left|\begin{bmatrix}
5 \\ 5 \\ 5
\end{bmatrix}\right| = \sqrt{75} = 5\sqrt{3}$$
$$d = \frac{S}{|q|}=\frac{5\sqrt{3}}{\sqrt{16+49+9}} = \frac{5\sqrt{3}}{\sqrt{74}} = \frac{5\sqrt{222}}{74}$$
**Answer:** $\frac{5\sqrt{222}}{74}$.

**Second Solution:**

Let the vector orthogonal to line and contain given point be $p$.
The coordinates of the point in line:
$$\begin{cases}x= \frac{2}{3}+\frac{4}{3}t \\
y = \frac{1}{3}- \frac{7}{3}t \\
z= t\end{cases}$$
Then, 
$$p = \begin{bmatrix}
1- \frac{2}{3}-\frac{4}{3}t \\ 1 - \frac{1}{3} + \frac{7}{3}t \\ -1-t
\end{bmatrix} = \begin{bmatrix}
\frac{1}{3}- \frac{4}{3}t \\ \frac{2}{3}+ \frac{7}{3}t \\ -1 -t
\end{bmatrix}$$
The direction $q= \begin{bmatrix} 4 \\ -7 \\ 3\end{bmatrix}$:
$$3p \cdot q = 4-16t-14-49t-9-9t=0$$
$$-19=74t \Rightarrow t = -\frac{19}{74}$$
$$|p| = \left|\begin{bmatrix}
\frac{1}{3}+ \frac{38}{111} \\ \frac{2}{3}- \frac{133}{222}\\ - 1 + \frac{19}{74}
\end{bmatrix}\right| = \left|\begin{bmatrix}
\frac{25}{37} \\  \frac{5}{74} \\ -\frac{55}{74}
\end{bmatrix}\right| = 
$$$$\frac{\sqrt{625+ \frac{25}{4} + \frac{3025}{4}}}{37} = \frac{\sqrt{2500+3050}}{74} = \frac{5\sqrt{100+122}}{74}$$
$|p| = \frac{5\sqrt{222}}{74}$

---
## Two vertices of a triangle are $(6,-1)$ and $(-2,5)$. If the orthocenter (intersection of altitudes) of the triangle is at $(1,2)$, find the coordinates of the third vertex:

Let our vertices be $P(1,20,\ A(6,-1),\ B(-2,5)$ and $C(x,y)$. Then, 
- $AB = (-8,6)$
- $BC=(x+2,y-5)$
- $AC(x-6,y+1)$
