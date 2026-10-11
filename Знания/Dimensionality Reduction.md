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
- Data should have zero mean

>[!note] 
>Короче находим вектор который будет сохранять максимальный variance $\sigma ^{2}$, затем уже находим следующий вектор которые также будет выдавать максимальный variance, но уже чтобы он был ортогонален предыдущему, то есть $w_{i}w_{j}=0\ |\ \forall i\neq j$, повторяем до тех пор пока не получим $d$ количество векторов

We want to maximize variance
$$\sigma ^{2}= \frac{1}{n}\sum_{i=1}^{n}(x_{i}' - \mu_{x'})^{2}$$
But
$$\displaylines{\mu_{x'}=\frac{1}{n}\sum_{i=1}^{n}x_{i}'= \frac{1}{n}\sum_{i=1}^{n}w^{T}x_{i} = w^{T}(\frac{1}{n}\sum_{i=1}^{n}x_{i}) =w^{T}\mu_{x} = 0  
}$$
So,
$$\displaylines{\sigma^{2} = \frac{1}{n}\sum_{i=1}^{n}(x_{i}')^{2} = \frac{1}{n}\sum_{i=1}^{n}(w^{T}x_{i})^{2} = \frac{1}{n}\sum_{i=1}^{n}(w^{T}x_{i}x_{i}^{Tw)}=\\
=w^{T}(\frac{1}{n}\sum_{i=1}^{n}x_{i}x_{i}^{T})w = w^T Cw
}$$

To maximize variance we can only try to maximize $C$ since
$$w^{T}w = 1$$
So, our optimization problem is
Find $w$ that maximize the following 
$$\mathcal{L} = w^{T}Cw - \lambda (w^{T}w - 1 )$$
Solve
$$\displaylines{\frac{\partial L}{\partial w} = 2Cw - \lambda 2w = 0 \Rightarrow \\
\Rightarrow Cw = \lambda w
}$$

$C$ doesn’t change direction, only scales, so $w$ is *eigenvector* of $C$ and $\lambda$ is *eigenvalue*, and also we confirm that each $w_{i}$ eigenvector of $C$ is also orthogonal to others.
 
But $C$ is $p\times p$ matrix, so it has $p$ eigenvectors, but we need the most appropriate $d$ vectors.

We had 
$$\cases{\displaylines{\sigma ^ {2}= w^{T}Cw \\ w^{T}w = 1}} \Rightarrow \sigma ^{2}w^{T}w = w^{T}Cw \Rightarrow \sigma ^{2}w = Cw$$

Thus,
$$\sigma ^{2}w = \lambda w = Cw$$

We can conclude that the most appropriate $d$ vectors – with the most variance – are vectors with the largest $\lambda$ eigenvalues.

>[!summary] Algorithm
>1) Transform the data to have zero mean by subtracting $\mu_{x}$ from each point
>2) Compute the sample covariance matrix $C$
>3) Find $p$ (eigenvector, eigenvalue) pairs of $C$
>4) Find the eigenvectors corresponding to $d$ highest eigenvalues $w_{1}, w_{2}, \cdots, w_{d}$
>5) Compute $X'$ as $X' = XW$, where $W = [w_{1},w_{2},\cdots, w_{d}]$

