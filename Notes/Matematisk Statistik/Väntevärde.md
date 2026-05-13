
Definieras ibland:  
"Det värde man kan förvänta sig av slumpvariabeln".

Ingen bra definition.

Tänk slantsingling – vilket värde kan man förvänta sig av krona eller klave?

För kontinuerliga variabler har alla enskilda värden sannolikhet $0$.

> **Väntevärdet är tyngdpunkten för s.f./t.f.**

---

## Definition

Väntevärdet för variabeln $X$ är



$$\Large
\mu = E(X) = 
\begin{cases}
\sum_{k=0}^{\infty} k\,p_X(k) \quad \text{om det är en diskret funktion} \\
\int_{-\infty}^{\infty} x f_X(x) dx \quad \text{om det är en kontinuerlig funktion}
\end{cases}
$$

---

### Observation

$$\Large
E(X) =
\int_{-\infty}^{\infty} (1-F(x)) dx
$$

---

# Sammanfattning

| Fördelning      | $\Large S$               | $\Large p(k)/f(k)$                                            | $\Large E(X)$                        |
| --------------- | ------------------------ | ------------------------------------------------------------- | ------------------------------------ |
| Likformig       | $\Large \{1,2,\dots,n\}$ | $\Large \frac{1}{n}$                                          | $\Large\frac{n+1}{2}$                |
| Geometrisk      | $\Large\{0,1,2,\dots\}$  | $\Large(1-p)^k p$                                             | $\Large\frac{1-p}{p}$                |
| Binomial        | $\Large\{0,1,\dots,n\}$  | $\Large\binom{n}{k}p^k(1-p)^{n-k}$                            | $\Large np$                          |
| Poisson         | $\Large \{0,1,2,\dots\}$ | $\Large \frac{\mu^k}{k!}e^{-\mu}$                             | $\Large\mu$                          |
| Hypergeometrisk | $\Large\{0,1,\dots\}$    | $\Large\frac{\binom{K}{k}\binom{N-K}{n-k}}{\binom{N}{n}}$     | $\Large\frac{nK}{N}$                 |
| Likformig       | $\Large [a,b]$           | $\Large \frac{1}{b-a}$                                        | $\Large\frac{a+b}{2}$                |
| Exponential     | $\Large\mathbb{R}^+$     | $\Large\lambda e^{-\lambda x}$                                | $\Large\frac{1}{\lambda}$            |
| Normal          | $\Large\mathbb{R}$       | $\Large\frac{1}{\sigma\sqrt{2\pi}}e^{-(x-\mu)^2/(2\sigma^2)}$ | $\Large\mu$                          |
| Weibull         | $\Large\mathbb{R}^+$     | $\Large\lambda c(\lambda x)^{c-1}e^{-(\lambda x)^c}$          | $\Large\lambda\Gamma(1+\frac{1}{c})$ |

---
# Väntevärde satser och observationer

För funktion $\Large g$

Diskret:

$$\Large
E(g(X))=
\begin{cases}
\sum_{k=0}^{\infty} g(k)p_X(k) \quad \text{om det är diskret} \\
\int_{-\infty}^{\infty} g(x)f_X(x)dx \quad \text{om der är kontinuerlig}
\end{cases}
$$
---
### Linjäritet

$$\Large
E(aX+bY+c)=aE(X)+bE(Y)+c
$$

---

### Oberoende

Om

$$\Large
X_1,X_2,\dots,X_n
$$

är oberoende:

$$\Large
E(X_1X_2\dots X_n)=E(X_1)E(X_2)\dots E(X_n)
$$
---
# Länkar
[[Väntevärdesriktig]]
