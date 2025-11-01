---
tags:
  - 1stYear
---
# Simple Questions:

1. **What is the geometrical interpretation of the dot product ?**
   ![](The%20Dot%20product%20and%20its%20properties..md#^b7a556)
   This means that the smaller the angle between them, the greater the value of their scalar product
---
2. **How to determine whether the vectors are linearly dependent?**
   ![](Introduction.%20Vector%20Spaces.%20Linear%20Independence.%20Basis..md#^288eaa)
   We can solve a system of equations and then show whether there is a combination of vectors that leads to a zero vector or not.
   Also, we may check determinant or rank of matrix of these vector
---
3. **What is the basis of vector space?**
   Set of linear independent vectors such that any vector of space can be represented as linear combination of them  
---
4. **A matrix is singular if ..** 
   The determinant of this matrix is equal to zero. It means there is no inverse matrix for this one.
---
5. **What is the difference between matrices and determinants?**
   A matrix is an array of elements represented as rows and columns. Determinants are considered as scalar factors of a matrix. Determinant can be found only for a square matrix having an equal number of rows and columns.
--- 
6. **Matrices $A$ and $C$ have dimensions of $m \times n$ and $p \times q$ respectively, and it is known that the product $ABC$ exists. What are possible dimensions of $B$ and $ABC$?**
   Let dimensions of $B$ be $a \times b$. We can multiply $A$ and $B$ if $n=a$, and result matrix will have $m \times b$ dimensions. By the same logic in the second multiplication, $b=p$ and result have $m \times q$ dimensions.
   Thus, $B$ is $n \times p$ matrix.
--- 
7. **How to determine the rank of a matrix?** 
   Rank is the maximum number of linearly independent rows or columns in a matrix.
   It means we can evaluate minors of different order, and if there is at least one non-zero minor of some particular order, the rank is equal to this order 
   Another method to find rank is Gaussian, we try to transform origin matrix to normal form, and amount of non-zero column or row is rank. 
---
8. **What is the meaning of the inverse matrix?**
   ![](Change%20of%20Basis.%20Matrix%20Inverses..md#^935ff3)
--- 
9. **How to restate a system of linear equations in the matrix form?**
   We should rearrange terms of each equation in the system in some common order of variable in left side of equation, and constant should be in right side, and set of coefficients of variable in left side of each equation is one row of matrix. There are also other matrices $n \times 1$ which represent variables themself and constant terms.
   Thus we have 3 matrices, multiplication of coefficients matrix and variables matrix gives us matrix of constant terms.
   $$A \times B=C$$    
--- 
10. **Rank of a matrix A is a ...**
    Rank is the maximum number of linearly independent rows or columns in a matrix.
--- 
11. **What is the geometrical interpretation of the cross product?**
    It's new vector that is perpendicular to both initial ones, and its magnitude is equal to the area of parallelogramm that is formed by initial vectors: $$a \times b = \hat{n} \cdot |a||b|\sin \theta$$
    where:
    - $\hat{n}$ is unit orthogonal vector,
    - $a$ and $b$ are initial vectors,
    - $\sin \theta$ is the angle between vectors.
---
12. **What is the transition matrix?** 
    A **transition matrix** is a square matrix that describes how a set of basis vectors in one coordinate system transforms into another set of basis vectors in a different coordinate system.
---
13. **How to represent a line in the vector form?** 
    A **line in vector form** is represented using a vector equation that describes all the points on the line. The general form is:
    $$r(t) = r_{0}+t \overline{v},$$
    where:
    - $r(t)$ is the position vector of a point on the line as a function of the parameter $t$,
    - $r_{0}$ is the position vector of a fixed point (a point on the line),
    - $\overline{v}$ is the direction vector, which indicates the direction of the line
    - $t$ is a scalar parameter that can take any real value.
---
14. **What is the result of intersection of two planes in vector form?** 
    Just line represented by vector form
---
15. **How to derive the formula for the distance from a point to a line?**
    We choose some point on a line and create vector from this point and given, then we evaluate the magnitude of cross product of this vector and direction vector of line, it will be area of parallelogramm, and if we devide this value by magnitude of direction vector it will be exact distance (altitude). 
---
16. **How to interpret geometrically the distance between lines?**
    Length of the perpendicular between lines.
---
17. **List all possible inter-positions of lines in the space.** 
    these lines are skew or concurrent or intersecting or coincident or parallel  
---
18. **What is the difference between general and normalized forms of equations of a plane?** 
    ![](Plane%20in%203D%20space.%20Equations..md#^0261bf)
    $$\hat{A}(x-x_{1}) + \hat{B}(y-y_{1}) + \hat{C}(z-z_{1}) = 0$$
    $\hat{A}= \frac{A}{\|n\|}$ where $\|n\|$ is the magnitude of normal vector.
---
19. **How to rewrite the equation of a plane in a vector form?**
    $$r(s, t) = {P_{0}} + s\cdot{d_{1}}+ t\cdot{d_2}$$
    $where\ {P_{0}}\ -\ a\ point\ on\ the\ plane;\ {d_{1},}\ {d_{2}}\ are\ the\ direction\ vectors$ 
---
20. **What is the normal to a plane?** 
    The vector that is perpendicular to each vector in the plane.
---
21. **How to interpret the cross products of two vectors?**
    A new vector that is orthogonal to both initial vectors, direction can be defined by rigth hand rule, and whose magnitude is equal to area of parallelogramm that is formed by initial vectors. 
---
22. **What is the meaning of the scalar triple product of three vectors?** 
    Volume of paralelepiped that is formed by these vectors
---
23. **Formulate the canonical equation of the given quadratic curve (e.g. an ellipse or a pair of intersected lines).**
    General form![](Conic%20sections.md#^e2b05d)
	    We should determine kind of curve via sign of determinant ($D>0$ is hyperbola, $D=0$ parabola or pair of lines, $D<0$ is ellipse), then if $B \neq 0$ then rotate the curve to eliminate this coefficient by finding angle:
	    $$\tan 2\theta = \frac{B}{A-C}$$
	    and then substituting $x$ and $y$ into equation, where:
	    $$\begin{bmatrix}
\cos \theta & -\sin \theta \\ \sin \theta & \cos \theta
\end{bmatrix} \begin{bmatrix}
x' \\ y'
\end{bmatrix} = \begin{bmatrix}
x \\ y
\end{bmatrix}$$
We complete the squares in the newly obtained equation. And it will canonical form of curve.
---
24. **Which orthogonal transformations of coordinates do you know?** 
    Orthogonal transformations of coordinates preserve the **lengths of vectors** and the **angles between them**, ensuring that the coordinate system remains orthogonal.
    $$Q \times Q^{T} = I$$
    Rotating and reflection.
---
25. **How to perform a transformation of the coordinate system?**
    *Translation:* Add a shift vector $T$ to each point.
    $x' = x+T$
    *Rotation:* Multiply the coordinates by a rotation matrix $R$.
    $x' = Rx$
    *Scaling:* Multiply each coordinate by a scale factor $s$.
    $x' = sx$
    *Reflection:* Multiply by a reflection matrix.
    *Affine transformation:* all previous transformations.
    $x' = Ax + T$    
---
26. **General equation of the quadric surfaces.**
    $$Ax^{2}+By^{2}+Cz^{2}+Dxy+Exz+Fyz+Gx+Hy+Iz+J=0$$
---
27. **Canonical equation of a sphere and ellipsoid.**
    For ellipsoid:
    $$\frac{(x-h)^{2}}{a^{2}}+ \frac{(y-k)^{2}}{b^{2}}+ \frac{(z-l)^{2}}{c^{2}} = 1$$
    For sphere, $a=b=c=r$
---
28. **Canonical equation of a hyperboloid and paraboloid.**
    One sheet hyperboloid
    $$\frac{x^{2}}{a^{2}}+ \frac{y^{2}}{b^{2}} - \frac{z^{2}}{c^{2}} = 1$$
    Two sheet hyperboloid
    $$\frac{x^{2}}{a^{2}}+ \frac{y^{2}}{b^{2}} - \frac{z^{2}}{c^{2}} = -1$$
    Elliptic paraboloid
    $$\frac{x^{2}}{a^{2}}+ \frac{y^{2}}{b^{2}} = 2z$$
    Hyperbolic paraboloid
    $$\frac{x^{2}}{a^{2}} - \frac{y^{2}}{b^{2}} = 2z$$
---
29. **Surfaces of revolution with their equations.** 
    *Surfaces of revolution* are surfaces generated by rotating a curve around an axis.
    *Sphere:* $x^{2}+y^{2}+z^{2} = r^{2}$
    *Cylinder:* $x^{2} + y^{2}=r^{2}$
    *Cone:* $z^{2} = \frac{x^{2}}{a^{2}} + \frac{y^{2}}{b^{2}}$ 
    *Ellipsoid:* $\frac{x^{2}}{a^{2}} + \frac{y^{2}}{b^{2}} + \frac{z^{2}}{c^{2}} =1$
    *Elliptic Paraboloid:* $\frac{x^{2}}{a^{2}}+ \frac{y^{2}}{b^{2}} = 2z$
    *One and two sheet Hyperboloids:* $\frac{x^{2}}{a^{2}}+ \frac{y^{2}}{b^{2}} - \frac{z^{2}}{c^{2}} = \pm 1$
---
30. **Canonical equation of a cone and cylinder**. 
    $$z^{2} = \frac{x^{2}}{a^{2}} + \frac{y^{2}}{b^{2}}$$
    $$x^{2} + y^{2}=r^{2}$$
---
31. **What is the type of a quadric surface given by a certain equation?** 
    
---
32. **How to compose the equation of a surface of revolution?** 
---
33. **What is the difference between a directrix and generatrix?** 
---
34. **How to represent a quadric surface in the vector form?** 
    
---
35. **What is the polar form of the equation of the line x=1**
---
# Hard Questions:

1. **Let V={v_1,v_2, ..., v_n} be a set of vectors. Give a definition of a span S(V)** 
---
2. **Give a definition of a basis of vector space** 
---
3. **Given that BC and CB are valid, prove that Tr(BC) = Tr(CB)** 
---
4. **Vectors v_1, v_2, ..., v_n are linearly independent if...** 
---
5. **Give a definition of an orthogonal matrix. Provide an example.** 
---
6. **Give definition of a trace of a matrix and prove its linearity.** 
---
7. **Give a definition of the affine transformation. Provide an example.** 
---
8. **Vector form of a circular cylinder** 
---
9. **Vector form of a cone** 
---
10. **Give a definition of an ellipsoid of revolution. Draw an example.** 
---
11. **How is linear independence related to matrix rank?** 
---
12. **Explain the change of basis (in 3D case).** 
---
13. **Define a rotation matrix in 2D space.** 
---
14. **Distance between skew lines**