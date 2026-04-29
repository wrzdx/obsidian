>[!note] Hyperplane
>A hyper plane in $\mathbb{R}^{p}$ dimensions is a set of points $\{x_{1},x_{2},..., x_{p}\}$ that satisfy the following equation
>$$w_{0} + w_{1}x_{1} + w_{2}x_{2} + \cdots w_{p}x_{p}=0$$
>- If $p=2$, a hyperplane is *a line*
>- If $w_{0} = 0$, the hyperplane *goes through the origin*
>- The vector $w= (w_{1}, w_{2}, ..., w_{p})$ is called the *normal vector* – it points in direction orthogonal to the surface of the hyperplane.


## Separating hyperplane
If we have separating hyperplane

$$w_{0} + w_{1}x_{1} + w_{2}x_{2} + \cdots w_{p}x_{p}=0$$

Then
1. $x$ lies positive side of the plane if 
   $$w_{0} + w_{1}x_{1} + w_{2}x_{2} + \cdots w_{p}x_{p}>0$$
2. or other if 
   $$w_{0} + w_{1}x_{1} + w_{2}x_{2} + \cdots w_{p}x_{p}<0$$

Thus, our decision function for $x_{new}$ is,
$$y_{new}= sign(w_{0} + w_{1}x_{1} + ... w_{p}x_{p})$$

But, there could be infinite number of such hyperplanes.

>[!note] Margin
>- Margin is the *perpendicular distance* from the decision boundary to the closest point on either side of the decision boundary
>  ![](Pasted%20image%2020260429140221.png)

*Optimal Decision Boundary (Separating plane)* – one that maximize the margin.

**Mathematical Expression of Margin:**

````col
```col-md
flexGrow=1
===
![](Pasted%20image%2020260429140915.png)
```
```col-md
flexGrow=1
===
![](Pasted%20image%2020260429140947.png)
```
````


Thus,
$$2\gamma = \frac{1}{\|w\|}w^{T}(x_{1} - x_{2}) = \frac{1}{\|w\|}(w^{T}x_{1}+w_0 - (w^{T}x_{2}+w_0))$$ Now, recall our decision function 
$$y_{new} = sign(w_{0} + w_{1}x_{1} + ... + w_{p}x_{p})$$
It only cares about sign and does not care about the value, so we can scale $w$ and $w_{0}$ such that
$$w^{T} + w_{0} = \pm 1$$
Thus, 
$$\displaylines{2\gamma =  \frac{1}{\|w\|}(1 - (-1)) = \frac{2}{\|w\|} \\ \gamma =\frac{1}{\|w\|}}$$

So we want to maximize $\frac{1}{\|w\|}$

But we have constraint
$$y_{i}(w_{0} + w_{1}x_{1} + ... + w_{p}x_{p})\geq 1$$

But, it’s easier to solve the following (*equivalent*) optimization problem
$$\displaylines{\underset{w}{argmin} \frac{1}{2}\|w\|^{2} \\ \text{subject to } y_{i}(w_{0} + w_{1}x_{1} + \cdots w_{p}x_{p} \geq 1}$$