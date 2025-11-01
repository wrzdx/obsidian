---
tags:
  - 1stYear
---
# General Equation of a Plane:

>[!abstract] In a rectangular Cartesian coordinate system
>$$A_{1}x+By + Cz + D = 0$$
>$x,y,z$ are arbitrary coordinates of a point on a plane.

> [!abstract] Given $M_{1}(x_{1},y_{1},z_{1})$ is a point in plane:
> $$Ax_{1}+By_{1}+Cz_{1} + D = 0$$

>[!important] We get *the general equation* of the plane:
>$$A(x-x_{1}) + B(y-y_{1}) + C(z-z_{1}) = 0$$

^0261bf

---
# Vector form:
![](Pasted%20image%2020241017140250.png)
$$r-r_{1}= [x-x_{1}, y-y_{1}, z-z_{1}]^{\top}$$
Hence, the general equation of the plane $A(x-x_{1}) + B(y-y_{1}) + C(z-z_{1}) = 0$ 
Can be presented in the vector form:
$$(r-r_{1})\cdot n = 0, \text{ where $n = \begin{bmatrix} A \\ B \\ C
\end{bmatrix}$}$$
If we expand the vector form of the plane equation, we will obtain the general form of the equation again.

---
# Equation of a Plane Passing Through Three Points:

$$\begin{vmatrix}
x-x_{1}&y-y_{1}&z-z_{1} \\ x_{2}-x_{1}&y_{2}-y_{1}&z_{2}-z_{1} \\ x_{3}-x_{1}&y_{3}-y_{1}&z_{3}-z_{1}
\end{vmatrix}=0$$
---
# Other forms of equation:

>[!abstract] Given two vector: *p,q* that are parallel to a plane, and a point $M_{1}(x_{1},y_{1},z_{1})$ on the plane
>Consider arbitrary vector $r = [x,y,z]$. Then three vectors $r-r_{1},p,q$ are coplanar.
>$$\begin{vmatrix}x-x_{1}&y-y_{1}&z-z_{1} \\ p_{x}&p_{y}&p_{z} \\ q_{x}&q_{y}&q_{z} 
\end{vmatrix} = 0$$

>[!abstract] Equation of a plane in the intercept form
>![|300](Pasted%20image%2020241019154250.png)
>$$\frac{x}{a} + \frac{y}{b} + \frac{z}{c} = 1$$
>We've just converted $a = \frac{D}{A},\ b =\frac{D}{B},\ c = \frac{D}{C}$

---
# Angle Between Two Planes:

>[!abstract] Definition 
>The angle between two planes equals the angle between their normal vectors.
>$$\cos \theta = \frac{n_{1}\cdot n_{2}}{\|n_{1}\|\|n_{2}\|}$$

---
# Distance From a Point To a Plane:

- Equation of plane: $Ax + By + Cz + D = 0$
- Point $Q(x_{1},y_{1},z_{1})$ is not in plane.
- Point $M(x,y,z)$ is an arbitrary point in plane
![|350](Pasted%20image%2020241019161325.png)
$$\displaylines{d = \frac{|n \cdot \overline{QM}|}{\|n\|}=\\ 
= \left|\frac{A(x-x_{1}) + B(y-y_{1}) + C(z-z_{1})}{\sqrt{A^{2}+ B^{2} +C^{2}}}\right|}$$
---
# Relative Position of Planes:
![400](Pasted%20image%2020241019161641.png)
- The planes are parallel and coincide if they have the same normal and $D$ coefficient
- The planes are parallel and not coincide if they have the same normal and the different $D$ coefficients
- The planes are not parallel if they have the different normal vectors.
---
# Relative Position of a Plane and a Line:

$\begin{cases}Ax + By + Cz + D = 0 \\ A_{1}x + B_{1}y + C_{1}z + D_{1} = 0\\ A_{2}x + B_{2}y + C_{2}z + D_{2}= 0\end{cases}$

There are three possible cases:
- If the rank of the coefficient matrix equals $3$, then $M_{0}(x_0,y_0,z_0)$ is the point of intersection of the plane and the line.
- If the system is consistent, and the rank of the coefficient matrix equals $2$, then the line $L$ lies in the plane $P$.
- If system is inconsistent then the line $L$ is parallel to the plane $P$.
---
# The Angle Between a Plane and a Line:

>[!abstract] Angle Between a Plane and a Line ($\beta = ?$)
>![|300](Pasted%20image%2020241019170533.png)
>- $n$ is a normal vector of the plane
>- $l$ is a direction of the line
>- $\beta$ is the angle between the plane and the line

---
# Linear Map:

- Given two vector spaces $E$ and $F$, a linear map between $E$ and $F$ is a function $f: E \to F$ satisfying the following two conditions:
	- $f(a+b) = f(a) + f(b),\ \forall a, b \in E$
	- $f(\lambda a) = \lambda f(a),\ \ \ \forall a \in E, \lambda \in \mathbb{R}$

