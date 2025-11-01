---
tags:
  - 1stYear
---
# Sequences and their limits:

- A (real) sequences is a total function $(x_{n})_{n\in N}:\ \mathbb{N}\rightarrow\mathbb{R}$ usually presented as $x_{0}, x_{1},x_{2},...$
- A real number $x\in \mathbb{R}$ is said to be a limit of a sequences $(x_{n})_{n\in N}$, (notation $\displaystyle x=\lim_{x\to\infty} x_{n}$) if
	- for each (any) real $\varepsilon>0$ 
		- for some (i.e., there exists) $m\in \mathbb{N}$ such that 
			- for all $n\geq m$ holds $|x_{m}-x_{n}|\leq \varepsilon$.

> [!hint] Examples and exercises
> - Examples:
> 	- Sequence $\displaystyle (1- \frac{1}{n+1})_{n\in \mathbb{N}}$ has a limit $1$.
> 	- Sequence $\displaystyle ((-1)^{n} - \frac{1}{n+1})_{n\in\mathbb{N}}$ has no any limit.

- A sequence converges to a real number $x\in \mathbb{R}$, if the sequences has $x$ as a limit.
- A sequences converges (or has a limit), if it has a limit (i.e, there exists $x$ such that ..).
- A sequences $(x_{n})_{x\in \mathbb{N}}$ is bounded, if for some interval $[a,b]\subseteq\mathbb{R}$ and each (all) $n \in \mathbb{N}$ holds $x_{n}\in [a,b]$. 

>[!hint] Examples and exercises
>- Sequences $\displaystyle (1- \frac{1}{n+1})_{n\in\mathbb{N}}$ and $\displaystyle ((-1)^{n} - \frac{1}{n+1})$ are bounded.

# Subsequences:

- A sequence $(y_{n})_{n\in \mathbb{N}}$ is said to be a subsequence of a sequence $(x_{n})_{x\in \mathbb{N}}$, if there exists a strictly monotone (strictly increasing / growing) total ("sub-indexing") function $m: \mathbb{N}\to\mathbb{N}$ such that for all $n\in\mathbb{N}$ holds $y_{n}=x_{m(n)}$.
<br>
- Example: Sequence $0,2,4,...$ of even numbers is a subsequence of all natural numbers $0,1,2,...$ but not vice-versa, a sub-indexing function is $m=\lambda m \in \mathbb{N}.(2n)$.
<br>
- Subsequence of a converging sequence does converge to the same limit as the sequence itself.

# Main properties: convergence and boundness:

- Each converging sequence has unique limit and is bounded.
   
  >[!check]- Proof for unique limit
  >- Let $y$ and $z$ be limits(s) of a sequence $(x_{n})_n\in\mathbb{N}$.
  >- Let $\varepsilon>0$ be any positive real number and $m_{y}\in \mathbb{N}$ and $m_{z}\in \mathbb{N}$ be numbers such that
  >	- $|x_{n}-y|\leq \varepsilon$ for all $n\geq m_{y}$,
  >	- $|x_{n}-z|\leq \varepsilon$ for all $n\geq m_{z}$,
  >	  and let $m=max\{m_{y},m_{z}\}$.   [^1].
  >- Then $$\displaylines{|y-z|=|(y-x_{m})+(x_{m}-z)|\leq\\ |y-x_{m}|+|x_{m}-z|\leq 2\varepsilon}.$$![Trianle inequality|200](The%20Dot%20product%20and%20its%20properties..md#^73428c)
  >- Hence $y=z$ because the distance between $y$ and $z$ is less than any positive number.
  >$\blacksquare$
 
  >[!check]- Proof for bounded
  >- Let $(x_{n})_n\in\mathbb{N}$ be a sequence and $x$ be its limit.
  >- Let $m\in\mathbb{N}$ be a number such that for all $n\geq m$ holds $|x_{n}-x|\leq 1$.
  >- Let $c=max\{|x_{0}|,...|x_{m}|, |x-1|,|x+1|\}$.     [^2].
  >- Then for all $n\in\mathbb{N}$ holds $-c\leq x_{n}\leq +c,$ i.e., 
  >  $(x_{n})_n\in\mathbb{N}$ is bounded.
  >$\blacksquare$
  
- (Bolzano – Weierstrass theorem) Each bounded sequence has a converging subsequence (but not vice versa)
  
  > [!check]- Proof
  > - Let $[a_{0},b_{0}] :=$ an interval containing all terms in $(x_{n})_{n\in\mathbb{N}}$, $m:= 0$ and $y_{m}:=$the first term from $(x_{n})_{n\in\mathbb{N}}$ in $[a_{0},b_{0}]$;
  >   <br>
  > - Loop:
  >   Let $[a_{m+1}, b_{m+1}]:=$ a half of the interval $[a_{m},b_{m}]$ that $(x_{n})_{n\in\mathbb{N}}$ hits infinitely often,
  >   $y_{m+1}:=$ the first after $y_{m}$ term from $(x_{n})_{n\in\mathbb{N}}$ in $[a_{m+1},b_{m+1}]$, and $m:=m+1$
  >   <br>
  >- Loop invariant (inductive statement):
  >	- $(x_{n})_{n\in\mathbb{N}}$ hits $[a_{m},b_{m}]$ infinitely often,
  >	- $y_{0}...y_{m}$ is subsequence of a prefix of $(x_{n})_{n\in\mathbb{N}}$,
  >	- and $|a_{m},b_{m}|= \frac{|a_{0},b_{0}|}{2^{m}}$.
  ><br>
  >- Let $\{y\} := {\bigcap}_{m\in\mathbb{N}} [a_{m},b_{m}]$ [^3]
  >- Let $\varepsilon>0$ be any positive real and $m\in\mathbb{N}$ be the first natural number such that $|a_{m},b_{m}|\leq \varepsilon$'
  >- By construction, for all $n\geq m$ holds $y_{n}\in [a_{m},b_{m}]$ and hence $|y_{n}-y|\leq \varepsilon$.
  >- It proves that $y = \displaystyle{\lim_{n\to\infty}} y_{n}.$
  >$\blacksquare$

- For any converging sequences $(x_{n})_{n\in\mathbb{N}}$ and $(y_{n})_{n\in\mathbb{N}}$ if $x=\displaystyle{\lim_{n\to\infty} x_{n}}$ and $y=\displaystyle{\lim_{n\to\infty} y_{n}}$ then:
	1. sequences $(x_{n}+y_{n})_{n\in\mathbb{N}},\ (x_{n}- y_{n})_{n\in\mathbb{N}},$ and $(x_{n}\times y_{n})_{n\in\mathbb{N}}$ are converging and $\displaystyle{\lim_{n\to\infty}(x_{n}+y_{n})=(x+y),\ \lim_{n\to\infty}=(x-y)}$, and $\displaystyle{\lim_{n\to\infty} x_{n}\times y_{n}=(x\times y)}$.   
	   >[!check]+ Proof
	   >- Let $\varepsilon > 0$ be any positive real;
	   >	- since $\displaystyle x=\lim_{n\to\infty}x_{n}$, there exists some $m_{x}\in \mathbb{N}$ such that for all $n\geq m$ holds $|x_{n}-x|\leq \varepsilon$
	   >	- since $\displaystyle y=\lim_{n\to\infty}y_{n}$, there exists some $m_{y}\in \mathbb{N}$ such that for all $n\geq m$ holds $|y_{n}-y|\leq \varepsilon$
	   >![](The%20Dot%20product%20and%20its%20properties..md#^73428c)
	   >- - - 
	   >- $$\displaylines{\displaystyle |(x_{n}+y_{n})-(x+y) | = \\|(x_{n}-x)+(y_{n}-y) |\leq \\ |x_{n}-x|+|y_{n}+y| \leq \\ \varepsilon + \varepsilon \leq 2\varepsilon}$$
	   >- Hence, sequence $(x_{n}+y_{n})_{n\in \mathbb{N}}$ converges to $(x+y)$ 
	   >- - -
	   >- $$\displaylines{\displaystyle 
	   >  |(x_{n}-y_{n}) - (x-y)| = |(x_{n}-x)-(y_{n}-y)| = \\ |(x_{n}-x)+(y-y_{n})| \leq \\ |x_{n}-x|+|y-y_{n}| \leq |x_{n}-x| + |y_{n}-y| \leq 2\varepsilon
	   >  }$$
	   >- Hence, sequence $(x_{n}-y_{n})_{n\in \mathbb{N}}$ converges to $(x-y)$ 
	   >- - -
	   >- $$\displaylines{\displaystyle 
	   >  |x_{n}\times y_{n} - x\times y|  = \\ |x_{n}\times y_{n}-x\times y_{n}+x\times y_{n} - x\times y| \leq \\ |x_{n}\times y_{n} - x\times y_{n}| + |x\times y_{n}-x\times y| \leq \\ |y_{n}\varepsilon|+|x \varepsilon|
	   >  }$$
	   >- Hence, sequence $(x_{n}\times y_{n})_{n\in \mathbb{N}}$ converges to $(x\times y)$
	   
	   
	  <br>
	
	2. If for all $n\in\mathbb{N}$ holds $y_{n}\neq 0$, and $y\neq 0$, then sequence $\displaystyle(\frac{x_{n}}{y_{n}})_{n\in\mathbb{N}}$ is converging and $\displaystyle{\lim_{n\to\infty}(\frac{x_{n}}{y_{n}})=\frac{x}{y}}$.
	   > [!check]+ Proof
	   > - Let us assume that $x\neq 0$.
	   > - Since $y = \displaystyle \lim_{n\to\infty} y_{n}\neq 0$, there exists some $\Delta >0$ such that for some $m_{\Delta}\in \mathbb{N}$ and all $n>m_{\Delta}$ holds $|y_{n}|\geq \Delta$.
	   > - Let $\varepsilon > 0$ be any positive real;
	   > 	- since $\displaystyle x = \lim_{n\to \infty} x_{n}$, there exists some $m_{x}\in \mathbb{N}$ such that for all $n\geq m_{x}$ holds $|x_{n}-x| \leq \frac{\varepsilon\Delta}{2}$;
	   > 	- since $y=\displaystyle \lim_{n\to\infty}y_{n}\neq 0$, there exists some $m_{y}\in \mathbb{N}$ such that for all $n\geq m_{y}$ holds $|y_{n}-y|\leq \frac{\varepsilon|y|\Delta}{2|x|}$;
	   > <br>
	   > 
	   > - Let $m:=max\{m_{\Delta}, m_{x}, m_{y}\}$ and $n\geq m$ be any natural number;
	   > - $$\displaylines{ \displaystyle |\frac{x_{n}}{y_{n}} - \frac{x}{y}| = | \frac{x_{n}y-xy_{n}}{yy_{n}}|= \\  | \frac{(x_{n}-x)y+x(y-y_{n})}{yy_{n}}|\leq \\ | \frac{x_{n}-x}{y_{n}}| + | \frac{x}{y}|\times | \frac{y-y_{n}}{y_{n}}|\leq\\ \frac{|x_n-x|}{\Delta} + | \frac{x}{y}| \times \frac{|y-y_{n}|}{\Delta}\\
	   >   \leq \frac{\varepsilon\Delta}{2\Delta}+| \frac{x}{y}| \times \frac{\varepsilon|y|\Delta}{2|x|\Delta} \\ = \frac{\varepsilon}{2} + \frac{\varepsilon}{2} = \varepsilon .}\\$$
	   >   ![](The%20Dot%20product%20and%20its%20properties..md#^73428c)
	   > -  It proves that $\displaystyle \lim_{n\to\infty}\left( \frac{x_{n}}{y_{n}}\right)= \frac{x}{y}$.
	   >   $\blacksquare$
	   

---
# Some Theory: 
- Any bounded *monotone* (i.e., non-decreasing) sequence converges to its supremum (i.e., the least upper bound).
- Any bounded *antimonotone* (i.e., non-increasing) sequence converges to its infimum (i.e, the greatest lower bound)
- For any real converging sequences $(x_{n})_{n\in \mathbb{N}}$ and $(y_{n})_{n\in \mathbb{N}}$, if for all $n\in \mathbb{N}$ holds $x_{n}\leq y_{n}$, then $\displaystyle \lim_{n\to \infty}x_{n}\leq \lim_{n\to \infty}y_{n}$

>[!abstract] Squeezing Lemma (Лемма о двух милиционерах)
>- Statement: For any real sequences $(x_{n})_{n\in \mathbb{N}},(y_{n})_{n\in \mathbb{N}},$ and $(z_{n})_{n\in \mathbb{N}},$
>	- if $(x_{n})_{n\in \mathbb{N}},$ and $(z_{n})_{n\in \mathbb{N}}$ converge and have joint limit 
>	- and for all $n\in \mathbb{N}$ holds $x_{n}\leq y_{n} \leq z_{n}$
>- then $(y_{n})_{n\in \mathbb{N}}$ converges to the same limit as both $(x_{n})_{n\in \mathbb{N}},$ and $(z_{n})_{n\in \mathbb{N}}$.

^a1615c

---
# Real number $e$:
- $\displaystyle e = ((1+ \frac{1}{n+1})^{n+1})_{n\in\mathbb{N}}$
---
# Cauchy sequences convergence test:

- A real sequence $(x_{n})_{n\in \mathbb{N}}$ meets Cauchy sequence convergence test if for any real $\varepsilon > 0$ for some (i.e., there exists) $m\in \mathbb{N}$ such that for all $n_{1},n_{2}\geq m$ holds $|x_{n_{1}}-x_{n_{2}} |\leq \varepsilon$ 
- A real sequence meets Cauchy sequence convergence test iff it does converge.
---
# Neighborhoods of real points (окрестность точки):

- A neighborhood for/of a real "point" $x\in\mathbb{R}$ is any set $V\subseteq \mathbb{R}$ such that for some real $v>0$ holds $]x-v,x+v[ \ \subseteq V$.
- Examples:
	- $\mathbb{R}$ is a neighborhood for any real point, but any finite set of reals (including $\varnothing$) is not a neighborhood for any real point.
	- For any reals $x$ and $v>0$
		- an open inverval $]x-v,x+v[$ is a neighborhood for all its points,
		- a close interval $[x-v,x+v]$ is a neighborhood of all its points but its end points $(x-v)$ and $(x+v)$.
---
# Infinities:

- Let us "expand" the set of reals $\mathbb{R}$ by two artificial elements $-\infty$ and $+\infty$ with the following axiomatization: for all $x\in \mathbb{R}$ hold:
	- $-\infty <x < +\infty$
	- $(\pm\infty) + x = x + (\pm \infty) = \pm \infty$
	- If $x>0$, then $(\pm\infty)\cdot x = x\cdot (\pm \infty) = \pm \infty$
	- If $x<0$, then $(\pm \infty)\cdot x = x \cdot (\pm \infty) = \mp \infty$
	- $\frac{x}{\pm\infty} = 0$
- Let us use $\mathbb{R}_{-\infty} = \mathbb{R} \cup \{-\infty\}, \mathbb{R}_{+\infty}= R\cup \{+\infty\},$ and $\mathbb{R}_{\infty} = \mathbb{R}_{\pm\infty} = \mathbb{R} \cup \{-\infty, +\infty\}$ to denote reals extended by infinities.

**How to depict extended reals:**
![](Pasted%20image%2020240930111530.png)

- In the left diagram, the inftinies are the endpoints of the number line. 
- In the right diagram, the infinities are the special points that are greater than or less than any point of the number line.  

---
# Infinities and their neighborhoods:

- A neighborhood $V\subseteq \mathbb{R}$ for/of an "infinity point" $\pm\infty$ is defined as follows:
	- $V\subseteq \mathbb{R}$ is a neighborhood of $+\infty$, if for some $v\in \mathbb{R}$ holds $]v,+\infty[\ \subseteq V$;
	- $V\subseteq \mathbb{R}$ is a neighborhood of $-\infty$, if for some $v\in \mathbb{R}$ holds $]-\infty,v[\ \subseteq V$;
- Examples: For any real $x$:
	- $]x,+\infty[$ is a neighborhood for all 
	  its real points and for $+\infty$,
	- $]-\infty, x[$ is a neighborhood for $-\infty$, and for all its points but the end point $x$.
- - -
# Infinities as limits of real sequences:
- Let $(x_{n})_{n\in\mathbb{N}}:\mathbb{N}\to \mathbb{R}$ be real sequence:
	- $+\infty$ is said to be a limit of $(x_{n})_{n\in\mathbb{N}}$, 
	  (notation $\displaystyle \lim_{n\to \infty}x_{n}=+\infty$), if for any $v\in \mathbb{R}$ there exists $m\in \mathbb{N}$ that for all $n\geq m$ holds $x_{n}>v$.
	- $-\infty$ is said to be a limit of $(x_{n})_{n\in\mathbb{N}}$, 
	  (notation $\displaystyle \lim_{n\to \infty} x_{n}= -\infty$), if for any $v\in \mathbb{R}$ there exists $m\in \mathbb{N}$ that for all $n\geq m$ holds $x_{n}<v$.
---
# Sequence limit in reals: from $\varepsilon \& m$ to neighborhoods and back:

>[!abstract] The sequence limit via $\varepsilon\&m$:
>A real number $x\in \mathbb{R}$ is a limit of a real sequence $(x_{n})_{n\in \mathbb{N}}$ 
>If for any $\varepsilon > 0$ for some $m\in \mathbb{N}$ such that for all $n\geq m$ holds $|x-x_{n}|\leq \varepsilon$.

>[!abstract] The sequence limit via neighborhoods
>A real number $x\in \mathbb{R}$ is a limit of a real sequence $(x_{n})_{n\in\mathbb{N}}$
>If for any neighborhood $V$ of $x$ for some neighborhood $U$ of $+\infty$ $(x_n)_{n\in \mathbb{N}}(U) \subseteq V$[^4].

---

# Sequence limit in infinities: from $V\&m$ to neighborhoods:

> [!abstract] The sequence limit at infinities via $V\&m$
> - $\pm \infty$ is a limit of real sequence $(x_{n})_{n\in \mathbb{N}}$
> if for any $v\in \mathbb{R}$ there exists $m\in \mathbb{N}$ that for all $n \geq m$ holds $x\ \frac{>}{<}\ v$ respectively. 

>[!abstract] The sequence limit at infinity via neighborhoods
>- $\pm \infty$ is a limit of a real sequence $(x_{n})_{n\in \mathbb{N}}$ 
>if for any neighborhood $V$ of $\pm \infty$ for some neighborhood $U$ of $+\infty$ holds $(x_n)_{n\in \mathbb{N}}(U)\subseteq V$[^4].

# Sequences and their limits in $\mathbb{R}_{\pm \infty}$:

- A point $x$ of the extended set $\mathbb{R}_{\pm \infty}$ is a limit of real sequence $(x_{n})_{n\in \mathbb{N}}$,
  if for any neighborhood $V$ of $x$ for some neighborhood $U$ of $+\infty$ holds $(x_{n})_{n\in \mathbb{N}}(U)\subseteq V$[^4].

[^1]: m is a number at which both of the above equalities work. The equalities will work if we take their intersection, in this case it is the maximum of these values
[^2]: c is a value that is larger or equal to the max element of sequence.  
[^3]: The intersection of all subintervals of $[a_{0},b_{0}]$ 
[^4]:The $(x_n)_{n\in \mathbb{N}}(U)$ means the terms $x_{n}$, where $n$ is taken from the set $U$.