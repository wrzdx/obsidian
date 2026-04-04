## Underfitting and Overfitting

````col
```col-md
flexGrow=1
===
![](Pasted%20image%2020260404042155.png)
![](Pasted%20image%2020260404042519.png)
```
```col-md
flexGrow=1
===
![](Pasted%20image%2020260404042302.png)
![](Pasted%20image%2020260404042454.png)
```
```col-md
flexGrow=1
===
![](Pasted%20image%2020260404042314.png)
![](Pasted%20image%2020260404042531.png)
```
````

## Linear Regression
$$y = w_{0} + w_{1}x_{1} + w_{2}x_{2} + \dots + w_{n}x_{n}$$

- The response variable is quantitative
- The relationship between response and predictors is assumed to be *linear* in the inputs
- Thus we are restricting ourselves to a hypothesis space of linear functions

## Mean Squared Error (MSE)
$$\displaylines{
f(x_{i}) = w_{0}+ w_{1}x_{i}\\
MSE = \mathcal{L}(w_{0}, w_{1}) = \frac{1}{n}\sum^{n}_{i=1} (y_{i} - f(x_{i}))^{2}
}$$
We need to find the value of parameters that minimize this cost or *loss function*.
$$\underset{w_{0}, w_{1}}{argmin}\ \mathcal{L}(w_{0},w_{1})$$
*argmin* – shorthand for “find the argument that minimizes …”

## Derivative

| Point X     | $f’$ slightly left to X | $f’$ at X | $f’$ slightly right to X |
| ----------- | ----------------------- | --------- | ------------------------ |
| **maximum** | > 0                     | 0         | < 0                      |
| **minimum** | < 0                     | 0         | > 0                      |

## The least Square Solution
$$\mathcal{L}(w_{0}, w_{1}) = \frac{1}{n}\sum^{n}_{i=1} (y_{i} - (w_{0}+ w_{1}x_{i}))^{2}$$
1) Compute partial derivatives of the loss function with respect to $w_{0}$ and $w_{1}$
2) Set them to 0
3) And solve for $w_0$ and $w_{1}$
$$\mathcal{L}(w_{0}, w_{1}) = \frac{1}{n}\sum^{n}_{i=1} (w_{1}^{2}x_{i}^{2} + 2w_{1}x_{i}(w_{0}-y_{i}) + w_{0}^{2}- 2w_{0}y_{i} + y_{i}^{2})$$
Partial Derivatives
$$\frac{\partial\mathcal{L}}{\partial w_{0}}=2w_{0}+2w_{1} \frac{1}{n}(\sum) $$