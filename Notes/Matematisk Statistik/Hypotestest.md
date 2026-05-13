# Hypotestest

- Matematisk grundad teori för att bevisa påståenden med angiven säkerhet
- Måste användas omdömesfullt
- Man kan göra tekniska fel vid beräkningar och logiska fel vid tolkning av resultat

---

# Procedur vid hypotestest

1. Hypotes

$$\Large
H_0 : \text{nollhypotes}
$$

$$\Large
H_1 : \text{mothypotes}
$$

---

2. Signifikansnivå

$$\Large
\alpha = P(\text{förkasta } H_0)
$$

---

3. Stickprov

$$\Large
x_1,x_2,\dots,x_n
$$

---

4. Teststatistika

$$\Large
T=T(x_1,x_2,\dots,x_n)
$$

---

5. Testregel

Om

$$\Large
A_\alpha
$$

förkastas $H_0$.

Om inte kan inget bevisas.

---

6. p-värde

$$
p=\min\{\alpha : A_\alpha(T_{obs})\}
$$

---


# Hypotestest för $\mu$ då $\sigma$ känd

Hypotes

$$\Large
H_0:\mu=\mu_0
$$

---

Mothypotes

$$\Large
H_1:\mu<\mu_0
$$

$$\Large
H_1:\mu>\mu_0
$$

$$\Large
H_1:\mu\neq\mu_0
$$

---

Teststatistika

$$\Large
T=\frac{\bar{x}-\mu_0}{\sigma/\sqrt{n}}
$$

---

Testregler

$$\Large
A_\alpha=\{T<-\lambda_\alpha\}
$$

$$\Large
A_\alpha=\{T>\lambda_\alpha\}
$$

$$\Large
A_\alpha=\{|T|>\lambda_{\alpha/2}\}
$$

---

# Hypotestest för $\mu$ då $\sigma$ okänd

Stickprov

$$\Large
x_1,x_2,\dots,x_n
$$

---

Medelvärde

$$\Large
\bar{x}=\frac{1}{n}\sum x_i
$$

---

Standardavvikelse

$$\Large
s=\sqrt{\frac{1}{n-1}\left(\sum x_i^2-n\bar{x}^2\right)}
$$

---

Teststatistika

$$\Large
T=\frac{\bar{x}-\mu_0}{s/\sqrt{n}}
$$

---

Testregler

$$\Large
A_\alpha=\{T<-t_\alpha(n-1)\}
$$

$$\Large
A_\alpha=\{T>t_\alpha(n-1)\}
$$

$$\Large
A_\alpha=\{|T|>t_{\alpha/2}(n-1)\}
$$

---

# Hypotestest för varians

Hypotes

$$\Large
H_0:\sigma^2=\sigma_0^2
$$

---

Teststatistika

$$\Large
T=\frac{(n-1)s^2}{\sigma_0^2}
$$

---

Testregler

$$\Large
A_\alpha=\{T<\chi^2_{1-\alpha}(n-1)\}
$$

$$\Large
A_\alpha=\{T>\chi^2_\alpha(n-1)\}
$$

---

Dubbelsidigt

$$\Large
A_\alpha=
\{T<\chi^2_{1-\alpha/2}(n-1)
\text{ eller }
T>\chi^2_{\alpha/2}(n-1)\}
$$

---

# Jämförelse mellan två stickprov

Hypotes

$$\Large
H_0:\mu_1=\mu_2
$$

---

Teststatistika

$$\Large
T=
\frac{\bar{x}-\bar{y}}
{\sqrt{
\frac{(n_1-1)s_1^2+(n_2-1)s_2^2}{n_1+n_2-2}
\left(\frac1{n_1}+\frac1{n_2}\right)
}}
$$

---

Testregel

$$\Large
A_\alpha=\{T<-t_\alpha(n_1+n_2-2)\}
$$

$$\Large
A_\alpha=\{T>t_\alpha(n_1+n_2-2)\}
$$

$$\Large
A_\alpha=\{|T|>t_{\alpha/2}(n_1+n_2-2)\}
$$

---

# Test för sannolikheter

Hypotes

$$\Large
H_0:p_1=p_2
$$

---

Teststatistika

$$\Large
T=
\frac{p_1^*-p_2^*}
{\sqrt{
\frac{p_1^*(1-p_1^*)}{n_1}
+
\frac{p_2^*(1-p_2^*)}{n_2}
}}
$$

---

Testregel

$$\Large
A_\alpha=\{T<-\lambda_\alpha\}
$$

$$\Large
A_\alpha=\{T>\lambda_\alpha\}
$$

$$\Large
A_\alpha=\{|T|>\lambda_{\alpha/2}\}
$$

---
# Testets styrka

Definition

$$\Large
\text{Styrka}=P(\text{förkasta }H_0|H_1)
$$

---

# Länkar
[[Matematisk Statistik]]