
# Definition
Skattning av parameter $\theta$, för en stokastisk variabel är en funktion av variablerna i ett stickprov på variabeln:

$$\Large

\theta_{obs}^* = \underbrace{\theta^*(x_1, x_2, \dots, x_n)}_\text{realiserat värde}
\quad \text{och} \quad \theta^* =  \underbrace{\theta^*(X_1, X_2, \dots, X_n)}_\text{stokastiska variabler}
$$

Skattning $\theta_{obs}^*$ är **konsistent** om $lim_{n \rightarrow \infty} P(|\theta_{n}^* - \theta | > \epsilon) = 0$ för varje $\epsilon > 0$. **Medelkvadratfelet** är MSE = $E((\theta_n^* - \theta)^2)$. 

Om $\theta_{obs}^*$ och $\hat{\theta}_{obs}$ både väntevärdesriktiga skattningar av $\theta$ och $V(\theta^*) \le V(\hat{\theta})$ för alla $\theta$ och $V(\theta^*) < V(\hat{\theta})$ för något $\theta$ så är $\theta_{obs}^*$ **effektivare än** $\hat{\theta}_{obs}$.

Eftersom 
$$\Large
\mu_{obs}^* = \bar{x} \ \text{är} \ \mu^* = \bar{X} 
$$
#### Sats 1
 Är $\mu_{obs}^*$ väntevärdesriktig och konsisten skattning av $\mu$

(Bevis mha Chebychevs olikhet.)
$$\Large
(\sigma^2)_{obs}^* = s^2 = \frac{1}{n-1} \sum_{i=1}^n (x_i - \bar{x})^2
$$
$$\Large
(\sigma^2)_{}^* = S^2 = \frac{1}{n-1} \sum_{i=1}^n (X_i - \bar{X})^2
$$
#### Sats 2
$(\sigma^2)_{obs}^*$ är en väntevärdesriktig och konsistent skattning av $\sigma^2$ 

---
## Normalfördelning
## $\sigma^2$ känd

Likelihood

$$\Large
L(\mu) =
\frac{1}{(2\pi\sigma^2)^{n/2}}
e^{-\sum (x_i-\mu)^2/(2\sigma^2)}
$$

---

MLE

$$\Large
\mu^*_{MLE} = \bar{x}
$$

---

## $\mu$ känd

MLE

$$\Large
(\sigma^2)^*_{MLE}
=
\frac{1}{n}\sum_{i=1}^{n}(x_i-\mu)^2
$$

---

## $\mu$ och $\sigma^2$ okända

MLE

$$\Large
\mu^*_{MLE} = \bar{x}
$$

---

$$\Large
(\sigma^2)^*_{MLE}
=
\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2
$$

---

Notera:

$$\Large
(\sigma^2)^*_{MLE}
$$

är **inte väntevärdesriktig**.

---

### MK-skattning

$$\Large
\mu^*_{MK} = \bar{x}
$$

---

$$\Large
(\sigma^2)^*_{MK}
=
\frac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{x})^2
$$


Denna är **väntevärdesriktig**.

---
## Två-sampel fallet

Stickprov

- $\Large x_1,\dots,x_m$
- $\Large y_1,\dots,y_n$


$$\Large
\mu_X,\quad \mu_Y
$$
---
Gemensam varians

$$\Large
\sigma^2
$$

---

MLE

$$\Large
\mu_X^* = \bar{x} 
\quad
\mu_Y^* = \bar{y}
$$

---

$$\Large
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

$$\Large
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

$$\Large
X \sim Bin(n,p)
$$

med känt $n$.

---

MLE och MK

$$\Large
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

$$\Large
X \sim Hyp(N,n,p)
$$

där $n,N$ är kända.

---

Skattning

$$\Large
p^*_{MLE} = p^*_{MK} = \frac{x}{n}
$$

---

# Poissonfördelning

Om

$$\Large
X \sim Poi(\mu)
$$


$$\Large
\mu^*_{MLE} = \mu^*_{MK} = \bar{x}
$$

---

# Medelfel

## Definition

Om parametern $\theta$ skattas med $\theta^*$ så är

$$\Large
d(\theta^*)
$$

en skattning av standardavvikelsen

$$\Large
D(\theta^*)
$$


Det kallas även **standard error (SE)**.

---
# Länkar
[[Matematisk Statistik]]
[[Maximum likelihood]]
[[Minsta Kvadrat Metoden (MK)]]
