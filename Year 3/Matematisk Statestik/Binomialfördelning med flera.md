# Matematisk statistik
Eric Järpe

## F 7: Binomialfördelning med flera

Eric Järpe  
ITE  
Högskolan i Halmstad  
22 oktober 2025

---

# Binomialfördelning

## Definition

Om variabeln $X$ är binomialfördelad med parametrarna $n$ och $p$ skrivs

$$
X \in Bin(n,p)
$$

med värderum

$$
S=\{0,1,\dots,n\}
$$

och sannolikhetsfunktion

$$
p(k)=\binom{n}{k}p^k(1-p)^{n-k}
$$

---

## Sats

Om

$$
X\in Bin(n,p)
$$

så gäller

$$
E(X)=np
$$

$$
V(X)=np(1-p)
$$

$$
D(X)=\sqrt{np(1-p)}
$$

---

## Sats

Om

$$
X\in Bin(m,p)
$$

och

$$
Y\in Bin(n,p)
$$

är oberoende, då

$$
X+Y\in Bin(m+n,p)
$$

---

# Binomialfördelningen

## Sats

Om

$$
S=\sum_{i=1}^{n}X_i
$$

där

$$
X_i=
\begin{cases}
1 & \text{med sannolikhet } p \\
0 & \text{med sannolikhet } 1-p
\end{cases}
$$

så

$$
X_i\in Bern(p)
$$

och

$$
S\in Bin(n,p)
$$

---

### Tolkning

En binomialfördelad variabel kan ses som

$$
S=\sum_{i=1}^{n}X_i
$$

där varje $X_i$ är Bernoullifördelad.

---

Eftersom

$$
E(X_i)=p
$$

och

$$
V(X_i)=p(1-p)
$$

får vi via **CGS**

$$
S \approx N(np,\sqrt{np(1-p)})
$$

---

### Normalapproximation

$$
P(S\le k)\approx
\Phi\left(
\frac{k+\frac12-np}{\sqrt{np(1-p)}}
\right)
$$

Den extra termen $\frac12$ kallas **halvkorrektion**.

---

# Exempel

Företaget Datadoktorn reparerar datorer.

Sannolikheten att en hårddisk kan återställas är

$$
p=0.83
$$

---

## a)

Sannolikhet att man lyckas återställa **minst 9 av 10** hårddiskar.

---

Låt

$$
S\in Bin(10,0.83)
$$

---

$$
P(S\ge9)
=
\binom{10}{9}0.83^9 0.17
+
\binom{10}{10}0.83^{10}
$$

---

$$
=0.3177+0.1551
$$

---

$$
=0.4730
$$

---

## b)

Minst **18 av 20** hårddiskar.

---

$$
S\in Bin(20,0.83)
$$

---

$$
P(S\ge18)
=
\binom{20}{18}0.83^{18}0.17^2
+
\binom{20}{19}0.83^{19}0.17
+
\binom{20}{20}0.83^{20}
$$

---

$$
=0.1918+0.0986+0.0240
$$

---

$$
=0.3146
$$

---

# Exempel

Rabarbro Grönfinger planterar tulpanlökar.

Varje kruka innehåller

$$
5
$$

lökar.

Varje lök blommar med sannolikhet

$$
p=0.7
$$

---

Totalt antal krukor

$$
30
$$

---

Total antal tulpaner

$$
S\in Bin(150,0.7)
$$

---

Exakt sannolikhet

$$
P(S\ge100)
=
\sum_{k=100}^{150}
\binom{150}{k}0.7^k0.3^{150-k}
$$

svår att beräkna manuellt.

---

## Normalapproximation

$$
S\approx N(150\cdot0.7,\sqrt{150\cdot0.7\cdot0.3})
$$

---

$$
= N(105,5.61)
$$

---

$$
P(S\ge100)
=
1-P(S\le99)
$$

---

$$
=
1-\Phi\left(
\frac{99+\frac12-105}{5.61}
\right)
$$

---

$$
=1-\Phi(-0.98)
$$

---

$$
=\Phi(0.98)
$$

---

$$
=0.8365
$$

---

(Exakt värde: $0.8366$)

---

# Poissonfördelning

## Definition

Om

$$
X\in Poi(\lambda)
$$

då är

$$
S=\{0,1,2,\dots\}
$$

och

$$
p(k)=\frac{\lambda^k}{k!}e^{-\lambda}
$$

---

## Moment

$$
E(X)=\lambda
$$

$$
V(X)=\lambda
$$

$$
D(X)=\sqrt{\lambda}
$$

---

## Sats

Om

$$
X\in Poi(\lambda_X)
$$

och

$$
Y\in Poi(\lambda_Y)
$$

är oberoende

---

$$
X+Y\in Poi(\lambda_X+\lambda_Y)
$$

---

# Exempel

Antal kunder till bank per timme:

$$
\lambda=4.9
$$

---

## a)

Sannolikhet att **högst 3 kunder** anländer.

---

$$
P(X\le3)
=
P(X=0)+P(X=1)+P(X=2)+P(X=3)
$$

---

$$
=
\left(
1+4.9+\frac{4.9^2}{2}+\frac{4.9^3}{6}
\right)e^{-4.9}
$$

---

$$
=0.2793
$$

---

## b)

Minst **10 000 kunder på ett år**.

---

Arbetstid per år

$$
8\cdot260=2080
$$

timmar.

---

Total antal kunder

$$
S\in Poi(2080\cdot4.9)
$$

---

$$
=Poi(10192)
$$

---

Normalapproximation

$$
P(S\ge10000)
=
1-\Phi\left(
\frac{9999.5-10192}{\sqrt{10192}}
\right)
$$

---

$$
=\Phi(1.91)
$$

---

$$
=0.9719
$$

---

# Geometrisk fördelning

## Definition

$$
X\in Geo(p)
$$

med värderum

$$
S=\{0,1,2,\dots\}
$$

---

Sannolikhetsfunktion

$$
p(k)=(1-p)^kp
$$

---

Fördelningsfunktion

$$
F(x)=1-(1-p)^{x+1}
$$

---

## Moment

$$
E(X)=\frac{1-p}{p}
$$

$$
V(X)=\frac{1-p}{p^2}
$$

$$
D(X)=\sqrt{\frac{1-p}{p^2}}
$$

---

## Sats

Om

$$
X\in Geo(p_X)
$$

och

$$
Y\in Geo(p_Y)
$$

oberoende

---

$$
\min(X,Y)\in Geo(p_X+p_Y-p_Xp_Y)
$$

---

# Exempel

Annette och Bernhard arbetar i kassan.

Antal kunder per 5 minuter:

$$
X\in Geo(0.18)
$$

$$
Y\in Geo(0.19)
$$

---

## a)

$$
P(X\le2)
$$

---

$$
=(1+0.82+0.82^2)\cdot0.18
$$

---

$$
=0.4486
$$

---

## b)

Vinnarantal kunder

$$
\max(X,Y)
$$

---

$$
P(\max(X,Y)\ge4)
=
1-P(\max(X,Y)\le3)
$$

---

$$
=
1-P(X\le3)P(Y\le3)
$$

---

$$
=
1-(1-(1-0.18)^4)(1-(1-0.19)^4)
$$

---

$$
=1-0.5479\cdot0.5695
$$

---

$$
=0.6880
$$

---

## c)

Bernhard arbetar

$$
7\text{ timmar}
$$

---

Antal femminutersperioder

$$
7\cdot12=84
$$

---

Total kunder

$$
S=\sum_{i=1}^{84}X_i
$$

---

Normalapproximation

$$
S\approx
N\left(
84\frac{1-0.19}{0.19},
\sqrt{84\frac{1-0.19}{0.19^2}}
\right)
$$

---

$$
= N(358.1,43.4)
$$

---

$$
P(S\ge350)
=
1-\Phi\left(
\frac{349.5-358.1}{43.4}
\right)
$$

---

$$
=1-\Phi(-0.20)
$$

---

$$
=0.5793
$$
