---
tags:
  - 2ndYear
---
![](Pasted%20image%2020250901163018.png)
$$P(A\mid B) = \frac{P(A \cap B)}{P(B)}$$ then
$$P(A_{1}\mid B) + P(A_{2}\mid B)+ \dots + P(A_{n}\mid B) = \frac{P(A_{1}\cap B) + P(A_{2}\cap B)+ \dots + P(A_{n}\cap B)}{P(B)}$$
and we know
$$\displaylines{B \subset A_{1}\cup A_{2} \cup \dots \cup A_{n} \Leftrightarrow (B \cap A_{1}) \cup (B \cap A_{2}) \dots \cup (B \cap A_{n}) = \\ P(A_{1}\cap B) + P(A_{2}\cap B)+ \dots + P(A_{n}\cap B)}$$
so
$$\frac{P(A_{1}\cap B) + P(A_{2}\cap B)+ \dots + P(A_{n}\cap B)}{P(B)} = \frac{B \subset A_{1}\cup A_{2} \cup \dots \cup A_{n}}{P(B)} = \frac{P(B)}{P(B)} = 1$$

![](Pasted%20image%2020250901170557.png)
$$\displaylines{\text{If } x_{1} = 1 \text{ then } P(x_{1} > x_{2}\cap x_{1}=1) = 0 \cdot \frac{1}{100} \\
\text{If } x_{1} = 2 \text{ then } P(x_{1} > x_2\cap x_{1}=2) = \frac{1}{99} \cdot \frac{1}{100} \\
\text{If } x_{1} = 3 \text{ then } P(x_{1} > x_2\cap x_{1}=3) = \frac{2}{99} \cdot \frac{1}{100}\\
\cdots \\
\text{If } x_{100} = 100 \text{ then } P(x_{1} > x_2\cap x_{1}=100) = \frac{99}{99} \cdot \frac{1}{100}}$$
So, 
$$P(x_{1} > x_2) = \frac{1}{99 \cdot 100} \cdot (1 + 2 + \dots + 99) = \frac{99 \cdot 100}{99 \cdot 100 \cdot 2} = \frac{1}{2}$$

![](Pasted%20image%2020250901173322.png)
$$\displaylines{
\text{If white ball has disappeared then $P = \frac{14}{39} \cdot \frac{26}{40}$} \\ \text{If black ball has disappeared then $P = \frac{13}{39} \cdot \frac{14}{40}$ } \\ \text{Total } P = \frac{14}{39} \cdot \frac{26}{40} + \frac{13}{39} \cdot \frac{14}{40} = \frac{14 \cdot 39}{39 \cdot 40} = \frac{7}{20} 
}$$
![](Pasted%20image%2020250901174004.png)
$$\displaylines{a)\  \text{All case}= 2^{6}= 64 \\
\text{Special case} = 4 \\ \text{So, } P = \frac{4}{64} = \frac{1}{16} \\ b) \ P = \frac{5}{128}}$$
![](Pasted%20image%2020250901174903.png)

![](Pasted%20image%2020250905195301.png)
![](Pasted%20image%2020250905200346.png)
$$P(A) = \sum^{6}_{i=0}\sum^{4}_{j=0}\left(\frac{C^{6-i}_{12}\cdot C^{i}_{8}}{C^{6}_{20}}\cdot \frac{C^{5-j}_{8}\cdot C^{j}_{4}}{C^{5}_{12}}\cdot \frac{15-i-j}{15} \cdot \frac{15-i-j-1}{14}\right)$$
