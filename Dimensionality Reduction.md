## Curse of Dimensionality
- High Dimensional Data is 
	- Difficult to visualize
	- Difficult to analyze
	- Difficult to understand – to get insight from the data (correlation, predictions)
	- Everything looks the same

**Solution:**
- To solve the problem, we usually transform every $p$-dimensional point $x_{i}$ to a new $d$-dimensional point $x_{i}'$
- Such that $d < p$
  $$X' = \{(x_{i}')|x_{i}' \in \mathbb{R}^{d}\}^{n}_{i}$$
- The process called *projection*


## Principal Component Analysis
- When projecting data from $p$-dimensional to a $d$-dimensional space, *PCA* defines $d$ vectors, each represented as $w_{j}$ where $j=1,...,d$
- Each vector is $p$-dimensional – that is, $w \in \mathbb{R}^{p}$
- The $i$-th projected  point is represented as $x_{i}' = [x_{i1}', x_{i2}', \cdots, x_{id}']$
  $$x_{id}' = w^{T}_{d}x_{i}$$
>[!note] 
>Короче находим $d<p$ векторы, желательно ортогональные, затем через них выражаем старые векторы, а коэффициенты (координаты) будут как раз значения новых фичей  