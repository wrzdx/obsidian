- we choose a complex model but train it such that it will not overfit

$$Success = Goodness\ of\ the\ Fit + \lambda Simplicity\ of\ the\ model$$
$$Goodness\ of\ the\ Fit = e.g.\ MSE$$
$$\lambda Simplicity\ of\ the\ model = e.g.\sum_{j=1}^{p}w_{j}^{2}$$
## L2 Regularization
$$\mathcal{L} = \frac{1}{n} \sum_{i=1}^{n}(y_{i} - w^{T}x_{i})^{2} + \lambda \sum_{j=1}^{p}w^{2}_{j}$$
- $\lambda \geq 0$ is a tuning parameter
- L2 called *ridge* regression
- for irrelevant input weights will be small but not 0


## L1 Regularization
$$\mathcal{L} = \frac{1}{n} \sum_{i=1}^{n}(y_{i} - w^{T}x_{i})^{2} + \lambda \sum_{j=1}^{p}w_{j}$$
- $\lambda \geq 0$ is a tuning parameter
- L1 called *lasso* regression
- for irrelevant input weights likely will be 0
- the model called *sparse* – many zero weights

