# Matematisk statistik
Eric Järpe

## F 13: Hypotesprövning

Eric Järpe  
ITE  
Högskolan i Halmstad  
3 december 2025

---

# Hypotestest

- Matematisk grundad teori för att bevisa påståenden med angiven säkerhet
- Måste användas omdömesfullt
- Man kan göra tekniska fel vid beräkningar och logiska fel vid tolkning av resultat

---

# Procedur vid hypotestest

1. Hypotes

$$
H_0 : \text{nollhypotes}
$$

$$
H_1 : \text{mothypotes}
$$

---

2. Signifikansnivå

$$
\alpha = P(\text{förkasta } H_0)
$$

---

3. Stickprov

$$
x_1,x_2,\dots,x_n
$$

---

4. Teststatistika

$$
T=T(x_1,x_2,\dots,x_n)
$$

---

5. Testregel

$$
A_\alpha
$$

Om

$$
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

# Signifikansnivå och styrka

## Typ I-fel

Förkasta $H_0$ då $H_0$ är sann.

$$
P(\text{Typ I})=\alpha
$$

---

## Typ II-fel

Inte förkasta $H_0$ då $H_1$ är sann.

$$
P(\text{Typ II})=\beta
$$

---

## Testets styrka

$$
1-\beta
$$

---

Vanliga signifikansnivåer

- $0.05$
- $0.01$
- $0.001$

---

# Relation mellan konfidensintervall och hypotest

Ensidigt intervall

$$
P(\theta\in(-\infty,U))=1-\alpha
$$

---

Implikation

$$
P(T<c_\alpha\mid H_0)=\alpha
$$

---

För dubbelsidigt intervall

$$
P(\theta\in(L,U))=1-\alpha
$$

---

Ger testregel

$$
P(|T|>c_{\alpha/2}\mid H_0)=\alpha
$$

---

### Exempel

$$
P\left(\mu\in\left(\bar{X}-t_{\alpha/2}(n-1)\frac{S}{\sqrt{n}},
\bar{X}+t_{\alpha/2}(n-1)\frac{S}{\sqrt{n}}\right)\right)=1-\alpha
$$

---

Ger

$$
T=\frac{\bar{X}-\mu_0}{S/\sqrt{n}}
$$

---

och testregel

$$
|T|>t_{\alpha/2}(n-1)
$$

---

# Hypotestest för $\mu$ då $\sigma$ känd

Hypotes

$$
H_0:\mu=\mu_0
$$

---

Mothypotes

$$
H_1:\mu<\mu_0
$$

$$
H_1:\mu>\mu_0
$$

$$
H_1:\mu\neq\mu_0
$$

---

Teststatistika

$$
T=\frac{\bar{x}-\mu_0}{\sigma/\sqrt{n}}
$$

---

Testregler

$$
A_\alpha=\{T<-\lambda_\alpha\}
$$

$$
A_\alpha=\{T>\lambda_\alpha\}
$$

$$
A_\alpha=\{|T|>\lambda_{\alpha/2}\}
$$

---

# Hypotestest för $\mu$ då $\sigma$ okänd

Stickprov

$$
x_1,x_2,\dots,x_n
$$

---

Medelvärde

$$
\bar{x}=\frac{1}{n}\sum x_i
$$

---

Standardavvikelse

$$
s=\sqrt{\frac{1}{n-1}\left(\sum x_i^2-n\bar{x}^2\right)}
$$

---

Teststatistika

$$
T=\frac{\bar{x}-\mu_0}{s/\sqrt{n}}
$$

---

Testregler

$$
A_\alpha=\{T<-t_\alpha(n-1)\}
$$

$$
A_\alpha=\{T>t_\alpha(n-1)\}
$$

$$
A_\alpha=\{|T|>t_{\alpha/2}(n-1)\}
$$

---

# Hypotestest för varians

Hypotes

$$
H_0:\sigma^2=\sigma_0^2
$$

---

Teststatistika

$$
T=\frac{(n-1)s^2}{\sigma_0^2}
$$

---

Testregler

$$
A_\alpha=\{T<\chi^2_{1-\alpha}(n-1)\}
$$

$$
A_\alpha=\{T>\chi^2_\alpha(n-1)\}
$$

---

Dubbelsidigt

$$
A_\alpha=
\{T<\chi^2_{1-\alpha/2}(n-1)
\text{ eller }
T>\chi^2_{\alpha/2}(n-1)\}
$$

---

# Exempel: test för $\mu$

Programmeraren Putte.

Stickprov

$$
n=100
$$

Standard

$$
\mu_0=9
$$

---

## a)

$$
\bar{x}=9.7
$$

$$
\sigma=3
$$

---

Hypotes

$$
H_0:\mu=9
$$

$$
H_1:\mu>9
$$

---

Teststatistika

$$
T=\frac{(9.7-9)\sqrt{100}}{3}=2.3333
$$

---

Kritiskt värde

$$
\lambda_{0.01}=2.326348
$$

---

Eftersom

$$
2.3333>2.326348
$$

förkastas $H_0$.

---

p-värde

$$
p=1-\Phi(2.33)=0.0099
$$

---

## b)

$$
\bar{x}=8.2
$$

$$
s=3.4
$$

---

Hypotes

$$
H_0:\mu=9
$$

$$
H_1:\mu<9
$$

---

Teststatistika

$$
T=\frac{(8.2-9)\sqrt{100}}{3.4}=-2.3529
$$

---

Kritiskt värde

$$
t_{0.01}(50)\approx2.4033
$$

---

Eftersom

$$
-2.3529>-2.4033
$$

kan $H_0$ inte förkastas.

---

p-värde

$$
0.01<p<0.02
$$

---

# Jämförelse mellan två stickprov

Hypotes

$$
H_0:\mu_1=\mu_2
$$

---

Teststatistika

$$
T=
\frac{\bar{x}-\bar{y}}
{\sqrt{
\frac{(n_1-1)s_1^2+(n_2-1)s_2^2}{n_1+n_2-2}
\left(\frac1{n_1}+\frac1{n_2}\right)
}}
$$

---

Testregel

$$
A_\alpha=\{T<-t_\alpha(n_1+n_2-2)\}
$$

$$
A_\alpha=\{T>t_\alpha(n_1+n_2-2)\}
$$

$$
A_\alpha=\{|T|>t_{\alpha/2}(n_1+n_2-2)\}
$$

---

# Exempel

Raketer:

```
7.7,5.3,5.7,3.4,6.4
```

```
4.6,5.4,1.7,5.8,3.2,4.8,2.5
```

---

Medelvärden

$$
\bar{x}=5.7
$$

$$
\bar{y}=4
$$

---

Teststatistika

$$
T=1.8617
$$

---

Kritiskt värde

$$
t_{0.05}(10)=1.8125
$$

---

Eftersom

$$
1.8617>1.8125
$$

förkastas $H_0$.

---

p-värde

$$
0.025<p<0.05
$$

---

# Test för sannolikheter

Hypotes

$$
H_0:p_1=p_2
$$

---

Teststatistika

$$
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

$$
A_\alpha=\{T<-\lambda_\alpha\}
$$

$$
A_\alpha=\{T>\lambda_\alpha\}
$$

$$
A_\alpha=\{|T|>\lambda_{\alpha/2}\}
$$

---

# Exempel

Ada och Beda

---

Data

$$
p_1^*=\frac{17}{59}=0.2881
$$

$$
p_2^*=\frac{10}{38}=0.2631
$$

---

Teststatistika

$$
T=0.2696
$$

---

Eftersom

$$
|T|<1.959964
$$

kan $H_0$ inte förkastas.

---

p-värde

$$
p=2(1-\Phi(|0.2696|))=0.7872
$$

---

# Testets styrka

Definition

$$
\text{Styrka}=P(\text{förkasta }H_0|H_1)
$$

---

## Exempel

Test

$$
H_0:\mu=0
$$

$$
H_1:\mu>0
$$

---

Parametrar

$$
\alpha=0.05
$$

$$
\sigma=1
$$

$$
n=25
$$

---

Kritiskt värde

$$
\lambda_\alpha=1.644854
$$

---

Styrka

$$
1-\Phi\left(\lambda_\alpha+\frac{\mu_0-\mu}{\sigma/\sqrt{n}}\right)
$$

---

Med

$$
\mu=0.5
$$

---

$$
1-\Phi(-0.8551)=\Phi(0.86)
$$

---

Resultat

$$
0.8051
$$