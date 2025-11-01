---
tags:
  - 1stYear
---
**Parameter:** $M = 24 + 10 = 34$

# Examine and indicate whether the following functions have finite limits at points $\{0,-1,M,- \infty\}$, prove (using definition of the limit) your findings for one of the following $3$ items: 

## a) $\lambda x \in \mathbb{R}$. $Mx$ and $\lambda x \in \mathbb{R}$. $x^M$:

**Statement:** $\displaystyle \lim_{x \to 0}34x=0$ 
**Prove:** We need to show that for each $\varepsilon >0$ there exists $\delta>0$ such that:
1. $0<|x-0|< \delta \Rightarrow |34x-0|< \varepsilon$   
   $|34x|<\varepsilon$   
   $|x|<\frac{\varepsilon}{34}$
2. Take $\delta = \frac{\varepsilon}{34}$   
   $0<|x|<\frac{\varepsilon}{34} \Rightarrow |34x| < \varepsilon \Rightarrow |34x-0|<\varepsilon$
$\blacksquare$ 

**Statement:** $\displaystyle \lim_{x \to -1} 34x = -34$
**Prove:** We need to show that for each $\varepsilon >0$ there exists $\delta >0$ such that:
1. $0<|x-(-1)|<\delta \Rightarrow |34x - (-34) |< \varepsilon$
   $|x-(-1)| < \frac{\varepsilon}{34}$
2. Take $\delta = \frac{\varepsilon}{34}$
   $|x-(-1)|<\frac{\varepsilon}{34} \Rightarrow |34x - (-34)|<\varepsilon$
$\blacksquare$

**Statement:** $\displaystyle \lim_{x \to 34} 34x = 1156$
**Prove:** We need to show that for each $\varepsilon >0$ there exists $\delta >0$ such that:
1. $0<|x-34|<\delta \Rightarrow |34x - 1156 |< \varepsilon$
   $|x-34| < \frac{\varepsilon}{34}$
2. Take $\delta = \frac{\varepsilon}{34}$
   $|x-34|<\frac{\varepsilon}{34} \Rightarrow |34x - 1156|<\varepsilon$
$\blacksquare$

**Statement:** $\displaystyle \lim_{x \to - \infty}34x = -\infty$
**Prove:** We need to show that for each $V \in \mathbb{R}$ there exist $u>0$ such that:
1. $x < -u \Rightarrow 34x < V$
   $x < \frac{V}{34}$
2. $-u = V/34$
   $u = - \frac{V}{34}$
$\blacksquare$

# Find the following limits:

## a) $\lim_{x \to M} \frac{x^{2}-Mx+2}{x^{2}-M}$

In this case, there is no undefined value if we substitute $34$ for $x$, because no division by zero occurs.

$$34^2 - 34 = 1156 - 34 = 1122 \neq 0$$

Since the denominator is non-zero, we can directly substitute the value of $x$:

$$\lim_{x \to 34} \frac{x^{2}-34x+2}{x^{2}-34} = \frac{34^{2}- 34*34+2}{34^{2}-34} = \frac{2}{1122} = \frac{1}{561}$$

## b) $\lim_{x \to M} \frac{x^{2}-(M+1)x+M}{x^{2}-M^{2}}$

If we substitute $34$ for $x$, then the denominator becomes zero, which leads to an undefined expression. Therefore, we need to simplify the expression first to avoid division by zero.

$$\displaylines{\lim_{x \to M} \frac{x^{2}-(M+1)x+M}{x^{2}-M^{2}} = \lim_{x \to M}\frac{x^{2}-Mx - x + M}{x^{2}-M^{2}} = \\
\lim_{x \to M} \left( \frac{x(x-M)}{(x-M)(x+M)} - \frac{x-M}{(x-M)(x+M)} \right) = \\
\lim_{x \to M} \left( \frac{x-1}{x+M} \right)}$$

Now, we are able to substitute $x = 34$ into the simplified expression:

$$\lim_{x \to 34} \left(\frac{x-1}{x+34}\right) = \frac{33}{68}$$

## c) $\lim_{x \to \infty} \frac{x^{2}-Mx+2}{Mx^{2}-1}$

We can simplify this expression by dividing both the numerator and the denominator by $x^2$, which is the highest power of $x$ in both terms. This gives us:

$$\displaylines{\lim_{x \to \infty} \frac{x^{2}-Mx+2}{Mx^{2}-1} = \lim_{x \to \infty} \frac{\frac{x^{2}-Mx+2}{x^{2}}}{\frac{Mx^{2}-1}{x^{2}}} = \\
\lim_{x \to \infty} \frac{1- \frac{M}{x} + \frac{2}{x^{2}}}{M- \frac{1}{x^{2}}} = \frac{1}{M} = \frac{1}{34}}$$

As $x \to \infty$, the terms involving $\frac{1}{x}$ and $\frac{1}{x^2}$ approach zero. Therefore, the expression simplifies to:

$$\frac{1}{M} = \frac{1}{34}$$

## d) $\lim_{x \to 0} (1+Mx)^\frac{M}{x}$

We recognize a standard limit form in this expression. To simplify, we first rewrite the expression as:

$$\lim_{x \to 0} (1+Mx)^{\frac{M}{x}} = \lim_{x \to 0} \left( (1+Mx)^{\frac{1}{Mx}} \right)^{M^{2}}$$

The standard limit we can apply here is $\lim_{n \to 0} (1+n)^{\frac{1}{n}} = e$. Using this, we can conclude:

$$\lim_{x \to 0} \left( (1+Mx)^{\frac{1}{Mx}} \right)^{M^{2}} = e^{M^{2}} = e^{1156}$$

# Prove (using the definition of the derivative) that $(x^{M})' = Mx^{M-1}$ and $(\frac{1}{x^{M}})' = - \frac{M}{x^{M+1}}$

**Step 1: Definition of the derivative.**

The definition of the derivative of a function $f(x)$ at a point $x_0$ is:

$$
f'(x_0) = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0}
$$

We'll apply this definition to both cases.

### Part 1: Proof for $(x^M)'$

For the function $f(x) = x^M$, we substitute it into the definition of the derivative:

$$
f'(x_0) = \lim_{x \to x_0} \frac{x^M - x_0^M}{x - x_0}
$$

We can simplify the numerator using the difference of powers formula:

$$
x^M - x_0^M = (x - x_0) \left(x^{M-1} + x^{M-2} x_0 + \dots + x_0^{M-1}\right)
$$

Substitute this into the derivative expression:

$$
f'(x_0) = \lim_{x \to x_0} \frac{(x - x_0) \left(x^{M-1} + x^{M-2} x_0 + \dots + x_0^{M-1}\right)}{x - x_0}
$$

We can cancel out $(x - x_0)$ from the numerator and denominator:

$$
f'(x_0) = \lim_{x \to x_0} \left(x^{M-1} + x^{M-2} x_0 + \dots + x_0^{M-1}\right)
$$

Now, as $x \to x_0$, each term involving $x$ becomes $x_0$, so we get:

$$
f'(x_0) = M x_0^{M-1}
$$

Thus, we have shown that:

$$
(x^M)' = M x^{M-1}
$$

### Part 2: Proof for $(\frac{1}{x^M})'$

Now, for the function $f(x) = \frac{1}{x^M}$, we know that $\frac{1}{x^M}$ can be rewritten as $x^{-M}$. Therefore, the proof for this function follows exactly the same reasoning as for $x^M$, but with the exponent being negative.

Using the definition of the derivative:

$$
f'(x_0) = \lim_{x \to x_0} \frac{x^{-M} - x_0^{-M}}{x - x_0}
$$

We can apply the difference of powers formula again:

$$
x^{-M} - x_0^{-M} = (x - x_0) \left( x^{-M-1} + x^{-M-2} x_0 + \dots + x_0^{-M-1} \right)
$$

Substituting this into the derivative expression:

$$
f'(x_0) = \lim_{x \to x_0} \frac{(x - x_0) \left( x^{-M-1} + x^{-M-2} x_0 + \dots + x_0^{-M-1} \right)}{x - x_0}
$$

Canceling out $(x - x_0)$:

$$
f'(x_0) = \lim_{x \to x_0} \left( x^{-M-1} + x^{-M-2} x_0 + \dots + x_0^{-M-1} \right)
$$

Now, as $x \to x_0$, we get:

$$
f'(x_0) = -M x_0^{-M-1}
$$

Therefore:

$$
\left(\frac{1}{x^M}\right)' = -\frac{M}{x^{M+1}}
$$

# Analyze graph of a function $\lambda x \in \mathbb{R}$. $(M \sqrt{x} + \frac{1}{M}\sqrt[3]{x^{2}} - \frac{1}{\sqrt[M]{x}})$ and sketch it on $[-3, +3]$ (using pen and paper).

Subtitute $M = 34$:
$$34 \sqrt{x} + \frac{1}{34}\sqrt[3]{x^{2}} - \frac{1}{\sqrt[34]{x}}$$
## Define domain and support of the function:

Domain of the function:
$$\begin{cases}x \geq0,\ x \in [0, +\infty), \text{ for  } \sqrt{x},\ \sqrt[34]{x}\\
\sqrt[34]{x} \neq 0, x \in (0,+\infty), \text{ for } \frac{1}{\sqrt[34](x)}
\end{cases}\Rightarrow x \in (0, + \infty)$$
Support of the function:
$$supp(\lambda) = \{x>0\ | \ \lambda x \neq0\}$$
## Find limits at its boundaries and asymptotes:

**Limits at its boundaries:**

- $\lim_{x \to +0}\left(34 \sqrt{x} + \frac{1}{34}\sqrt[3]{x^{2}} - \frac{1}{\sqrt[34]{x}}\right) = -\infty$
- $\lim_{x \to +\infty}\left(34 \sqrt{x} + \frac{1}{34}\sqrt[3]{x^{2}} - \frac{1}{\sqrt[34]{x}}\right)= +\infty$

**Asymptotes:**

- Vertical asymptote: $x=0$ because it occurs dividing by zero
- Oblique asymptote: 
  $y=kx + b$, where $k = \lim_{x \to + \infty} \frac{f(x)}{x}$ and $b=\lim_{x \to + \infty}(f(x) - kx)$
  $$\displaylines{k = \lim_{x \to + \infty}\frac{34 \sqrt{x} + \frac{1}{34}\sqrt[3]{x^{2}} - \frac{1}{\sqrt[34]{x}}}{x}=\\ \lim_{x \to + \infty} \frac{34}{\sqrt{x}} + \frac{1}{34\sqrt[3]{x}} - \frac{1}{x\sqrt[34]{x}} =0}$$
$$\displaylines{b = \lim_{x \to + \infty}\left(34 \sqrt{x} + \frac{1}{34}\sqrt[3]{x^{2}} - \frac{1}{\sqrt[34]{x}} - 0x\right)= + \infty
}$$
## Study points of discontinuity, monotonicity and critical points:

**Find points of discontinuity:**

This function has no points of discontinuities because every term of function continues in domain of function.

**Study monotonicity:**

We should find derivative of function:

$$\displaylines{f'(x)=(34 \sqrt{x} + \frac{1}{34}\sqrt[3]{x^{2}} - \frac{1}{\sqrt[34]{x}})' = 34(x^{\frac{1}{2}})' + \frac{1}{34}(x^{\frac{2}{3}})'- (x^{- \frac{1}{34}})' =\\
\frac{17}{x^{\frac{1}{2}}} + \frac{1}{51 x^{\frac{1}{3}}} + \frac{1}{34x^{\frac{35}{34}}}
}$$
We can see $f'(x)$ is positive in domain because each term is positive
It means $f(x)$ increases

**Critical points:**

In point $x=0$, $f'(x)$ is undefined, because it is boundary of our function

**Define is function convex up or down:**

Find derivative of $f'(x)$:

$$\displaylines{f''(x) = 17(x^{- \frac{1}{2}})' + \frac{1}{51}(x^{- \frac{1}{3}})' + \frac{1}{34} (x^{- \frac{35}{34}})' =\\
- \frac{17}{2} x^{-\frac{3}{2}} - \frac{1}{153}x^{- \frac{4}{3}} - \frac{35}{1156}x^{- \frac{69}{34}}
}$$
$f''(x)$ is negative in domain, so function is convex up

## Sketch the function:

$f(1) = 34 + \frac{1}{34} - 1 = 33\frac{1}{34}$

![|400](Pasted%20image%2020241116134446.png)




