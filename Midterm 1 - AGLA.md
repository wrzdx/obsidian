---
tags:
  - 1stYear
---
# Theory:

1. Vectors $v_{1}, v_{2},...,v_{n}$ are linearly independent if for $\lambda_{1},\ \lambda_{2},...,\ \lambda_{n}\in\mathbb{R},\ \lambda_{1}v_{1} + \lambda_{2}v_{2} +\ ...\ + \lambda_{n}v_{n} = 0$ if and only if $\lambda_{1}=\lambda_2=...=\lambda_{n}=0.$  
2. Condition of coplanarity of three vectors:
   Three vectors are complanar if their scalar triple product is equal to $0$:
   $$\displaylines{a \cdot (b \times c) = 0}$$
3. Trace of a matrix is the sum of all elements on the main diagonal:
   $$Tr(A) = \sum^{m}_{i=1}a_{ii}$$
   
   Trace is linear if it satisfies the following properties:
   
   - **Additivity:** $Tr(A + B) = Tr(A) + Tr(B)$
   - **Homogeneity:** $Tr(c \cdot A) = c \cdot Tr(A)$

   **Additivity:**
   $$Tr(A+B) = \sum^{m}_{i=1}(a_{ii} + b_{ii}) = \sum^{m}_{i=1}a_{ii} + \sum^{m}_{i=1}b_{ii} = Tr(A) + Tr(B)$$
   
   **Homogeneity:**
   $$Tr(c \cdot A) = \sum^{m}_{i=1}(c \cdot a_{ii}) = c \cdot \sum^{m}_{i=1}a_{ii} = c \cdot Tr(A)$$
# Practice:

## 1. Vector operations / Matrices:

### Find the determinant of the $3 \times 3$ matrix:
$\begin{bmatrix}2&5&-3 \\ 1& 4 & -2 \\ -7 & 3 & 0\end{bmatrix}$
$$\displaylines{\Delta = (2*4*0 + 5*(-2)*(-7) + (-3)* 1 * 3) - \\(-7*4*(-3) + (3*(-2)*2) + 0 * 1 * 5) = \\ (0 + 70 -9) - (84 - 12 + 0) = 61 - 72 = -11}$$
---
### Find  a vector that is orthogonal to both $v_{1} = (1,0,1)$ and $v_{2}=(1,3,0)$ and which dot product with vector $v_{3} = (1,1,0)$ equals to $8$:

$$\displaylines{\lambda(v_{1}\times v_{2})\cdot v_{3} = 8\\
v_{1}\times v_{2}=\begin{bmatrix}
1 \\ 0 \\ 1
\end{bmatrix} \times \begin{bmatrix}
1 \\ 3 \\0
\end{bmatrix} = det \begin{bmatrix}
i & 1 & 1 \\ j & 0 & 3  \\ k & 1 & 0
\end{bmatrix} = \\
i \begin{bmatrix}
0 & 3  \\  1 & 0
\end{bmatrix} + j \begin{bmatrix}
1&1 \\ 1&0
\end{bmatrix} + k\begin{bmatrix}
1&1 \\ 0&3
\end{bmatrix} = -3i + j + 3k=
\begin{bmatrix}
-3 \\ 1 \\ 3
\end{bmatrix}\\
\lambda(v_{1} \times v_{2})\cdot v_{3} = \lambda\begin{bmatrix}
-3 \\ 1 \\ 3
\end{bmatrix}\cdot \begin{bmatrix}
1 \\ 1 \\ 0 
\end{bmatrix} = \lambda(-3+1+0)=8}$$
$$-2\lambda = 8 \Rightarrow \lambda = -4$$
**Answer:** $\lambda\begin{bmatrix}-3 \\ 1 \\ 3\end{bmatrix} = \begin{bmatrix}12 \\ -4 \\ -12\end{bmatrix}$

## 2. Lines / Planes:

### Find the angle between the planes $2x - y + z = 6$, $x+y+2z =3$:

We can consider the planes $2x - y +z = 6$ and $x+y+2z = 3$ through a plane that is perpendicular to both of them. From the equations of these planes, we can directly determine the normal vectors.

Each plane can be written in the general form $Ax+By+Cz =D$, where the coefficient $A,\ B$ and $C$ are the components of the normal vector to the plane. These coefficient represents the direction in which the plane is perpendicular to all vectors lying on it.
- For the first plane, the normal vector is $\overline{n}_{1} = \begin{bmatrix}2 \\ -1 \\ 1\end{bmatrix}$
- For the second plane, the normal vector is $\overline{n}_{2} = \begin{bmatrix}1 \\ 1 \\ 2 \end{bmatrix}$
![](Pasted%20image%2020241016210817.png)
In the diagram, the angle between these planes is represented by the angle between their normal vectors. Using the dot product of the normal vectors, we can calculate this angle:
$$cos \theta = \frac{\overline{n}_{1} \cdot \overline{n}_{2}}{|\overline{n}_{1}||\overline{n}_{2}|} = \frac{3}{\sqrt{6}\sqrt{6}} = \frac{1}{2} \Rightarrow \theta = 60^\circ$$

#### What is the general equation of the plane which contains the following two parallel lines: $\frac{x+1}{6} = \frac{y-2}{7} =z$ and $\frac{x-3}{6} = \frac{y-4}{7} = z-1$:

To find the equation of a plane that contains two parallel lines, we need to determine the **normal vector** to the plane. This vector will be **perpendicular** to both parallel vectors. To find this normal vector, we can use the **cross product** of two **linearly independent vectors** that lie in the plane.

1. **Guiding vector:**
   The **guiding vector** of a line, denoted as $\overline{q}$, is the vector that defines the direction of the line in space. According to the canonical representation of a line in space:
   $$\frac{x-x_{0}}{q_{x}} = \frac{y-y_0}{q_{y}} = \frac{z-z_{0}}{q_{z}}$$
   the components of the guiding vector $(q_{x},q_{y},q_{z}$) are the denominators in this equation. In our case, we have the line $\frac{x+1}{6} = \frac{y-2}{7} =z$, and the guiding vector is $\overline{q} = (6,7,1)$. This vector $\overline{q}$ is parallel to our vectors, so it also lie in the plane of these vectors.

2. **Choosing a second vector:**
   To find a second vector that lies in the plane, we can pick **two points** – one on each of the parallel lines. The vector connecting these two points will also lie in the plane. Let us convert the canonical form of the line into **parametric form**:
    $$\frac{x+1}{6} = \frac{y-2}{7} = z = t$$$$\begin{cases}
x=6t-1 \\
y=7t+2 \\
z=t
\end{cases}$$$$\frac{x-3}{6}=\frac{y-4}{7}=z-1=t$$$$\begin{cases}
x=6t+3 \\
y=7t+4 \\
z=t+1
\end{cases}$$
   Let $t=0$, then $P_{1} = (-1,2,0)$, $P_{2} = (3,4,1)$
   And the second vector is $\overline{P_{1}P_{2}} = (4,2,1)$.
   
3. **Finding the normal vector:**
   Now, we have two vectors lying in the plane: the guiding vector $\overline{q} = (6,7,1)$ and the vector $\overline{P_{1}P_{2}} = (4,2,1)$. To find the normal vector $\overline{n}$, we compute their **cross product**:
   $$\displaylines{\overline{n} = \overline{q}\times \overline{P_{1}P_{2}}=\begin{bmatrix}
i&j&k \\ 6&7&1 \\ 4&2&1
\end{bmatrix} = 5i -2j -16k\\ \overline{n} = \begin{bmatrix}
5 \\ -2 \\ -16
\end{bmatrix}}$$
4. **Equation of the plane:**
   Finally, we can use the normal vector $\overline{n} = (5,-2,-16)$ and the point $P_{1}(-1,2,0)$ to write the equation of the plane. The equation of the plane is:
   $$n_{x}(x-x_{0})+n_{y}(y-y_{0})+n_{z}(z-z_{0}) = 0$$
   Substituting the values:
   $$5(x+1) - 2(y-2) - 16(z-0) = 0$$
   Simplifying:
   $$5x-2y-16z+9=0$$
   

## 3. Find the distance from the point $(1,1,-1)$ to the line of intersection of the planes $x+y+z=1$ and $2x-y-5z=1$:

To find distance from the point $(1,1,-1)$ to the line of intersection of the planes $x + y + z = 1$ and $2x-y-5z = 1$, 
we should first find the line itself:
1. Let us find two point in the intersection of the planes:
   
   Let $z=0$, then the system of equations:
   $\begin{cases}x+y=1 \\2x-y = 1\end{cases} \Rightarrow \begin{cases}x = \frac{2}{3} \\ y = \frac{1}{3}\end{cases} - \text{This is the first point}$
   Let $x = 0$, then:
   $\begin{cases}y+z= 1\\-y-5z=1\end{cases}\Rightarrow \begin{cases}z=- \frac{1}{2}\\y = \frac{3}{2}\end{cases} - \text{This is the second point}$

2. Now we can make the Canonical Equation of the Line:
   ![](Straight%20line%20in%202D%20plane%20and%203D%20space.%20Equations%20of%20a%20line%20in%20plane..md#^522015)
   In our case:
   $$\frac{x-\frac{2}{3}}{0-\frac{2}{3}} = \frac{y - \frac{1}{3}}{\frac{3}{2} - \frac{1}{3}} = \frac{z-0}{\frac{-1}{2}-0}$$
   Simplifying:
   $$-\frac{3}{2}x+ 1 = \frac{6}{7}y - \frac{2}{7} = - 2z$$

There are two ways to find the distance between the line and the point:

- The first uses dot product
- The second uses the cross product (area interpretation)

**The first one via dot product:**

1. We express vector that is perpendicular to the line and contains the given point with some parameter $t$.
2. Dot product of this vector and the direction vector of line will be $0$, because they are perpendicular.

We should express the coordinates of the point in our line by converting the Canonical Equation to the Parametric:
$$\begin{cases}
x = - \frac{2}{3}t + \frac{2}{3} \\
y = \frac{7}{6}t+ \frac{1}{3} \\
z = - \frac{1}{2}t
\end{cases}$$
Next, we define the vector via the point from the condition and point in line and the direction vector:

$$\overline{v} = \begin{bmatrix}- \frac{2}{3}t + \frac{2}{3} - 1 \\ \frac{7}{6}t + \frac{1}{3} - 1 \\ - \frac{1}{2}t + 1\end{bmatrix} = \begin{bmatrix}
- \frac{2}{3}t- \frac{1}{3} \\ \frac{7}{6}t - \frac{2}{3} \\ - \frac{1}{2}t + 1
\end{bmatrix}$$
$$\overline{q} = \begin{bmatrix}
- \frac{2}{3}\\ \frac{7}{6} \\ - \frac{1}{2}
\end{bmatrix} - \text{ coefficients before }t$$
Write the dot product of these vectors:

$$\displaylines{\overline{v}\cdot \overline{q} = \frac{4}{9}t + \frac{2}{9} + \frac{49}{36}t - \frac{7}{9} + \frac{1}{4}t - \frac{1}{2} =\\
\frac{37}{18}t -\frac{19}{18}=0 \\
t= \frac{19}{37}}$$
Subsitute $t$ back:
$$\overline{v}=\begin{bmatrix}
- \frac{2}{3}\cdot \frac{19}{37}- \frac{1}{3} \\ \frac{7}{6}\cdot \frac{19}{37} - \frac{2}{3} \\ - \frac{1}{2}\cdot \frac{19}{37} + 1
\end{bmatrix} = \begin{bmatrix}
- \frac{25}{37} \\ - \frac{5}{74}\\ \frac{55}{74}
\end{bmatrix}$$
Calculate the length of this vector:
$$\displaylines{d = \sqrt{\left(- \frac{25}{37}\right)^{2} + \left(- \frac{5}{74}\right)^{2} + \left(\frac{55}{74}\right)^{2}} =\\ \sqrt{\frac{5^{2}}{37^{2}}\left(25 + \frac{1}{4} + \frac{121}{4}\right)} = \frac{5\sqrt{222}}{74}}$$

**The second way via cross product (area interpretation):**

1. We should find some point in the line and make the vector by this point and the given point
2. Define the direction vector 
3. We have two vectors that makes parallelogramm square which is equal to length of the cross product of those vectors.
4. Area is also equal to multiplication of the direction vector length and the distance between given point and line.
![|350](Pasted%20image%2020241020141649.png)

Let given point is $P(1,1,-1)$, and let us select some point in intersection line $Q(0,\frac{3}{2}, - \frac{1}{2})$, direction vector $\overline{q}(- \frac{2}{3},\frac{7}{6},- \frac{1}{2})$, $\overline{PK}$ – perpendicular vector to line.

Find the area of the parallelogramm via cross product of the vectors $\overline{PQ}(-1,\frac{1}{2},\frac{1}{2}),\ \overline{q}(- \frac{2}{3},\frac{7}{6},- \frac{1}{2})$ :
$$\displaylines{\overline{PQ} \times \overline{q} = \begin{bmatrix}
-1  \\ \frac{1}{2} \\ \frac{1}{2}
\end{bmatrix} \times \begin{bmatrix}
- \frac{2}{3} \\ \frac{7}{6} \\ - \frac{1}{2}
\end{bmatrix} = \begin{vmatrix}
i&j&k \\ -1& \frac{1}{2} & \frac{1}{2} \\ - \frac{2}{3}& \frac{7}{6}& - \frac{1}{2}
\end{vmatrix} =\\ i\left(- \frac{1}{4} - \frac{7}{12}\right)- j\left(\frac{1}{2} + \frac{1}{3}\right)+ k\left(-\frac{7}{6}+\frac{1}{3}\right)=\\
-\frac{5}{6}i - \frac{5}{6}j - \frac{5}{6}k =\begin{bmatrix}
-\frac{5}{6} \\ -\frac{5}{6} \\ -\frac{5}{6}
\end{bmatrix}}$$
So, the area is:
$$\displaylines{S = | \overline{PQ}\times \overline{q}| = \sqrt{\left(- \frac{5}{6}\right)^2+\left(- \frac{5}{6}\right)^2+\left(- \frac{5}{6}\right)^2}=\\
\sqrt{3 \cdot \frac{25}{36}} = \frac{5\sqrt{12}}{12}}$$
Then:
$$S = \frac{5\sqrt{12}}{12} = |\overline{PK}|\cdot |\overline{q}| \Rightarrow |\overline{PK}| = \frac{5\sqrt{12}}{12 |\overline{q}|}$$
$$|\overline{q}| = \sqrt{\left(- \frac{2}{3}\right)^{2}+ \left(\frac{7}{6}\right)^{2}+\left(- \frac{1}{2}\right)^{2}}= \sqrt{\frac{37}{18}}$$
$$|\overline{PK}|= \frac{5\sqrt{12\cdot18}}{12\sqrt{37}} = \frac{30\sqrt{6}}{12\sqrt{37}} = \frac{5\sqrt{222}}{74}$$

**Answer:** $\displaystyle \frac{5\sqrt{222}}{74}$

---
## 4. Two vertices of a triangle are $(4,-3)$ and $(-2,5)$. If the orthocenter (intersection of altitudes) of the triangle is at $(1,2)$ find the coordinates of the third vertex:
![|400](Pasted%20image%2020241020175902.png)

Let $A(4,-3)$, $B(-2,5)$ and $P(1,2)$, then:

- $\overline{AP} = (-3,5)$
- $\overline{BP} = (3,-3)$

Let $C(x,y)$, then:

- $\overline{AC} = (x-4,y+3)$
- $\overline{BC} = (x+2, y-5)$

We know that $\overline{AP}\cdot \overline{BC} = 0$ and $\overline{BP}\cdot \overline{AC} =0$:

- $\overline{AP}\cdot \overline{BC} = -3(x+2) + 5(y-5) = -3x + 5y -31=0$
- $\overline{BP}\cdot \overline{AC} = 3(x-4) -3(y+3) = 3x-3y -21=0$

So, we get the system of equation:
$$\begin{cases}
-3x + 5y-31 =0 \\
3x - 3y -21 =0
\end{cases} \begin{cases}
2y = 52 \Rightarrow y =26 \\
3x  = 21+26*3 = 99 \Rightarrow x = 33
\end{cases}$$
Thus, the coordinates of the third vertex is $(33,26)$.

---
## In a regular tetrahedron $ABCD$, find the coordinates of the point $M$ in the basis $\{D,DA,DB,DC\}$, if the point $M$ has coordinates $(0,\frac{1}{3},\frac{1}{3})$ in the basis $\{A,AD,AB,AC\}$:
![|400](Pasted%20image%2020241020183134.png)

To find the coordinates of the $M$ in the another basis, we should find the vector $DM$ by new basis. Let us express it:
$AB = DB - DA$
$AC = DC - DA$
$AM = \frac{1}{3}AB + \frac{1}{3}AC = \frac{1}{3}DB + \frac{1}{3}DC - \frac{2}{3}DA$
$DM = DA+AM = DA + \frac{1}{3}DB + \frac{1}{3}DC- \frac{2}{3}DA = \frac{1}{3}DA + \frac{1}{3}DB + \frac{1}{3}DC$

Thus, the coordinates of the $M$ in the new basis is $(\frac{1}{3},\frac{1}{3},\frac{1}{3})$.




