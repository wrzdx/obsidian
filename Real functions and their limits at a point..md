---
tags:
  - 1stYear
---
# From sequences to functions and their limits in $\mathbb{R}_{\pm\infty}$:

>[!abstract] Sequence limit
>A point $x$ of $\mathbb{R}_{\pm\infty}$ is a limit of a real sequence $(x_{n})_{n\in \mathbb{N}}$ 
>if for any neighborhood $V$ of $x$ for some neighborhood $U$ of $+\infty$ holds $(x_{n})_{n\in \mathbb{N}}(U)\subseteq V$.

>[!abstract] Function limit
>A point $y$ of $\mathbb{R}_{\pm \infty}$ is a limit of a real function $f:D\to \mathbb{R}$ when $x$ tending to $d\in \mathbb{R}_{\pm \infty}$ (notation $\displaystyle y = \lim_{x\to d}f(x)$),
>if for any neighborhood $V$ of $y$ for some neighborhood $U$ of $d$ holds $f(U)\subseteq V$. 

---
# Function limit in reals at real points: from neighborhoods to $\varepsilon\&\delta$ and back:

> [!abstract] Function limit via neighborhoods
> A point $y$ of $\mathbb{R}_{\pm \infty}$ is a limit of a real function $f:D\to \mathbb{R}$ when $x$ tending to $d\in \mathbb{R}_{\pm \infty}$,
> if $D$ is a neighborhood of $d$ and for any neighborhood $V$ of $y$ for some neighborhood $U$ of $d$ holds $f(U)\subseteq V$.

>[!abstract] Function limit via $\varepsilon\&\delta$
>A point $y$ in $\mathbb{R}$ is a limit of a real function $f:D\to \mathbb{R}$ when $x$ tending to $d\in \mathbb{R}$, 
>if for any $\varepsilon>0$ for some $\delta>0$ for every $x$ in support of $f$ 
>	if $|x-d|\leq \delta$ then $|f(x)-y|\leq \varepsilon$. 

---
# Function limit in reals at infinities: from neighborhoods to $\varepsilon \& u$ and back:

- A point $y$ in $\mathbb{R}$ is a limit of a real function $f: D \to \mathbb{R}$ when $x$ tending to $\pm \infty$, if 
	- for any $\varepsilon >0$ 
		- for some $u>0$ 
			- for every $x$ in support of $f$ 
				- if $x \frac{\geq}{\leq}\pm u$ then 
				    - $|f(x)-y|\leq \varepsilon$.
- It means that if $f(x)$ approaches $y$ as $x \to+\infty$ or $x \to-\infty$, then for any arbitrary small $\varepsilon>0$ there exists a sufficiently large $u$ such that for all $x$ greater than $u$ (or less than   $-u$, if you're considering $-\infty$) holds the inequality $|f(x) - y|\leq \varepsilon$. 
---
- A point $y$ of $\mathbb{R}_{\pm \infty}$ is a limit of a real function $f:D \to \mathbb{R}$ when $x$ tending to $d \in \mathbb{R}_{\pm \infty}$,
	- if for any neighborhood $V$ of $y$ 
		- for some neighborhood $U$ of $d$ 
			- holds $f(U) \subseteq V$.
- $f(d) = y$  –  Notion.
---
# Function limits in infinities at infinities: from neighborhood to $\displaystyle v \& u$ and back:

Let $f: D \to \mathbb{R}$.
- $\displaystyle -\infty = \lim_{x\to \pm \infty}f(x),$
	- if for any $v \in \mathbb{R}$ 
		- for some $u>0$
			-  for every $x$ in support of $f$
				- if $x \frac{\geq}{\leq}\pm u$ then $f(x)\geq v$.
- $\displaystyle +\infty = \lim_{x\to \pm \infty}f(x)$,
	- if for any $v \in \mathbb{R}$
		- for some $u>0$ 
			- for every $x$ in support of $f$
				- if $x \frac{\geq}{\leq}\pm u$ then $f(x) \leq v$.
---
- $\pm \infty$ is a limit of a real function $f: D \to \mathbb{R}$ when $x$ tending to $d \in \mathbb{R}_{\pm \infty}$, 
	- if for any neighborhood $V$ of $\pm \infty$
		-  for some neighborhood $U$ of $d$
			- holds $f(U) \subseteq V$.
----
# Right-side limit in reals at real points: from neighborhood to $\varepsilon \& \delta$ and back:

- A point $y$ in $R$ is a right-side limit of a real function $f: D \to \mathbb{R}$ when $x$ tending (from right) to $d \in \mathbb{R}$ (notation $\displaystyle y = \lim_{x \to d+0}f(x)$) if:
	- for any $\varepsilon>0$
		- for some $\delta>0$
			- for every $x$ in support of $f$
				- if $d<x \leq d + \delta$
					- then $|f(x) - y| \leq \varepsilon$.
	- function $f$ with a restricted domain $D\ \cap \ ]d, +\infty[$ has $y$ as a limit when $x$ tending to $d$.
---
# Cardinal sine function $\text{sinc}(x)$:  

- Remark that function $\lambda x \in \mathbb{R}.$ $\left( \frac{\sin(x)}{x}\right)$ has a punctured point $x = 0$ where the function is not defined (out of its support) while the function is defined everywhere else.
<br>
- The cardinal sine function $\text{sinc}:\mathbb{R} \to \mathbb{R}$ at a real point $x \in \mathbb{R}$ is defined as 
  $$\text{sinc($x$)} = \begin{cases}1, \text{ if $x = 0$} \\
\frac{sin(x)}{x}, \text{ if $x \neq 0$}\end{cases}$$
----
# Cardinal sine at point of the origin


- **Statement (второй или первый замечательный предел)**:
  $$\lim_{x \to 0} \text{sinc}(x) = 1$$

- **Pseudo-proof**:
  - We can consider only "small" positive $x \in (0, \frac{\pi}{4}]$, because:
    - The limit definition is "downward closed" in the choice of $\delta$'s.
    - The sine function is odd.
    - $\text{sinc}(0) = 1$.
  - In other words, we can focus on proving:
    $$\lim_{x \to 0^+} \text{sinc}(x) = 1$$
  - Visual illustration:
    - Consider the diagram on the right:
      ![|300](Pasted%20image%2020241028233100.png)
      $$S_{\Delta OAB} < S_{\text{sector} \ OAB} < S_{\Delta OAC}$$
      where:
      $$\displaylines{
      S_{\Delta OAB} = OB \cdot OA \cdot \frac{1}{2} \sin(\angle AOB) = r^2 \cdot \frac{1}{2} \sin(x) = \frac{1}{2} \sin(x) \\
      S_{\text{sector }OAB} = \frac{x}{2\pi} \cdot \pi r^2 = x \cdot r^2 \cdot \frac{1}{2} = x \cdot \frac{1}{2} \\
      S_{\Delta OAC} = \frac{1}{2} OC \cdot \tan(x) \cdot OA = \frac{1}{2} \tan(x)
      }$$
      Hence, we get the inequality:
      $$\frac{1}{2} \sin(x) < \frac{1}{2} x < \frac{1}{2} \tan(x)$$

  - **Implication**:
    - From the inequality:
      $$1 < \frac{x}{\sin(x)} < \frac{1}{\cos(x)}$$
      This implies:
      $$\cos(x) < \text{sinc}(x) < 1$$

  - **Conclusion**:
    - Since:
      $$\lim_{x \to 0^+} \cos(x) = 1$$
      Using the [**squeezing lemma**](Theory%20of%20sequences%20and%20their%20limits..md#^a1615c), we conclude:
      $$\lim_{x \to 0^+} \text{sinc}(x) = 1$$
---
# Equivalence of Limits of Functions and Sequences: Detailed Proof

## Statement of the Equivalence
For any real function $f : D \to \mathbb{R}$, for any point $d \in \mathbb{R}_{\pm\infty}$, where the function $f$ is defined and behaves correctly in the neighborhood of $d$, the following two statements are equivalent:

1. $y = \displaystyle \lim_{x \to d} f(x)$
2. $y = \displaystyle \lim_{n \to \infty} f(d_n)$ for every sequence $(d_n)_{n \in \mathbb{N}}$ such that $d = \displaystyle \lim_{n \to \infty} d_n$.

## Proof: From Function Limit to Sequence Limit (a ⇒ b) for Real Values of $y$ and $d$
1. Let $(d_n)_{n \in \mathbb{N}}$ be a sequence such that $d = \displaystyle \lim_{n \to \infty} d_n$ and $\epsilon > 0$ is a positive value.
2. Since $y = \displaystyle \lim_{x \to d} f(x)$, there exists $\delta > 0$ such that for any $x \in D$, if $|x - d| \leq \delta$, then $|f(x) - y| \leq \epsilon$ [^1]. 
3. Since $d = \displaystyle \lim_{n \to \infty} d_n$, there exists $m \in \mathbb{N}$ such that for any $n \geq m$, $|d - d_n| \leq \delta$.
4. Hence, for all $n \geq m$, $|f(d_n) - y| \leq \epsilon$ [^2].

**Conclusion**: For $\epsilon > 0$, we find $m \in \mathbb{N}$ such that for all $n \geq m$, $|f(d_n) - y| \leq \epsilon$, thus proving $y = \displaystyle \lim_{n \to \infty} f(d_n)$.

## Proof: From Sequence Limit to Function Limit (b ⇒ a) for Real Values of $y$ and $d$
1. Assume $y = \displaystyle \lim_{n \to \infty} f(d_n)$ for every sequence $(d_n)_{n \in \mathbb{N}}$ with $d = \displaystyle \lim_{n \to \infty} d_n$, but suppose $y \neq \displaystyle \lim_{x \to d} f(x)$.
2. Since $y \neq \displaystyle \lim_{x \to d} f(x)$, there exists $\epsilon > 0$ such that for all $\delta > 0$, there exists $x$ such that $|x - d| \leq \delta$, but $|f(x) - y| > \epsilon$ [^3].
3. Let $d_n$ be a point in the support of $f$ such that $|d_n - d| \leq \frac{1}{n+1}$ and $|f(d_n) - y| > \epsilon$; then $d = \displaystyle \lim_{n \to \infty} d_n$, but $y \neq \displaystyle \lim_{n \to \infty} f(d_n)$, which contradicts our assumption.

**Conclusion**: The assumption $y \neq \displaystyle \lim_{x \to d} f(x)$ is incorrect, hence $y = \displaystyle \lim_{x \to d} f(x)$.

[^1]: Тут мы пытаемся сказать для любого $\varepsilon>0$ мы можем найти окрестность точки $d$, внутри которого будет выполняться условие предела ФУНКЦИИ
[^2]: $d_{n}$ начиная с некоторого $n \geq m$ будет вести себя почти также как $d$ 
[^3]: найдется такое расстояние между y и f(x) для некоторого икс в любой окрестности d