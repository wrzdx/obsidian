- Goal: given a set of training data points from $C$ classes, compute the predictive probabilities for each of the $C$ potential classes 
  $$p(y_{new} = c | x_{new}, X, y)$$ 
**Bayes equation:**
$$p(y_{new} = c | x_{new}, X, y) = \frac{p(x_{new}|y_{new} = c, X,y)p(y_{new}=c|X,y)}{p(x_{new}|X, y)} $$
or 
$$p(y_{new}=c|x_{new}) = \frac{p(x_{new}|c)p(c)}{p(x_{new})}$$
$$p(y_{new}=c|x_{new}) = \frac{p(x_{new}|c)p(c)}{\sum_{c'=1}^{C}p(x_{new}| c')p(c')}$$

**Likelihood:**
$$p(x_{new}| c) = p((x_{1}, ..., x_{p})_{new}|c) = \prod_{i=1}^{p}p(x_{1}|c)$$
- if we assume $x_{i}$ is independent 
- But every $p(x_{i})$ is between 0 and 1 the result will be very small number and we could lose precision, so we calculate log of product instead of just log

**Advantages**
- It is easy and fast to predict class of test data set. It also perform well in multi class prediction
- When assumption of independence holds, a Naive Bayes classifier performs better compare to other models like logistic regression and you need less training data.
- Allows online learning

