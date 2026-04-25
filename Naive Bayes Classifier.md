- Goal: given a set of training data points from $C$ classes, compute the predictive probabilities for each of the $C$ potential classes 
  $$p(y_{new} = c | x_{new}, X, y)$$ 
**Bayes equation:**
$$p(y_{new} = c | x_{new}, X, y) = \frac{p(x_{new}|y_{new} = c, X,y)p(y_{new}=c|X,y)}{p(x_{new}|X, y)} $$
or 
$$p(y_{new}=c|x_{new}) = \frac{p(x_{new}|c)p(c)}{p(x_{new})}$$
