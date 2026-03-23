# Matematisk statistik
Eric Järpe

## F 6: Normalfördelning

Eric Järpe  
ITE  
Högskolan i Halmstad  
11 oktober 2025

---

# Normalfördelning

- Vanlig fördelning för att beskriva naturliga fenomen
- Viktig fördelning inom statistikteorin då skattningar och test bygger på den via asymptotiska resultat

Täthetsfunktion

$$
f(x)=\frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$

---

Fördelningsfunktion

$$
F(x)=
\frac{1}{\sqrt{2\pi}\sigma}
\int_{-\infty}^{x} e^{-\frac{(t-\mu)^2}{2\sigma^2}} dt
$$

Kan inte uttryckas explicit ⇒ används **tabeller**.

---

$$
X \in N(\mu,\sigma)
$$

med

$$
S=\mathbb{R}
$$

---

# Standard normalfördelning

$$
X \in N(0,1)
$$

Täthetsfunktion

$$
\phi(x)=\frac{1}{\sqrt{2\pi}}e^{-x^2/2}
$$

---

Fördelningsfunktion

$$
\Phi(x)=
\frac{1}{\sqrt{2\pi}}
\int_{-\infty}^{x} e^{-t^2/2} dt
$$

---

Värden finns i tabeller.

---

### Egenskaper

$$
E(X)=0
$$

$$
V(X)=1
$$

---

### Symmetri

$$
\phi(-x)=\phi(x)
$$

$$
\Phi(-x)=1-\Phi(x)
$$

---

### Intervall

$$
P(a\le X\le b)=\Phi(b)-\Phi(a)
$$

---

### Percentil

$$
\lambda_\alpha : P(X>\lambda_\alpha)=\alpha
$$

---

# Exempel

Antag

$$
X\in N(0,1)
$$

---

### a)

$$
P(X\le -0.73)
$$

---

Lösning

$$
P(X\le -0.73)=\Phi(-0.73)
$$

$$
=1-\Phi(0.73)
$$

$$
=1-0.7673
$$

$$
=0.2327
$$

---

### b)

$$
P(3|X|+X\ge5)
$$

---

Resultat

$$
2-\Phi(1.25)-\Phi(2.5)
$$

$$
=0.1118
$$

---

# Allmän normalfördelning

## Sats

$$
X\in N(\mu,\sigma)
\quad \Leftrightarrow \quad
\frac{X-\mu}{\sigma}\in N(0,1)
$$

---

Täthet

$$
f(x)=\frac{1}{\sigma}\phi\left(\frac{x-\mu}{\sigma}\right)
$$

---

Fördelningsfunktion

$$
F(x)=\Phi\left(\frac{x-\mu}{\sigma}\right)
$$

---

### Moment

$$
E(X)=\mu
$$

$$
V(X)=\sigma^2
$$

$$
D(X)=\sigma
$$

---

### Intervall

$$
P(a\le X\le b)
=
\Phi\left(\frac{b-\mu}{\sigma}\right)
-
\Phi\left(\frac{a-\mu}{\sigma}\right)
$$

---

### Viktigt specialfall

$$
P(|X-\mu|\le k\sigma)=2\Phi(k)-1
$$

---

Approximationer

$$
P(|X-\mu|\le\sigma)\approx0.68
$$

$$
P(|X-\mu|\le2\sigma)\approx0.95
$$

$$
P(|X-\mu|\le3\sigma)\approx0.997
$$

---

## FIGUR ATT INFÖRA

Under **68–95–99.7-regeln**

Infoga normalfördelningsfigur som visar intervallen

- $\mu \pm \sigma$
- $\mu \pm 2\sigma$
- $\mu \pm 3\sigma$

---

# Exempel

Antag

$$
X\in N(\mu,\sigma)
$$

---

### a)

$$
P(102\le X\le201)
$$

med

$$
\mu=101,\quad\sigma=202
$$

---

$$
P(102\le X\le201)
=
\Phi\left(\frac{201-101}{202}\right)
-
\Phi\left(\frac{102-101}{202}\right)
$$

---

$$
=
\Phi(0.5)-\Phi(0)
$$

---

$$
=0.6915-0.5
$$

---

$$
=0.1915
$$

---

### b)

Bestäm $\sigma$ om

$$
P(X^2-X\le2)=0.5
$$

och

$$
\mu=0.5
$$

---

Resultat

$$
\sigma=2.2239
$$

---

# Summor av normalfördelade variabler

## Sats

Om

$$
X\in N(\mu_X,\sigma_X)
$$

och

$$
Y\in N(\mu_Y,\sigma_Y)
$$

oberoende

---

Då

$$
X+Y\in N(\mu_X+\mu_Y,\sqrt{\sigma_X^2+\sigma_Y^2})
$$

---

och

$$
X-Y\in N(\mu_X-\mu_Y,\sqrt{\sigma_X^2+\sigma_Y^2})
$$

---

# Stickprov från normalfördelning

Om

$$
X_1,\dots,X_n
$$

är stickprov från

$$
X\in N(\mu,\sigma)
$$

---

Medelvärde

$$
\bar X_n\in N(\mu,\frac{\sigma}{\sqrt{n}})
$$

---

Skillnad mellan stickprov

$$
\bar X_m-\bar Y_n
\in
N\left(
\mu_X-\mu_Y,
\sqrt{\frac{\sigma_X^2}{m}+\frac{\sigma_Y^2}{n}}
\right)
$$

---

# Exempel

Motstånd har resistens

$$
X\in N(11,1.1)
$$

---

### a)

Sannolikhet att mätning avrundas till

$$
12
$$

---

$$
P(11.5<X\le12.5)
$$

---

$$
=
\Phi(1.36)-\Phi(0.45)
$$

---

$$
=0.9131-0.6736
$$

---

$$
=0.2395
$$

---

### b)

Medelvärde av fyra motstånd

$$
\bar X\in N(11,0.55)
$$

---

$$
P(11.5<\bar X\le12.5)
$$

---

$$
=\Phi(2.73)-\Phi(0.91)
$$

---

$$
=0.9968-0.8186
$$

---

$$
=0.0877
$$

---

# $\chi^2$-fördelning

## Definition

$$
X\in\chi^2_f
$$

med täthet

$$
f(x)=
\frac{x^{f/2-1}e^{-x/2}}
{\Gamma(f/2)2^{f/2}}
$$

---

$$
x\in\mathbb{R}^+
$$

---

### Moment

$$
E(X)=f
$$

$$
V(X)=2f
$$

---

### Sats

Om

$$
X_1,\dots,X_f
$$

är stickprov från

$$
N(0,1)
$$

---

Då

$$
\sum_{i=1}^{f}X_i^2\in\chi^2_f
$$

---

# Exempel

Antag

$$
X,Y\in N(0,1)
$$

oberoende.

---

### a)

Fördelning av

$$
X^2
$$

---

Resultat

$$
X^2\in\chi^2_1
$$

---

### b)

Fördelning av

$$
X^2+Y^2
$$

---

Resultat

$$
X^2+Y^2\in\chi^2_2
$$

---

# Centrala Gränsvärdessatsen (CGS)

## Sats

Om

$$
X_1,\dots,X_n
$$

är stickprov från variabel

$$
E(X)=\mu,\quad D(X)=\sigma
$$

---

Då

$$
\frac{\sum_{i=1}^n X_i-n\mu}{\sigma\sqrt n}
\rightarrow N(0,1)
$$

---

### Approximation

$$
\bar X\approx N\left(\mu,\frac{\sigma}{\sqrt n}\right)
$$

---

$$
\sum X_i\approx N(n\mu,\sigma\sqrt n)
$$

---

# Exempel

83 email analyseras.

Antal misstänkta ord per email:

$$
\mu=0.41
$$

$$
\sigma=0.23
$$

---

Total

$$
S=\sum_{i=1}^{83}X_i
$$

---

Approximation

$$
S\in N(83\cdot0.41,0.23\sqrt{83})
$$

---

$$
= N(34.03,2.10)
$$

---

### Sannolikhet

$$
P(S\ge37)
$$

---

$$
=1-\Phi\left(\frac{36.5-34.03}{2.10}\right)
$$

---

$$
=1-\Phi(1.18)
$$

---

$$
=0.1190
$$

---

# Exempel

Tjocklek av ark:

$$
E(X)=0.097
$$

$$
\sigma=0.02
$$

---

100 ark:

$$
S\in N(100\cdot0.097,0.02\sqrt{100})
$$

---

$$
= N(9.7,0.2)
$$

---

Sannolikhet att blocket innehåller minst 100 ark

$$
P(S\le10)
$$

---

$$
=
\Phi\left(\frac{10-9.7}{0.2}\right)
$$

---

$$
=\Phi(1.5)
$$

---

$$
=0.9332
$$
