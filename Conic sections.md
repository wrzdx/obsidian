---
tags:
  - 1stYear
---
# Part 1. Quadratic curves

In general, any quadratic ( second order ) curve is a set of points satisfying the equation:

$$Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0$$ ^e2b05d

---

# Part 2. Ellipse

## Definition

> [!note] *Ellipse. Canonical equation of an ellipse*
>
> An ellipse is a plane curve, which is represented by the equation:
>
> $$\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1$$
>
> in some Cartesian coordinate system.

![|400](Pasted%20image%2020241030100631.png)

---

## Parametric form of the equation of an ellipse

Given:

$$
\begin{cases}
x = a\cos t \\
y = b\sin t
\end{cases}
$$

and eliminating the parameter $t$, we get:

$$
\begin{cases}
\frac{x^2}{a^2} = \cos^2 t \\
\frac{y^2}{b^2} = \sin^2 t
\end{cases}
$$

This gives you a nice way to plot a point M(x, y) on an ellipse.

**Shifted ellipse:** with center at $M(x_{0},y_{0})$.

$$\frac{(x - x_0)^2}{a^2} + \frac{(y - y_0)^2}{b^2} = 1$$

---

## Foci and eccentricity

![|400](Pasted%20image%2020241030102218.png)

> [!note] *Foci* (aka focuses)
>
> Given an ellipse with major axis $2a$. Foci (plural from *focus*) are points $F_1(-c, 0)$ and $F_2(c, 0)$ that satisfy:
>
> $$c^2 = a^2 - b^2$$

> [!note] *Eccentricity*
>
> Given an ellipse with major axis $2a$ and foci $F_1(-c, 0)$, $F_2(c, 0)$, the eccentricity of the ellipse is denoted as $\varepsilon$: 
>
> $$\varepsilon = \frac{c}{a}, \ \ \ 0\leq\varepsilon<1$$
> 
> 

![|500](Pasted%20image%2020241030103439.png)

---

## Focal distances

![|400](Pasted%20image%2020241030103555.png)

> [!note] *Focal distances*
>
> Distance from a point $M(x, y)$ on an ellipse to each of the foci:
>
> $$r_1 = a + x\varepsilon$$
> $$r_2 = a - x\varepsilon$$

> [!summary]- *Proof (click to expand)*
> 
> We need to show that $r_1 = a + x\varepsilon$.
> 
> $$r_1 = \sqrt{(x + c)^2 + y^2}$$
> *This is the distance from point $M(x, y)$ to the focus $F_1(-c, 0)$.*
> 
> $$y^2 = \left(a^2 - x^2\right)\frac{b^2}{a^2}$$
> *Expressing $y^2$ through $x$ using the equation of the ellipse.*
> 
> $$c = a\varepsilon; \text{Note also: } b^2 = a^2 - c^2 = a^2(1 - \varepsilon^2)$$
> *This is the relationship between the eccentricity and the semi-axes of the ellipse.*
> 
> $$y^2 = \left(a^2 - x^2\right)\frac{b^2}{a^2} = a^2 - a^2\varepsilon^2 - x^2 + x^2\varepsilon^2$$
> *Substitute $b^2$ to simplify the expression for $y^2$.*
> 
> $$r_1^2 = (x + c)^2 + y^2 = x^2 + 2xc + c^2 + a^2 - a^2\varepsilon^2 - x^2 + x^2\varepsilon^2 = (a + x\varepsilon)^2$$
> *Expand and simplify, resulting in $r_1 = a + x\varepsilon$.*
> 
> Note, that $r_2 = a - x\varepsilon$ and hence $r_1 + r_2 = 2a$.
> *Confirming that the sum of distances to the foci remains constant.*

---

## Directrices

![|400](Pasted%20image%2020241030105209.png)

The equations of the directrices are:

$$x = \frac{a}{\varepsilon}, \quad x = -\frac{a}{\varepsilon}$$
![|400](Pasted%20image%2020241030105402.png)
Why $\displaystyle \frac{r_1}{d_1} = \frac{r_2}{d_2} = \varepsilon$?
$$d_1 = \frac{a}{\varepsilon} + x = \frac{1}{\varepsilon}r_1; \quad d_2 = \frac{a}{\varepsilon} - x = \frac{1}{\varepsilon}r_2$$

---

## Tangent lines

![|400](Pasted%20image%2020241030113458.png)

---

# Part 3. Hyperbola

## Definition. Canonical equation

> [!note] *Definition. Canonical equation*
> 
> A hyperbola is a plane curve, which can be represented in some Cartesian coordinate system by one of the below equations:
> 
> $$\frac{x^2}{a^2} - \frac{y^2}{b^2} = 1 \quad \text{or} \quad \frac{x^2}{a^2} - \frac{y^2}{b^2} = -1$$
> ![|400](Pasted%20image%2020241030113744.png)
> If $a = b$, then it is an equilateral hyperbola.
> 
>**Shifted hyperbola:**
$$\frac{(x - x_0)^2}{a^2} - \frac{(y - y_0)^2}{b^2} = \pm 1$$
Center of the hyperbola is at $M(x_0, y_0)$.

---

## Foci and eccentricity

![|400](Pasted%20image%2020241030114639.png)
> [!note] *Foci* (aka focuses)
>
> Given a hyperbola $\frac{x^2}{a^2} - \frac{y^2}{b^2} = 1$. Foci are points $F_1(-c, 0)$ and $F_2(c, 0)$ that satisfy:
>
> $$c^2 = a^2 + b^2$$

> [!note] *Eccentricity*
> 
> Given $\frac{x^2}{a^2} - \frac{y^2}{b^2} = 1$. Eccentricity of the hyperbola $\varepsilon$:
> 
> $$\varepsilon = \frac{c}{a}$$
> 
> Note, $\varepsilon > 1$

---

## Focal distances

![|400](Pasted%20image%2020241030114639.png)

> [!note] *Focal distances*
> 
> Distance from a point $M(x, y)$ on a hyperbola to each of the foci:
> 
> $$r_1 = \pm(x\varepsilon + a)$$
> $$r_2 = \pm(x\varepsilon - a)$$
> 
> For any point on the hyperbola:
> 
> $$r_1 - r_2 = \pm 2a$$
