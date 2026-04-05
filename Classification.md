Convert determining class of target to determining probability that target belongs to particular class. Then our problem got into regression problem.
$$z = w_{0}+ w_{1}x_{1}+\dots w_{n}x_{n}$$
$$\displaylines{w = \begin{bmatrix}w_{0}\\ w_{1} \\ \vdots \\ w_{n} \end{bmatrix}\quad x = \begin{bmatrix}x_{0}\\ x_{1} \\ \vdots \\ x_{n} \end{bmatrix}\\z= w^{T}x}$$
**Sigmoid**
$$\sigma (z) = \frac{1}{1+e^{-z}}$$
![|500](Pasted%20image%2020260405093059.png)

**Cross Entropy**
$$H(t, p) = - \sum t(i) \cdot log(p(i))$$
Binary Case:
$$\mathcal{L} = - (y \cdot log(p) + (1-y)\cdot log(1-p))$$
where:
- $y$ – either 1 or 0
- $p$ – predicted probability
- $log$ – natural logarithm
$$\mathcal{L} = - \frac{1}{n}\sum_{i=1}^{n}y_{i}\cdot log(\sigma(z_{i})) + (1-y)\cdot log(1- \sigma(z_{i}))$$
