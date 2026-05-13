
### Definition

Konfidensintervall

$$\Large
(L,U)
$$

så att

$$\Large
P((L,U)\ni\theta)=1-\alpha
$$

där

$$\Large
1-\alpha
$$

är **konfidensgraden**.

---

### Typer av intervall

Ensidiga

$$\Large
(-\infty,U), \quad (L,\infty)
$$

---

Dubbelsidiga

$$\Large
(L,U)
$$

---

Vanliga konfidensgrader

- 95%
- 99%
- 90%

---

# Konfidensintervall för väntevärdet

## Sats

Om

$$\Large
X_1,X_2,\dots,X_n
$$

är ett stickprov från $X$

och

$$\Large
X\in N
$$

eller

$$ \Large
n>25
$$

---

### Om $\sigma$ känd

$$\Large
\left(
\bar{x}-\lambda_{\alpha/2}\frac{\sigma}{\sqrt{n}},
\bar{x}+\lambda_{\alpha/2}\frac{\sigma}{\sqrt{n}}
\right)
$$

---

### Om $\sigma$ okänd

$$ \Large
\left(
\bar{x}-t_{\alpha/2}(n-1)\frac{s}{\sqrt{n}},
\bar{x}+t_{\alpha/2}(n-1)\frac{s}{\sqrt{n}}
\right)
$$

---
# Konfidensintervall för standardavvikelsen

## Sats

Om

$$\Large
X_1,X_2,\dots,X_n
$$

är stickprov från $X$

---

Dubbelsidigt intervall

$$\Large
\left(
\sqrt{\frac{n-1}{\chi^2_{\alpha/2}(n-1)}}s,
\sqrt{\frac{n-1}{\chi^2_{1-\alpha/2}(n-1)}}s
\right)
$$

---

Ensidigt

$$\Large
\left(
0,\sqrt{\frac{n-1}{\chi^2_{1-\alpha}(n-1)}}s
\right)
$$

---

eller

$$\Large
\left(
\sqrt{\frac{n-1}{\chi^2_{\alpha}(n-1)}}s,\infty
\right)
$$

---

# Parade variabler

Antag

$$\Large
X_1,\dots,X_n
$$

och

$$\Large
Y_1,\dots,Y_n
$$

---

Definiera differens

$$\Large
\Delta_i=X_i-Y_i
$$

---

Då kan konfidensintervall bildas för

$$\Large
\mu_X-\mu_Y
$$

---

# Två-sampel-intervall

Stickprov

$$\Large
X_1,\dots,X_{n_1}
$$

och

$$\Large
Y_1,\dots,Y_{n_2}
$$

---

### Om varians känd

$$\Large
\bar{x}-\bar{y}\pm
\lambda_{\alpha/2}
\sqrt{
\frac{\sigma_1^2}{n_1}
+
\frac{\sigma_2^2}{n_2}
}
$$

---

### Om varians okänd

$$\Large
\bar{x}-\bar{y}
\pm
t_{\alpha/2}(n_1+n_2-2)
\sqrt{
\frac{(n_1-1)s_1^2+(n_2-1)s_2^2}{n_1+n_2-2}
\left(\frac1{n_1}+\frac1{n_2}\right)
}
$$

---

# Konfidensintervall för sannolikheter

## Binomial

Om

$$\Large
X\sim Bin(n,p)
$$

---

Skattning

$$\Large
p^*=\frac{x}{n}
$$

---

Konfidensintervall

$$\Large
p^*\pm
\lambda_{\alpha/2}
\sqrt{\frac{p^*(1-p^*)}{n}}
$$

---

# Skillnad mellan sannolikheter

Om

$$\Large
X\sim Bin(n_1,p_1)
$$

$$\Large
Y\sim Bin(n_2,p_2)
$$

---

Intervall

$$\Large
p_1^*-p_2^*
\pm
\lambda_{\alpha/2}
\sqrt{
\frac{p_1^*(1-p_1^*)}{n_1}
+
\frac{p_2^*(1-p_2^*)}{n_2}
}
$$

---

# Hypergeometrisk fördelning

Om

$$\Large
X\sim Hyp(N,n,p)
$$

---

Konfidensintervall

$$\Large
p^*\pm
\lambda_{\alpha/2}
\sqrt{
\frac{(N-n)p^*(1-p^*)}{(N-1)n}
}
$$

---

# Poissonfördelning

Om

$$\Large
X\sim Poi(\mu)
$$

och $\mu$ stort.

---

Konfidensintervall

$$\Large
x\pm\lambda_{\alpha/2}\sqrt{x}
$$

---
