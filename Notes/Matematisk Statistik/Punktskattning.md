# Punktskattning

---

## Normalfördelning

### Fall 1: $\sigma^2$ känd

$$\Large
\mu^*_{MLE} = \bar{x}
$$

---

### Fall 2: $\mu$ känd

$$\Large
(\sigma^2)^*_{MLE} = \frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^2
$$

---

### Fall 3: $\mu$ och $\sigma^2$ okända

$$\Large
\mu^*_{MLE} = \bar{x}
$$

$$\Large
(\sigma^2)^*_{MLE} = \frac{1}{n} \sum_{i=1}^{n} (x_i - \bar{x})^2
$$

MK-skattning:

$$\Large
(\sigma^2)^*_{MK} = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})^2
$$

---

## Två-sampel-fall (normalfördelning)

Stickprov $x$ (storlek $m$) och $y$ (storlek $n$):

$$\Large
(\mu_X)^*_{MLE} = \bar{x}, \quad (\mu_Y)^*_{MLE} = \bar{y}
$$

$$\Large
(\sigma^2)^*_{MLE} = \frac{1}{m+n} \left( \sum_{i=1}^{m} (x_i - \bar{x})^2 + \sum_{i=1}^{n} (y_i - \bar{y})^2 \right)
$$

Väntevärdesriktig skattning:

$$\Large
(\sigma^2)^* = \frac{1}{m+n-2} \left( \sum_{i=1}^{m} (x_i - \bar{x})^2 + \sum_{i=1}^{n} (y_i - \bar{y})^2 \right)
$$

---

## Binomialfördelning

För $X \in \text{Bin}(n, p)$:

$$\Large
p^*_{MLE} = p^*_{MK} = \frac{x}{n}
$$

---

## Hypergeometrisk fördelning

$$\Large
p^*_{MLE} = p^*_{MK} = \frac{x}{n}
$$

---

## Poissonfördelning

$$\Large
\mu^*_{MLE} = \mu^*_{MK} = \bar{x}
$$

---

## Standard Error (SE)

Om $\theta$ skattas med $\theta^*$:

$$\Large
d(\theta^*) = \text{SE} = \text{skattning av } D(\theta^*)
$$