# Matematisk statistik
Eric Järpe

## F 12: Intervallskattning

Eric Järpe  
ITE  
Högskolan i Halmstad  
30 november 2025

---

# Konfidensintervall

Antag att vi vill skatta värdet av parametern

$$
\theta
$$

---

## Punktskattning

Ett första steg för att gissa $\theta$.

Men osäkerheten i skattningen är okänd.

---

## Intervallskattning

Istället anger man ett intervall där parametern finns med given sannolikhet.

---

### Definition

Konfidensintervall

$$
(L,U)
$$

så att

$$
P((L,U)\ni\theta)=1-\alpha
$$

där

$$
1-\alpha
$$

är **konfidensgraden**.

---

### Typer av intervall

Ensidiga

$$
(-\infty,U), \quad (L,\infty)
$$

---

Dubbelsidiga

$$
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

$$
X_1,X_2,\dots,X_n
$$

är ett stickprov från $X$

och

$$
X\in N
$$

eller

$$
n>25
$$

---

### Om $\sigma$ känd

$$
\left(
\bar{x}-\lambda_{\alpha/2}\frac{\sigma}{\sqrt{n}},
\bar{x}+\lambda_{\alpha/2}\frac{\sigma}{\sqrt{n}}
\right)
$$

---

### Om $\sigma$ okänd

$$
\left(
\bar{x}-t_{\alpha/2}(n-1)\frac{s}{\sqrt{n}},
\bar{x}+t_{\alpha/2}(n-1)\frac{s}{\sqrt{n}}
\right)
$$

---

# Exempel

Observationer

```
30.8, 17.2, 21.7, 85.8, 81.3, 49.8, 88.1, 16.3, 61.6, 69.6
```

---

Antal observationer

$$
n=10
$$

---

Medelvärde

$$
\bar{x}=52.22
$$

---

## a) $\sigma=30$

95% konfidensintervall

$$
(\bar{x}-\lambda_{\alpha/2}\frac{\sigma}{\sqrt{n}},
\bar{x}+\lambda_{\alpha/2}\frac{\sigma}{\sqrt{n}})
$$

---

$$
\lambda_{\alpha/2}\frac{\sigma}{\sqrt{n}}
=
1.959964\frac{30}{\sqrt{10}}
=
18.594919
$$

---

Alltså

$$
(52.22-18.594919,\;52.22+18.594919)
$$

---

$$
(33.6258,\;70.8142)
$$

---

## b) $\sigma$ okänd

$$
\sum x_i^2=34832.76
$$

---

Standardavvikelse

$$
s=
\sqrt{
\frac{1}{10-1}(34832.76-10\cdot52.22^2)
}
=
28.98942
$$

---

Konfidensintervall

$$
(\bar{x}-t_{\alpha/2,n-1}\frac{s}{\sqrt{n}},
\bar{x}+t_{\alpha/2,n-1}\frac{s}{\sqrt{n}})
$$

---

$$
(52.22-20.73817,\;52.22+20.73817)
$$

---

$$
(31.4818,\;72.9582)
$$

---

# Exempel: Slantsingling

Varje kast

$$
X=
\begin{cases}
1 & \text{krona}\\
0 & \text{klave}
\end{cases}
$$

---

Sannolikhet

$$
P(X=1)=p
$$

---

Medelvärde

$$
E(X)=p
$$

---

Varians

$$
V(X)=p(1-p)
$$

---

Eftersom

$$
p(1-p)\le0.25
$$

---

Konfidensintervall

$$
(\bar{x}-\lambda_{\alpha/2}\frac{\sigma}{\sqrt{n}},
\bar{x}+\lambda_{\alpha/2}\frac{\sigma}{\sqrt{n}})
$$

---

Längd

$$
U-L=2\lambda_{\alpha/2}\frac{\sigma}{\sqrt{n}}
$$

---

Krav

$$
2\cdot1.959964\frac{0.5}{\sqrt{n}}<0.1
$$

---

$$
n>
\left(
\frac{2\cdot1.959964\cdot0.5}{0.1}
\right)^2
=
384.1458
$$

---

Svar

$$
n\ge385
$$

---

# Konfidensintervall för standardavvikelsen

## Sats

Om

$$
X_1,X_2,\dots,X_n
$$

är stickprov från $X$

---

Dubbelsidigt intervall

$$
\left(
\sqrt{\frac{n-1}{\chi^2_{\alpha/2}(n-1)}}s,
\sqrt{\frac{n-1}{\chi^2_{1-\alpha/2}(n-1)}}s
\right)
$$

---

Ensidigt

$$
\left(
0,\sqrt{\frac{n-1}{\chi^2_{1-\alpha}(n-1)}}s
\right)
$$

---

eller

$$
\left(
\sqrt{\frac{n-1}{\chi^2_{\alpha}(n-1)}}s,\infty
\right)
$$

---

# Parade variabler

Antag

$$
X_1,\dots,X_n
$$

och

$$
Y_1,\dots,Y_n
$$

---

Definiera differens

$$
\Delta_i=X_i-Y_i
$$

---

Då kan konfidensintervall bildas för

$$
\mu_X-\mu_Y
$$

---

# Två-sampel-intervall

Stickprov

$$
X_1,\dots,X_{n_1}
$$

och

$$
Y_1,\dots,Y_{n_2}
$$

---

### Om varians känd

$$
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

$$
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

$$
X\sim Bin(n,p)
$$

---

Skattning

$$
p^*=\frac{x}{n}
$$

---

Konfidensintervall

$$
p^*\pm
\lambda_{\alpha/2}
\sqrt{\frac{p^*(1-p^*)}{n}}
$$

---

# Skillnad mellan sannolikheter

Om

$$
X\sim Bin(n_1,p_1)
$$

$$
Y\sim Bin(n_2,p_2)
$$

---

Intervall

$$
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

$$
X\sim Hyp(N,n,p)
$$

---

Konfidensintervall

$$
p^*\pm
\lambda_{\alpha/2}
\sqrt{
\frac{(N-n)p^*(1-p^*)}{(N-1)n}
}
$$

---

# Poissonfördelning

Om

$$
X\sim Poi(\mu)
$$

och $\mu$ stort.

---

Konfidensintervall

$$
x\pm\lambda_{\alpha/2}\sqrt{x}
$$

---

# Exempel: standardavvikelse

Observerade värden för sockerhalt.

---

$$
\sum x_i=990.60
$$

$$
\sum x_i^2=16444.5
$$

---

Standardavvikelse

$$
s=
\sqrt{
\frac{1}{59}
\left(16444.5-\frac{990.6^2}{60}\right)
}
=
1.2329
$$

---

Med

$$
\chi^2_{1-0.01}(59)>29.7067
$$

---

Konfidensintervall

$$
\left(
0,
\sqrt{\frac{59}{29.7067}}\,1.2329
\right)
$$

---

$$
(0,1.7377)
$$

---

# Exempel: differens mellan felsannolikheter

Data

- 59080 tecken, 76 fel
- 83767 tecken, 75 fel

---

Skattningar

$$
p_1^*=\frac{76}{59080}=0.001286
$$

$$
p_2^*=\frac{75}{83767}=0.000895
$$

---

Konfidensintervall

$$
(p_1^*-p_2^*)
\pm
\lambda_{\alpha/2}
\sqrt{
\frac{p_1^*(1-p_1^*)}{n_1}
+
\frac{p_2^*(1-p_2^*)}{n_2}
}
$$

---

Resultat

$$
(0.00003,0.00075)
$$