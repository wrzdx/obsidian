- Learning the machine learning model by *iteratively* reducing the loss

$$\displaylines{w_{0}= w_{0} - \alpha \frac{\partial\mathcal{L}}{\partial w_{0}}\\
w_{1}=w_{1} - \alpha \frac{\partial\mathcal{L}}{\partial w_{1}}} $$
where $\alpha$ – *learning rate*

For single predictor:
$$\displaylines{w_{0} = w_{0} - \alpha \frac{1}{n} \sum^{n}_{i=1}(\hat{y_{i}} - y_{i}) \\w_{1} = w_{1} - \alpha \frac{1}{n} \sum^{n}_{i=1}(\hat{y_{i}} - y_{i})x_{i}}$$

For multiple predictor:
$$w_{j} = w_{j} - \alpha \frac{1}{n} \sum^{n}_{i=1}(\hat{y_{i}} - y_{i})x_{i}^{j}$$

