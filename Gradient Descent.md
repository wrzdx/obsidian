- Learning the machine learning model by *iteratively* reducing the loss

$$\displaylines{w_{0}= w_{0} - \alpha \frac{\partial\mathcal{L}}{\partial w_{0}}\\
w_{1}=w_{1} - \alpha \frac{\partial\mathcal{L}}{\partial w_{1}}} $$
where $\alpha$ – *learning rate*