## What is Machine Learning?
- Computer programs that improve their performance at some task through experience

## Experience
Data

$$D = \{(x_{i}, y_{i}\}^{N}_{i=1}$$
- $N$ – number of available examples
- $y_{i}$ – targets
- $x_{i}$ – predictors

## Performance
- Needs to be defined according to the given task 
- For example: the ratio of correctly identified malwares

## Goal of Learning
- Learning or inferring a “functional” relationship between predictors and target

$$\displaylines{
D = \{(x_{i}, y_{i}\}^{N}_{i=1}\\ 
x \in \mathbb{R}^{d}\\
y = f(x)}$$

Goal of learning – $\hat{f}\approx f$

$$\displaylines{y=f(x; parameters)\\
y = f(x;w)\\
y = f(x;w_{0}, w_{1}) = w_{0} + w_{1}x}$$
![](Pasted%20image%2020260329181004.png)

## Classification and Regression
![|600](Pasted%20image%2020260329181110.png)

## Assessing the Quality of Learning

- Let $T_{r} = \{x_{i}, y_{i}\}^{N}_{i=1}$ be the training data we used to estimate $\hat{f}(x)$.
- To access the quality of estimate, we can compute 
  $$\mathrm{MSE_{Tr}} = \mathrm{Ave}_{i\in \mathrm{Tr}}[y_{i} - \hat{f}(i)]^{2}$$
- But this is not a reliable approach – This leads to *overfitting*.
- We should try to use the test data $T_{e} = \{x_{i}, y_{i}\}^{M}_{i=1}$
  $$\mathrm{MSE_{Te}} = \mathrm{Ave}_{i\in \mathrm{Te}}[y_{i} - \hat{f}(i)]^{2}$$
- Putting it all together – there are two phase: *training* and *evaluation*