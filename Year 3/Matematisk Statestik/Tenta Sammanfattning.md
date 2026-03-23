# Matematisk statistik – Tentamenssammanfattning

Denna sammanfattning innehåller de viktigaste begreppen, satserna och formlerna som behövs för att lösa uppgifter i **matematisk statistik och sannolikhet**.

## Centrala områden

1. Sannolikhetslära
2. Slumpvariabler
3. Diskreta och kontinuerliga fördelningar
4. Normalfördelning
5. Centrala gränsvärdessatsen
6. Stickprov och deskriptiv statistik
7. Punktskattning
8. Maximum likelihood (ML) och minsta kvadrat (MK)
9. Konfidensintervall
10. Hypotesprövning
11. $\chi^2$-test

---
# Grundläggande sannolikhet

## Sannolikhet

$$
P(A) \in [0,1]
$$

## Komplement

$$
P(A^c) = 1 - P(A)
$$

## Additionsregel

$$
P(A \cup B) = P(A) + P(B) - P(A \cap B)
$$

## Oberoende händelser

$$
P(A \cap B) = P(A)P(B)
$$

---

# Total sannolikhet

Om

$$
A_1,A_2,\dots,A_n
$$

är en partition:

$$
P(B) = \sum_{i=1}^{n} P(B|A_i)P(A_i)
$$

---

# Bayes sats

$$
P(A_i|B)=
\frac{P(B|A_i)P(A_i)}
{\sum_{j=1}^{n}P(B|A_j)P(A_j)}
$$
---

# Slumpvariabler

En slumpvariabel $X$ är en funktion

$$
X:\Omega \to \mathbb{R}
$$

## Fördelningsfunktion

$$
F_X(x) = P(X \le x)
$$

---

# Diskreta variabler

Sannolikhetsfunktion

$$
p(k)=P(X=k)
$$

---

# Kontinuerliga variabler

Täthetsfunktion

$$
f(x)
$$

så att

$$
P(a\le X \le b)=\int_a^b f(x)dx
$$

och

$$
\int_{-\infty}^{\infty} f(x)dx =1
$$

---

# Moment

## Väntevärde

$$
E(X)
$$

Diskret:

$$
E(X)=\sum x p(x)
$$

Kontinuerlig:

$$
E(X)=\int x f(x)dx
$$

---

## Varians

$$
V(X)=E(X^2)-E(X)^2
$$

Standardavvikelse

$$
D(X)=\sqrt{V(X)}
$$
---

# Viktiga sannolikhetsfördelningar

## Bernoulli

$$
X \sim Bern(p)
$$

$$
P(X=1)=p
$$

$$
E(X)=p
$$

$$
V(X)=p(1-p)
$$

---

# Binomialfördelning

$$
X \sim Bin(n,p)
$$

$$
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}
$$

Moment

$$
E(X)=np
$$

$$
V(X)=np(1-p)
$$

---

# Poissonfördelning

$$
X \sim Poi(\lambda)
$$

$$
P(X=k)=\frac{\lambda^k}{k!}e^{-\lambda}
$$

Moment

$$
E(X)=\lambda
$$

$$
V(X)=\lambda
$$

---

# Geometrisk fördelning

$$
X \sim Geo(p)
$$

$$
P(X=k)=(1-p)^k p
$$

Moment

$$
E(X)=\frac{1-p}{p}
$$

$$
V(X)=\frac{1-p}{p^2}
$$
---

# Normalfördelning

$$
X \sim N(\mu,\sigma)
$$

Täthet

$$
f(x)=
\frac{1}{\sqrt{2\pi}\sigma}
e^{-(x-\mu)^2/(2\sigma^2)}
$$

---

## Standardisering

$$
Z=\frac{X-\mu}{\sigma}
$$

där

$$
Z \sim N(0,1)
$$

---

## Sannolikheter

$$
P(a \le X \le b)
=
\Phi\left(\frac{b-\mu}{\sigma}\right)
-
\Phi\left(\frac{a-\mu}{\sigma}\right)
$$

---

# 68–95–99.7-regeln

$$
P(|X-\mu| \le \sigma) \approx 0.68
$$

$$
P(|X-\mu| \le 2\sigma) \approx 0.95
$$

$$
P(|X-\mu| \le 3\sigma) \approx 0.997
$$
---

# Centrala gränsvärdessatsen

Om

$$
X_1,X_2,\dots,X_n
$$

är oberoende med

$$
E(X)=\mu, \quad D(X)=\sigma
$$

så gäller

$$
\frac{\sum X_i-n\mu}{\sigma\sqrt{n}}
\to N(0,1)
$$

---

Approximation

$$
\bar X \approx N\left(\mu,\frac{\sigma}{\sqrt n}\right)
$$

---

Summan

$$
\sum X_i \approx N(n\mu,\sigma\sqrt n)
$$
---

# Deskriptiv statistik

Stickprov

$$
x_1,x_2,\dots,x_n
$$

---

# Lägesmått

## Medelvärde

$$
\bar{x}=\frac{1}{n}\sum x_i
$$

---

## Median

Mittenvärdet i sorterat stickprov.

---

## Typvärde

Vanligaste observation.

---

# Spridningsmått

## Varians

$$
s^2=
\frac{1}{n-1}
\sum (x_i-\bar{x})^2
$$

---

## Standardavvikelse

$$
s=\sqrt{s^2}
$$

---

## Variationsbredd

$$
R=x_{max}-x_{min}
$$
---
# Punktskattning

Skattning av parameter

$$
\theta^*=\theta^*(X_1,\dots,X_n)
$$

---

## Väntevärdesriktig

$$
E(\theta^*)=\theta
$$

---

## Konsistent

$$
\theta^* \to \theta
$$

när

$$
n \to \infty
$$

---

# Medelkvadratfel

$$
MSE = E((\theta^*-\theta)^2)
$$

---

# Effektivitet

En skattning är effektiv om den har **minst varians** bland väntevärdesriktiga skattningar.

---

# Maximum Likelihood

Likelihoodfunktion

$$
L(\theta)=\prod_{i=1}^n f(x_i;\theta)
$$

---

Log-likelihood

$$
\ell(\theta)=\ln L(\theta)
$$

---

MLE

$$
\theta^*_{MLE} = \arg\max L(\theta)
$$

---

Vanliga resultat

Normalfördelning

$$
\mu^*=\bar{x}
$$

$$
\sigma^2_{MLE}=\frac{1}{n}\sum (x_i-\bar{x})^2
$$

---

Poisson

$$
\mu^*=\bar{x}
$$

---

Binomial

$$
p^*=\frac{x}{n}
$$

---

# Konfidensintervall

Definition

$$
P((L,U)\ni\theta)=1-\alpha
$$

---

# Intervall för väntevärde

## $\sigma$ känd

$$
\bar{x}\pm\lambda_{\alpha/2}\frac{\sigma}{\sqrt n}
$$

---

## $\sigma$ okänd

$$
\bar{x}\pm t_{\alpha/2}(n-1)\frac{s}{\sqrt n}
$$

---

# Varians

$$
\left(
\sqrt{\frac{n-1}{\chi^2_{\alpha/2}}}s,
\sqrt{\frac{n-1}{\chi^2_{1-\alpha/2}}}s
\right)
$$

---

# Binomial sannolikhet

$$
p^* \pm
\lambda_{\alpha/2}
\sqrt{\frac{p^*(1-p^*)}{n}}
$$

---

# Hypotesprövning

Hypoteser

$$
H_0
$$

$$
H_1
$$

---

Signifikansnivå

$$
\alpha
$$

---

Teststatistika

$$
T
$$

---

Beslut

Förkasta $H_0$ om

$$
T \in A_\alpha
$$

---

# Typ I fel

$$
P(\text{förkasta } H_0|H_0)=\alpha
$$

---

# Typ II fel

$$
\beta
$$

---

# Styrka

$$
1-\beta
$$

---

# Test för väntevärde

## $\sigma$ känd

$$
T=\frac{\bar{x}-\mu_0}{\sigma/\sqrt n}
$$

---

## $\sigma$ okänd

$$
T=\frac{\bar{x}-\mu_0}{s/\sqrt n}
$$

---

# Test för varians

$$
T=\frac{(n-1)s^2}{\sigma_0^2}
$$

---

# Två stickprov

$$
T=
\frac{\bar{x}-\bar{y}}
{\sqrt{
\frac{(n_1-1)s_1^2+(n_2-1)s_2^2}{n_1+n_2-2}
\left(\frac1{n_1}+\frac1{n_2}\right)
}}
$$

---

# Test för sannolikheter

$$
T=
\frac{p_1^*-p_2^*}
{\sqrt{
\frac{p_1^*(1-p_1^*)}{n_1}+
\frac{p_2^*(1-p_2^*)}{n_2}
}}
$$

---

# $\chi^2$-test

Test av fördelning

Hypotes

$$
H_0:F=F_0
$$

---

Teststatistika

$$
U=\sum_{k=1}^{K}\frac{(O_k-E_k)^2}{E_k}
$$

---

Förväntade frekvenser

$$
E_k=N P(X\in I_k|H_0)
$$

---

Fördelning

$$
U\sim\chi^2_{K-1}
$$

---

Beslut

Förkasta $H_0$ om

$$
U>\chi^2_{\alpha,K-1}
$$

---

# Tentastrategi

## Steg vid sannolikhetsproblem

1. Identifiera fördelning
2. Standardisera vid normalfördelning
3. Använd tabeller eller $\Phi$

---

## Steg vid konfidensintervall

1. Identifiera parameter
2. Avgör om $\sigma$ är känd
3. Välj normal eller t-fördelning
4. Beräkna intervall

---

## Steg vid hypotestest

1. Formulera $H_0,H_1$
2. Bestäm $\alpha$
3. Beräkna teststatistika
4. Jämför med kritiskt värde
5. Dra slutsats

---

## Vanliga fällor

- glömmer $\sqrt{n}$
- använder normal istället för t
- fel variansformel
- glömmer absolutbelopp i dubbelsidigt test

---
