---
tags:
  - 1stYear
---
# Review:
---
>[!abstract] Locus
>"When a point moves so as to satisfy some geometrical condition or conditions, the path traced out by the point is called the **locus** of the point."
>
>**Example:**
>- Suppose a point $P(x,y)$ moves such that its distances from two fixed points $A(2,3)$ and $B(5,-3)$ are equal. Then the geometrical law is lengths $PA = PB$ hence hence $PA^{2}= PB^{2}$
>  $$(x-2)^{2} + (y-3)^{2} = (x-5)^{2}+ (y+3)^{2} \Rightarrow$$
>  $$2x - 4y - 7 = 0 - \text{locus is a straight line}$$

---
# Straight line in plane:
---
## Definition:

Given a point $M_{0}$ and a vector $\text{a}$, set of all points $M$ for which: 
$$\overline{M_{0}M} = t\text{a}, \ \ t \in \mathbb{R}$$

---
## Parametric Vector Equation:

![](Pasted%20image%2020241009095851.png)

**Equation:** $r - r_{0} = tq$, where $t$ is a parameter.

---
## Parametric Equation in 3D:

>[!note] In *rectangular Cartesian coordinate system*
>$$\text{Equation of a line: }\begin{cases} 
 x = x_{0} + q_{x}t \\
 y= y_{0} + q_{y}t  \\
 z = z_{0} + q_{z}t 
\end{cases}$$

$$r - r_{0} = [x-x_{0}, y-y_{0}, z-z_{0}]^\top$$
$$q = [q_{x},q_{y},q_{z}]^\top$$
Просто уравнение прямой в пространстве как $y = kx + b$ только у нас $b$ это некоторая точка в пространстве, через которую проходит прямая когда $t = 0$,  $t$ это просто $x$, а $q$ это $k$ только в этом случае нулевой вектор, который задает направление прямой.

---
## Canonical equation of a line:

Eliminating $t$ from the system:
$\begin{cases} x = x_{0} + q_{x}t\\ y = y_{0} + q_{y}t \\ z = z_{0} + q_{z}t\end{cases}$

>[!note] we get the *Canonical equation*
>$$\frac{x-x_{0}}{q_{x}} = \frac{y-y_{0}}{q_{y}} = \frac{z-z_{0}}{q_{z}}$$

>[!note] Given two points: $M_{0}$ and $M_{1}$:
>$$\frac{x-x_{0}}{x_{1}-x_{0}} = \frac{y-y_{0}}{y_{1}-y_{0}} = \frac{z-z_{0}}{z_{1}-z_{0}}$$

^522015

Тут про то как построить прямую через две точки, если у нас есть координаты двух  точек то мы можем посчитать некий коэффициент для каждой точки ($xk_{1},\ yk_{2},\ zk_{3}$)

---
## General Equation, Normal (in 2D):

![](Pasted%20image%2020241017110325.png)

$$\displaylines{Ax + By + C = 0\\
\text{for point $M_{0}$ on a line:}\\
Ax_{0}+By_{0}+C = 0}$$
$$\displaylines{(r-r_{0}) = [x-x_{0}, y-y_{0}]^{\top}; n=[A,B]^{\top}\\
n \cdot (r-r_{0}) = 0}$$
---
## Angle Between Two Lines:

- The angle between two lines is the angle between direction vectors of the lines.
$$\cos \theta = \frac{p \cdot q}{|p||q|}$$
Where $p$ and $q$ are direction vectors of lines.

- The angle between two lines is the angle between normal vectors of the lines.
$$\cos \theta = \frac{n_{1}\cdot n_{2}}{|n_{1}||n_{2}|}$$
Where $n_{1}$ and $n_{2}$ are normal vectors of lines.

---
## Distance From a Point to a Line:

![](Pasted%20image%2020241017114740.png)
$$d = \frac{|n \cdot \overline{PQ}|}{\|n\|} = \frac{||n| \cdot |\overline{PQ}| \cdot \cos \theta|}{\|n\|}$$
$$d = |\overline{PQ}| \cdot |\cos \theta|$$
