## With separatable variables: 
easy no need some algorithms


## Homogeneous DE:

If change $y=\lambda y$ and $x=\lambda x$ and we can cancel out $\lambda$ it means we have homogenous DE
To solve such type of equation we need to do the following change of variables: $y = tx$ and $y' = t'x + t$
Solve with respect to $t$ and get the solution

## DE that reduce to homogeneous:

If we have the following type of DE:
$$y' = \frac{a_{1}x + b_{1}y + c_{1}}{a_{2}x + b_{1}y + c_{2}}$$
If the determinant of this matrix:
$$\begin{vmatrix}
a_{1} & b_{1}\\ a_{2}& b_{2}
\end{vmatrix} \neq 0$$
We need to make the following change of variables:

$$\displaylines{x = \hat{x} + \alpha \\ y = \hat{y} + \beta}$$
Where $\alpha$ and $\beta$ can be found by solving the folloing system of equations:

$$\cases{a_{1}\alpha + b_{1}\beta + c_{1}=0 \\ a_{2}\alpha + b_{2}\beta + c_{2} = 0}$$
So, after the substitution we get just homogeneous equation

If the determinant of this matrix:
$$\begin{vmatrix}
a_{1} & b_{1}\\ a_{2}& b_{2}
\end{vmatrix} \neq 0$$
So do the following substitution
$$z = a_{1}x + b_{1}y $$Or$$ z = a_{2}x + b_{2}y$$

## Non-homogeneous DE of first order

$$r(x)y' +p(x)y =q(x)$$

### By Bernoulli's method

Substitution:
$$ \cases{y = uv \\ y' =u'v + uv'}$$
We get 
$$r(x)u'v + r(x)uv' + p(x)uv = q(x)$$
$$r(x)u'v + u(r(x)v' + p(x)v) = q(x)$$
Solve the following system
$$\cases{r(x)v' + p(x)v = 0 \\ r(x)u'v = q(x)}$$
The answer is 
$$y=uv$$
### By Lagrange's or method of variation of arbitrary constants:

We solve as it would be ordinary homogeneous equation by making right side $0$
$$r(x)y' +p(x)y =0$$
Solving this we get some solution:
$$\displaylines{y = f(x, u)\\ y' = ...}$$
Substitute to initial equation and we get simple equation with separable variables. Solve it w.r.t. $u(x)$ and substitute this value to $y=f(x,u)$ 




## Solve DE in full differentials

$$Mdx + Ndy = 0$$
We need to check whether it is full differantial
$$\frac{\partial M}{\partial y} = \frac{\partial N}{\partial x}$$
If it is then we do the following steps
1. Find $\int M dx$
2. $F = \int Mdx + \phi (y)$
3. $\frac{\partial F}{\partial y} = \frac{\int M dx}{\partial y} + \phi'(y)$ and it should be equal to $N$

Ладно, че то лень стало