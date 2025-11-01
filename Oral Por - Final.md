---
tags:
  - 1stYear
---

| 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  | 13  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 2   | 1   | 1   | 1   | 1   | 2   | 1   | 1   | 1   | 1   | 2   | 1   |
$M = 34$

---
## Is real number $\frac{1}{\sqrt{M}}$ irrational?
Assume the number is rational, then it can be represented as fraction of coprime integers $\displaystyle \frac{a}{b}>0,\ b \neq 0$. It's greater than zero because square root of any number should be greater zero and therefore our number is also greater then zero, and denominator can't be equal to zero, it causes undefined value.

So,
$$\frac{1}{\sqrt{M}}= \frac{1}{\sqrt{34}} = \frac{a}{b} \mid \text{Square both sides}$$
$$\frac{1}{34} = \frac{a^{2}}{b^{2}} \Rightarrow b^{2}=34a^2$$
Since $b^{2}$ is divisible by $34$, and $34$ can be factorized into the primes $2$ and $17$, $b^{2}$ must also be divisible by both $2$ and $17$. By the **Fundamental Theorem of Arithmetic**, the factorization of integers into primes is unique, so for $b^{2}$ to include both $2$ and $17$ as factors, $b$ must also include both $2$ and $17$ as factors. Thus, $b$ is divisible by their product $34$.

As we know $b$ is divisible by $34$, we can represent $b=34k$, where $k$ is some integer number.
Let us substitute it back,
$$b^{2}= (34k)^{2} = 34a^{2}$$
Divide both sides by $34$,
$$34k^{2} = a^2$$
By the same logic as with $b$, $a$ is divisible by $34$. 

Contradiction! We said, that $a$ and $b$ is coprime, but they can both be divided by $34$.  

Thus, our number is irrational.

## Find (using definition) derivative of the function $\lambda x \in \mathbb{R}. (\sqrt{Mx}(x+M))$.

The physical meaning is speed of changing, the geometrical meaning is tangent or slope of function at some point.

Definition
$$f'(x) = \lim_{\Delta x \to0}  \frac{f(x+\Delta x)-f(x)}{\Delta x}$$
Our function
$$f(x) =\sqrt{Mx}(x+M) = \sqrt{34x}(x+34)$$
$$f'(x) = \lim_{h \to0}\frac{\sqrt{34(x+h)}(x+h+34)-\sqrt{34x}(x+34)}{h}$$
If we substitute directly $h=0$, we get undefined value kind of $\frac{0}{0}$

In this case we can use Lopital's rule:
$$\lim_{h \to a}\frac{f(h)}{g(h)} = \lim_{h \to a}\frac{f'(h)}{g'(h)}$$
![|400](Pasted%20image%2020241208005041.png)
Let
$$k(h) = \sqrt{34(x+h)}(x+h+34)-\sqrt{34x}(x+34)$$
Then
$$k'(h) = (\sqrt{34(x+h)}(x+h+34))' - (\sqrt{34x}(x+34))'$$
We know $(f(x)g(x))' = f'(x)g(x)+f(x)g'(x)$, so
$$(\sqrt{34(x+h)}(x+h+34))' = (\sqrt{34(x+h)})'(x+h+34) + (\sqrt{34(x+h)})(x+h+34)'$$
Let us evaluate the first part
$$(\sqrt{34(x+h)})'(x+h+34) = \frac{1}{2\sqrt{34(x+h)}}\cdot34\cdot(x+h+34)=\frac{17x+17h+578}{\sqrt{34(x+h)}}$$
And second part
$$(\sqrt{34(x+h)})(x+h+34)' =\sqrt{34(x+h)}$$
Substitute back
$$k'(h)=\frac{17x+17h+578}{\sqrt{34(x+h)}} + \sqrt{34(x+h)} - 0$$
Let denominator be
$$g(h) = h$$
Then
$$g'(h) = 1$$
Substitute all back
$$f'(x) = \lim_{h \to0} \frac{k(h)}{g(h)} = \lim_{h \to0} \frac{k'(h)}{g'(h)} = \lim_{h \to0}(\frac{17x+17h+578}{\sqrt{34(x+h)}} + \sqrt{34(x+h)})$$
Now, we can directly substitute $h=0$
$$f'(x) = \frac{17x+578}{\sqrt{34x}} + \sqrt{34x} = \frac{578+51x}{\sqrt{34x}} = \frac{\sqrt{34x}(578+51x)}{34x} = \frac{\sqrt{34x}(34+3x)}{2x}$$
## Using variable substitution find $\int f(x)dx$ for the following $f(x)$:

### a. $\displaystyle \frac{M}{M+\sqrt{x}}$

$$\frac{M}{M+\sqrt{x}} = \frac{34}{34+\sqrt{x}}$$
Let $u = 34+ \sqrt{x}$ and $du = \frac{dx}{2\sqrt{x}}$, $2\sqrt{x}du = 2(u-34)du = dx$ 

$$\int\frac{34}{34+\sqrt{x}}dx = \int \frac{34}{u}\cdot2(u-34)du = \int68- \frac{2312}{u} du = \int68 du -2312\int \frac{du}{u} = $$
$$=68u - 2312\ln|u| + c, \text{ where } c \in \mathbb{R}$$
Substitute back
$$68u - 2312\ln|u| + c = 2312 + 68\sqrt{x} + 2313\ln|34+\sqrt{x}| + c, \text{ where } c \in \mathbb{R}$$

### b. $\displaystyle\frac{M}{1+Me^{x}}$
$$\displaystyle\frac{M}{1+Me^{x}} = \frac{34}{1+34e^{x}}$$
Let $u = 1+34e^{x}$, 
and $du = 34e^{x}dx \Rightarrow  \frac{du}{u-1} = dx$  
So, 
$$\int\frac{34}{1+34e^{x}}dx = \int\frac{34}{u(u-1)}du$$
Let's try to decompose this expression into the following type (Partial Fractions Method)
$$\frac{34}{u(u-1)} = \frac{A}{u} + \frac{B}{u-1}$$
We can quickly determine $A$ and $B$ by the following trick:
1. At first we should multiply both sides by one of the denominators of the unknown coefficient, let it be $u$
   $$\frac{34}{u-1} = A + \frac{B \cdot u}{u-1}$$
2. And just substitute $0$ into $u$
   $$-34 = A$$
3. We perform the same action in order to find another coefficient
   $$\frac{34}{u} = A\frac{u-1}{u} + B$$
   $$34 = B$$
Now, since we know these coefficients we can rewrite our initial integral:
$$\int\frac{34}{u(u-1)}du = \int- \frac{34}{u} + \frac{34}{u-1} du = -34\int \frac{du}{u} + 34 \int \frac{du}{u-1}$$
The first term we can define
$$-34\int \frac{du}{u} = -34\ln |u| +c$$
To evaluate the second one, we can add new variable:
Let $v = u-1$, $dv = du$
$$34\int \frac{du}{u-1} = 34\int \frac{dv}{v} = 34\ln|v| + c$$
Substitute back
$$34\ln|v|+c = 34\ln|u-1| + c$$
So,
$$\int\frac{34}{u(u-1)}du =-34\ln |u|+34\ln|u-1| + c = 34\ln|\frac{u-1}{u}| +c$$
Substitute back
$$34\ln|\frac{u-1}{u}| +c = 34\ln|\frac{34e^{x}}{1+34e^{x}}|+c$$
