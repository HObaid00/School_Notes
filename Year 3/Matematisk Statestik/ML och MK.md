# Matematisk statistik
Eric Järpe

## F 11: ML och MK

Eric Järpe  
ITE  
Högskolan i Halmstad  
10 november 2025

---

# Maximum Likelihood (ML)

För ett givet utfall kan den sammansatta sannolikhetsfunktionen för en diskret variabel respektive den sammansatta tätheten för en kontinuerlig ses som en funktion av den okända parametern $\theta$.

---

## Definition

Om

$$
x_1,x_2,\dots,x_n
$$

är ett stickprov från $X$ vars sannolikhetsfördelning innehåller parametern $\theta$, så är **Likelihoodfunktionen**

$$\Large
L(\theta) =
\begin{cases}
p(x_1,x_2,\dots,x_n;\theta), & X \text{ diskret} \\
f(x_1,x_2,\dots,x_n;\theta), & X \text{ kontinuerlig}
\end{cases}
$$

---

### Observation

$$\Large
L(\theta) =
\begin{cases}
\prod_{i=1}^{n} p(x_i;\theta), & X \text{ diskret} \\
\prod_{i=1}^{n} f(x_i;\theta), & X \text{ kontinuerlig}
\end{cases}
$$

---

# Maximum Likelihood-skattningen (MLE)

## Definition

Maximum likelihood-skattningen är det värde på $\theta$ som maximerar likelihoodfunktionen.

$$\Large
\theta^*_{MLE} = \arg\max_{\theta} L(\theta)
$$

---

### Log-likelihood

I praktiken maximerar man ofta istället

$$\Large
\ln L(\theta) = \ell(\theta)
$$

---

$$\Large
\ell(\theta) =
\begin{cases}
\sum_{i=1}^{n} \ln p(x_i;\theta), & X \text{ diskret} \\
\sum_{i=1}^{n} \ln f(x_i;\theta), & X \text{ kontinuerlig}
\end{cases}
$$

---

# Minsta kvadrat-skattningen (MK)

Antag att

$$\Large
x_1,x_2,\dots,x_n
$$

är ett stickprov från $X$.

---

Låt

$$\Large
\mu(\theta) = E(X;\theta)
$$

---

## Definition

Minsta kvadrat-skattningen definieras som

$$
\theta^*_{MK} = \arg\min_{\theta} Q(\theta)
$$

där

$$
Q(\theta) = \sum_{i=1}^{n}(x_i - \mu(\theta))^2
$$

---

# Exempel: Rayleighfördelning

Vindhastighet $X$ antas vara Rayleighfördelad

$$
F_X(x) = 1 - e^{-x^2/(2\sigma^2)}
$$

med

$$
D_X = \mathbb{R}^+
$$

---

Antag observationer

$$
x_1,x_2,\dots,x_n
$$

---

Beräkna

a) ML-skattningen av $\sigma$

b) MK-skattningen av $\sigma$

---

# a) ML-skattning

Täthetsfunktionen är

$$
f(x) = \frac{x}{\sigma^2} e^{-x^2/(2\sigma^2)}
$$

---

Likelihood

$$
L(\sigma) =
\prod_{i=1}^{n}
\frac{x_i}{\sigma^2}
e^{-x_i^2/(2\sigma^2)}
$$

---

$$
=
\sigma^{-2n}
\left(\prod_{i=1}^{n} x_i\right)
e^{-\frac{1}{2\sigma^2}\sum x_i^2}
$$

---

Log-likelihood

$$
\ell(\sigma) =
-2n\ln\sigma
+
\sum_{i=1}^{n}\ln x_i
-
\frac{1}{2\sigma^2}\sum_{i=1}^{n} x_i^2
$$

---

Maximering

$$
\frac{d\ell}{d\sigma}
=
-\frac{2n}{\sigma}
+
\frac{1}{\sigma^3}\sum x_i^2
=
0
$$

---

Ger

$$
\sigma^*_{ML}
=
\sqrt{\frac{1}{2}\bar{x^2}}
$$

---

# b) MK-skattning

För Rayleighfördelningen gäller

$$
E(X)
=
\sqrt{\frac{\pi}{2}}\sigma
$$

---

Kvadratsumman

$$
Q(\sigma)
=
\sum_{i=1}^{n}
\left(x_i - \sqrt{\frac{\pi}{2}}\sigma\right)^2
$$

---

Minimera genom

$$
\frac{dQ}{d\sigma}=0
$$

---

Ger

$$
\sum_{i=1}^{n}x_i
=
\sqrt{\frac{\pi}{2}} n\sigma
$$

---

Alltså

$$
\sigma^*_{MK}
=
\sqrt{\frac{2}{\pi}}\bar{x}
$$

---

# Punktskattning för normalfördelningen

Antag

$$
X \sim N(\mu,\sigma^2)
$$

---

## Fall 1: $\sigma^2$ känd

Likelihood

$$
L(\mu) =
\frac{1}{(2\pi\sigma^2)^{n/2}}
e^{-\sum (x_i-\mu)^2/(2\sigma^2)}
$$

---

MLE

$$
\mu^*_{MLE} = \bar{x}
$$

---

## Fall 2: $\mu$ känd

MLE

$$
(\sigma^2)^*_{MLE}
=
\frac{1}{n}\sum_{i=1}^{n}(x_i-\mu)^2
$$

---

## Fall 3: $\mu$ och $\sigma^2$ okända

MLE

$$
\mu^*_{MLE} = \bar{x}
$$

---

$$
(\sigma^2)^*_{MLE}
=
\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2
$$

---

Notera:

$$
(\sigma^2)^*_{MLE}
$$

är **inte väntevärdesriktig**.

---

### MK-skattning

$$
\mu^*_{MK} = \bar{x}
$$

---

$$
(\sigma^2)^*_{MK}
=
\frac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{x})^2
$$

---

Denna är **väntevärdesriktig**.

---

# Två-sampel-fallet

Stickprov

- $x_1,\dots,x_m$
- $y_1,\dots,y_n$

---

Väntevärden

$$
\mu_X,\quad \mu_Y
$$

---

Gemensam varians

$$
\sigma^2
$$

---

MLE

$$
\mu_X^* = \bar{x}
$$

---

$$
\mu_Y^* = \bar{y}
$$

---

$$
(\sigma^2)^*_{MLE}
=
\frac{1}{m+n}
\left(
\sum_{i=1}^{m}(x_i-\bar{x})^2
+
\sum_{i=1}^{n}(y_i-\bar{y})^2
\right)
$$

---

### Väntevärdesriktig variansskattning

$$
(\sigma^2)^*
=
\frac{1}{m+n-2}
\left(
\sum_{i=1}^{m}(x_i-\bar{x})^2
+
\sum_{i=1}^{n}(y_i-\bar{y})^2
\right)
$$

---

# Binomialfördelning

Om

$$
X \sim Bin(n,p)
$$

med känt $n$.

---

MLE och MK

$$
p^*_{MLE} = p^*_{MK} = \frac{x}{n}
$$

---

Egenskaper

- väntevärdesriktig
- konsistent
- effektiv

---

# Hypergeometrisk fördelning

Om

$$
X \sim Hyp(N,n,p)
$$

där $n,N$ är kända.

---

Skattning

$$
p^*_{MLE} = p^*_{MK} = \frac{x}{n}
$$

---

# Poissonfördelning

Om

$$
X \sim Poi(\mu)
$$

---

MLE och MK

$$
\mu^*_{MLE} = \mu^*_{MK} = \bar{x}
$$

---

# Medelfel

## Definition

Om parametern $\theta$ skattas med $\theta^*$ så är

$$
d(\theta^*)
$$

en skattning av standardavvikelsen

$$
D(\theta^*)
$$

---

Det kallas även **standard error (SE)**.

---

(Se även Bayesiansk skattning i kursboken.)