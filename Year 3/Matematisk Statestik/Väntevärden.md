# Matematisk statistik
Eric Järpe

## F 5: Väntevärden

Eric Järpe  
ITE  
Högskolan i Halmstad  
28 september 2025

---

# Väntevärden

Definieras ibland:  
"Det värde man kan förvänta sig av slumpvariabeln".

Ingen bra definition.

Tänk slantsingling – vilket värde kan man förvänta sig av krona eller klave?

För kontinuerliga variabler har alla enskilda värden sannolikhet $0$.

---

Istället:

**Väntevärdet är tyngdpunkten för s.f./t.f.**

---

## Definition

Väntevärdet för variabeln $X$ är

$$
\mu = E(X)
$$

Diskret:

$$
E(X) =
\sum_{k=0}^{\infty} k\,p_X(k)
$$

Kontinuerlig:

$$
E(X) =
\int_{-\infty}^{\infty} x f_X(x) dx
$$

---

### Observation

$$
E(X) =
\int_{-\infty}^{\infty} (1-F(x)) dx
$$

---

# Sammanfattning

| Fördelning      | $S$               | $p(k)/f(k)$                                             | $E(X)$                         |
| --------------- | ----------------- | ------------------------------------------------------- | ------------------------------ |
| Likformig       | $\{1,2,\dots,n\}$ | $\frac{1}{n}$                                           | $\frac{n+1}{2}$                |
| Geometrisk      | $\{0,1,2,\dots\}$ | $(1-p)^k p$                                             | $\frac{1-p}{p}$                |
| Binomial        | $\{0,1,\dots,n\}$ | $\binom{n}{k}p^k(1-p)^{n-k}$                            | $np$                           |
| Poisson         | $\{0,1,2,\dots\}$ | $\frac{\mu^k}{k!}e^{-\mu}$                              | $\mu$                          |
| Hypergeometrisk | $\{0,1,\dots\}$   | $\frac{\binom{K}{k}\binom{N-K}{n-k}}{\binom{N}{n}}$     | $\frac{nK}{N}$                 |
| Likformig       | $[a,b]$           | $\frac{1}{b-a}$                                         | $\frac{a+b}{2}$                |
| Exponential     | $\mathbb{R}^+$    | $\lambda e^{-\lambda x}$                                | $\frac{1}{\lambda}$            |
| Normal          | $\mathbb{R}$      | $\frac{1}{\sigma\sqrt{2\pi}}e^{-(x-\mu)^2/(2\sigma^2)}$ | $\mu$                          |
| Weibull         | $\mathbb{R}^+$    | $\lambda c(\lambda x)^{c-1}e^{-(\lambda x)^c}$          | $\lambda\Gamma(1+\frac{1}{c})$ |

---

# Exempel

Antag att $X$ har

### a)

Täthetsfunktion

$$
f(x) =
\frac{\theta(\theta+1)}{(\theta+x)^2}
$$

med

$$
S=(0,1), \quad \theta>0
$$

---

### Väntevärde

$$
E(X)=\int_0^1 x\frac{\theta(\theta+1)}{(\theta+x)^2}dx
$$

Substitution

$$
u=\theta+x
$$

ger

$$
E(X)=\theta(\theta+1)\ln\frac{\theta+1}{\theta}-\theta
$$

---

### b)

Fördelningsfunktion

$$
F(x)=
\frac12\left(1+\sin\left(\frac{\pi x}{2(\theta+|x|)}\right)\right)
$$

med

$$
S=\mathbb{R}
$$

---

Symmetri:

$$
F(-x)=1-F(x)
$$

⇒ tätheten är symmetrisk.

Alltså

$$
E(X)=0
$$

---

# Sats

För funktion $g$

Diskret:

$$
E(g(X))=
\sum_{k=0}^{\infty} g(k)p_X(k)
$$

Kontinuerlig:

$$
E(g(X))=
\int_{-\infty}^{\infty} g(x)f_X(x)dx
$$

---

### Linjäritet

$$
E(aX+bY+c)=aE(X)+bE(Y)+c
$$

---

### Oberoende

Om

$$
X_1,X_2,\dots,X_n
$$

är oberoende:

$$
E(X_1X_2\dots X_n)=E(X_1)E(X_2)\dots E(X_n)
$$

---

# Exempel

Produkter med längd

$$
X
$$

inom toleranser

$$
(a-1,a+1)
$$

Täthet

$$
f_X(x)=e^{-2|x-a|}
$$

---

## a) Väntevärde

$$
E(X)=\int_{-\infty}^{\infty} xe^{-2|x-a|}dx
$$

Substitution

$$
u=x-a
$$

ger

$$
E(X)=a
$$

---

## b) Förväntad vinst

Vinstfunktion

$$
V(x)=
\begin{cases}
-400 & x<a-1 \\
100 & a-1\le x\le a+1 \\
0 & x>a+1
\end{cases}
$$

---

$$
E(V)=\int_S V(x)f(x)dx
$$

Resultat

$$
E(V)=100-300e^{-2}
$$

---

# Lägesmått

### Väntevärde

$$
\mu=E(X)
$$

Tyngdpunkten.

---

### Median

$$
\int_{-\infty}^{m}f(x)dx=
\int_{m}^{\infty}f(x)dx
$$

---

### Typvärde

$$
t=\arg\max_k p_X(k)
$$

---

### Geometriskt centralmått

Diskret:

$$
g=\prod_{k=0}^{\infty}k^{p_X(k)}
$$

Kontinuerlig:

$$
g=e^{\int_{-\infty}^{\infty}(\ln x)f(x)dx}
$$

---

# Exempel

Täthet

$$
f(x)=\frac{\theta(\theta+1)}{(\theta+x)^2}
$$

---

Median definieras av

$$
0.5=\int_0^m f(x)dx
$$

---

Resultat

$$
m=\frac{\theta}{2\theta+1}
$$

---

# Spridningsmått

Två variabler kan ha samma väntevärde men olika osäkerhet.

---

## Varians

$$
\sigma^2=V(X)=E((X-\mu)^2)
$$

---

### Beräkningsformel

$$
V(X)=E(X^2)-\mu^2
$$

Diskret:

$$
\sum k^2p(k)-\left(\sum kp(k)\right)^2
$$

Kontinuerlig:

$$
\int x^2f(x)dx-\left(\int xf(x)dx\right)^2
$$

---

# Standardavvikelse

$$
\sigma=D(X)=\sqrt{V(X)}
$$

---

# Variationskoefficient

$$
R(X)=\frac{D(X)}{E(X)}
$$

---

### Observation

Om

$$
S=[a,b]
$$

så approximeras

$$
\sigma\approx\frac{1}{4}(b-a)
$$

---

# Linjära transformationer

$$
E(aX+b)=a\mu+b
$$

$$
V(aX+b)=a^2\sigma^2
$$

$$
D(aX+b)=|a|D(X)
$$

---

# Standardisering

Om

$$
E(X)=\mu,\quad V(X)=\sigma^2
$$

så är

$$
Y=\frac{X-\mu}{\sigma}
$$

standardiseringen.

---

# Skevhet

$$
\gamma=
E\left(\frac{X-\mu}{\sigma}\right)^3
$$

---

# Kurtosis

$$
\kappa=
E\left(\frac{X-\mu}{\sigma}\right)^4
$$

---

# Kovarians

$$
C(X,Y)=E((X-\mu_X)(Y-\mu_Y))
$$

Diskret:

$$
\sum\sum(i-\mu_X)(j-\mu_Y)p_{X,Y}(i,j)
$$

Kontinuerlig:

$$
\int\int(x-\mu_X)(y-\mu_Y)f_{X,Y}(x,y)dxdy
$$

---

### Alternativ form

$$
C(X,Y)=E(XY)-E(X)E(Y)
$$

---

# Korrelation

$$
\rho(X,Y)=\frac{C(X,Y)}{D(X)D(Y)}
$$

---

### Tolkning

- $\rho\approx1$ eller $-1$ ⇒ starkt beroende
- $\rho\approx0$ ⇒ svagt linjärt beroende

---

# Sats

Om

$$
X\perp Y
$$

så

$$
C(X,Y)=0
$$

---

# Summor av variabler

$$
E(X+Y)=E(X)+E(Y)
$$

---

$$
V(X+Y)=V(X)+V(Y)+2C(X,Y)
$$

---

Om

$$
X\perp Y
$$

$$
V(X+Y)=V(X)+V(Y)
$$

---

$$
D(X+Y)=\sqrt{D(X)^2+D(Y)^2}
$$

---

# Exempel

Täthet

$$
f_{X,Y}(x,y)=\frac{xy+c}{c+1}e^{-x-y}
$$

med

$$
(x,y)\in(\mathbb{R}^+)^2
$$

---

### Resultat

$$
E(X)=\frac{c+2}{c+1}
$$

$$
E(X^2)=\frac{2c+6}{c+1}
$$

$$
V(X)=\frac{c^2+4c+2}{(c+1)^2}
$$

---

$$
E(XY)=\frac{c+4}{c+1}
$$

---

$$
C(X,Y)=\frac{c}{(c+1)^2}
$$

---

$$
\rho(X,Y)=\frac{c}{c^2+4c+2}
$$

---

### Observation

$$
c=0 \Rightarrow \rho=0
$$

$$
\lim_{c\to\infty}\rho=0
$$

Maximalt värde fås för

$$
c=\sqrt{2}
$$
