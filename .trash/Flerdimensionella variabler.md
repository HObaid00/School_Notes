# Matematisk statistik
Eric Järpe

## F 4: Flerdimensionella variabler

Eric Järpe  
ITE  
Högskolan i Halmstad  
30 september 2025

---

# Flera dimensioner

## Definition

En $r$-dimensionell variabel

$$
X = (X_1, X_2, \dots, X_r)
$$

är en funktion definierad på ett utfallsrum $\Omega$ med värden i

$$
\mathbb{R}^r
$$

---

### Fördelningsfunktion

$$
F(x) = F(x_1, x_2, \dots, x_r)
$$

$$
= P(X_1 \le x_1, X_2 \le x_2, \dots, X_r \le x_r)
$$

$$
= P(\{X_1 \le x_1\} \cap \{X_2 \le x_2\} \cap \dots \cap \{X_r \le x_r\})
$$

(eng. *joint distribution function*)

---

# Diskreta variabler i flera dimensioner

Om $(X,Y)$ är en diskret variabel så är dess **sammansatta s.f.**

$$
p_{X,Y}(j,k) = P(X=j, Y=k)
$$

där

$$
S_X, S_Y \subseteq \mathbb{N}
$$

---

### Sannolikhet för mängd

För varje

$$
A \subseteq S_X \times S_Y
$$

är

$$
P((X,Y)\in A) =
\sum_{(j,k)\in A} p_{X,Y}(j,k)
$$

---

### Normalisering

$$
\sum_{(j,k)\in S_X \times S_Y} p_{X,Y}(j,k) = 1
$$

---

### Fördelningsfunktion

$$
F(x,y) =
\sum_{j=0}^{x}\sum_{k=0}^{y} p_{X,Y}(j,k)
$$

---

### Marginalsannolikheter

$$
P(X=j) = \sum_{k\in S_Y} p_{X,Y}(j,k)
$$

$$
P(Y=k) = \sum_{j\in S_X} p_{X,Y}(j,k)
$$

---

# Multinomialfördelning

$$
X=(X_1,X_2,\dots,X_r) \in Mult(n,p_1,p_2,\dots,p_r)
$$

där

- $n \in \mathbb{Z}^+$
- $p_i \in (0,1)$
- $\sum_{i=1}^{r} p_i = 1$

---

### Sannolikhetsfunktion

$$
p(k_1,k_2,\dots,k_r) =
\frac{n!}{k_1!k_2!\dots k_r!}
p_1^{k_1}p_2^{k_2}\dots p_r^{k_r}
$$

där

$$
\sum_{i=1}^{r} k_i = n
$$

---

### Tolkning

Tänk:

$n$ kulor som fördelas på $r$ skålar

- $k_1$ i skål 1
- $k_2$ i skål 2
- osv.

---

# Exempel

Agaton och Begaton spelar ett spel.

Poäng:

$$
1,2,3,\dots
$$

Sannolikheten att Agaton får $a$ poäng och Begaton $b$ är proportionell mot

$$
e^{-ab}
$$

---

### Normeringsvillkor

Låt

- $A$ = Agatons poäng
- $B$ = Begatons poäng

$$
P(A\in S_A, B\in S_B)
=
\sum_{a=1}^{\infty}\sum_{b=1}^{\infty} p_{A,B}(a,b)
$$

---

Med

$$
p_{A,B}(a,b) = Ce^{-ab}
$$

måste

$$
\sum_{a=1}^{\infty}\sum_{b=1}^{\infty} Ce^{-ab} = 1
$$

---

### Nedre gräns

$$
\frac{1}{C}
=
\sum_{a=1}^{\infty}\sum_{b=1}^{\infty} e^{-ab}
$$

vilket ger

$$
C > \frac{e-1}{e}
$$

---

### Övre gräns

Liknande resonemang ger

$$
C < \frac{e(e-1)}{e+1}
$$

---

Alltså

$$
C \in \left(\frac{e-1}{e}, \frac{e(e-1)}{e+1}\right)
$$

---

# Kontinuerliga variabler i flera dimensioner

Om

$$
X=(X_1,X_2,\dots,X_r)
$$

är kontinuerlig så har den täthetsfunktion

$$
f(x_1,x_2,\dots,x_r)
=
\frac{\partial^r}{\partial x_1\dots\partial x_r}
P(X_1\le x_1,\dots,X_r\le x_r)
$$

---

### Sannolikhet

För

$$
A \subseteq S
$$

är

$$
P((X_1,\dots,X_r)\in A)
=
\int\int\dots\int_A
f(x_1,\dots,x_r)
dx_1\dots dx_r
$$

---

### Villkor för täthetsfunktion

1.

$$
f(x_1,\dots,x_r) \ge 0
$$

2.

$$
\int_S f(x_1,\dots,x_r)dx_1\dots dx_r = 1
$$

---

### Fördelningsfunktion

$$
F(x_1,\dots,x_r)
=
\int_{-\infty}^{x_1}
\dots
\int_{-\infty}^{x_r}
f(t_1,\dots,t_r)dt_1\dots dt_r
$$

---

### Marginaltäthet

Täthet för $X_i$ fås genom integration över övriga variabler.

---

# Oberoende stokastiska variabler

Variablerna

$$
X_1,X_2,\dots,X_r
$$

är **oberoende** om

$$
P(X_1\in A_1,\dots,X_r\in A_r)
=
P(X_1\in A_1)\dots P(X_r\in A_r)
$$

---

### Sats

$X$ och $Y$ är oberoende om och endast om

$$
F_{X,Y}(x,y)=F_X(x)F_Y(y)
$$

---

eller

Diskret:

$$
p_{X,Y}(x,y)=p_X(x)p_Y(y)
$$

Kontinuerlig:

$$
f_{X,Y}(x,y)=f_X(x)f_Y(y)
$$

---

# Multivariat likformig fördelning

$$
X=(X_1,\dots,X_r)\in U(S)
$$

där

$$
S\subseteq\mathbb{R}^r
$$

---

### Täthetsfunktion

$$
f(x)=\frac{1}{\|S\|}
$$

för

$$
x\in S
$$

där

$$
\|S\|
$$

är volymen av området.

---

### Exempel

Buffons nålproblem.

---

# Multivariat normalfördelning

$$
X=(X_1,\dots,X_r)\in MN(\mu,\Sigma)
$$

där

- $\mu\in\mathbb{R}^r$
- $\Sigma$ kovariansmatris

---

### Täthetsfunktion

$$
f(x)=
((2\pi)^n \det\Sigma)^{-1}
e^{-\frac12(x-\mu)\Sigma^{-1}(x-\mu)^T}
$$

---

### Sats

Om

$$
(X,Y)\in MN
\left(
\begin{bmatrix}\mu_X\\\mu_Y\end{bmatrix},
\begin{bmatrix}c_{11}&c_{12}\\c_{21}&c_{22}\end{bmatrix}
\right)
$$

så gäller

$$
X|Y=y \in
N\left(
\mu_X+\frac{c_{12}}{c_{22}}(y-\mu_Y),
c_{11}-\frac{c_{12}^2}{c_{22}}
\right)
$$

---

# Exempel

Låt

- $L_A$ = Agdas längd
- $L_H$ = Huldas längd

---

Fördelningar

$$
L_A\in N(170,228)
$$

$$
L_H\in N(162,191)
$$

och

$$
C(L_A,L_H)=205
$$

---

### Beräkning

$$
\mu_A + \frac{c_{12}}{c_{22}}(y-\mu_H)
=
170+\frac{205}{191}(165-162)
=
173.2199
$$

---

### Varians

$$
c_{11}-\frac{c_{12}^2}{c_{22}}
=
228-\frac{205^2}{191}
=
7.9738
$$

---

Alltså

$$
L_A|L_H=165
\in
N(173.2199,7.9738)
$$

---

### Sannolikhet

$$
P(L_A>172|L_H=165)
=
\Phi(0.43)
=
0.6664
$$

---

# Fördelning av max och min

Låt

$$
Z=\max(X_1,\dots,X_r)
$$

$$
W=\min(X_1,\dots,X_r)
$$

---

### Sats

$$
F_Z(z)=F_{X_1}(z)\dots F_{X_r}(z)
$$

---

$$
F_W(w)
=
1-(1-F_{X_1}(w))\dots(1-F_{X_r}(w))
$$

---

# Exempel

10 studenter drar kort.

Låt

$$
X_i
$$

vara valören.

---

Sannolikhet att **maxkortet ≥ ess**

$$
P(\max X_i \ge 14)
$$

---

$$
=
1-P(\max X_i < 14)
$$

---

$$
=
1-P(X_1\le13,\dots,X_{10}\le13)
$$

---

$$
=
1-P(X_1\le13)\dots P(X_{10}\le13)
$$

---

$$
=
1-\left(\frac{12}{13}\right)^{10}
$$

---

$$
=0.5509
$$

---

# Summor av stokastiska variabler

Summan

$$
S=X+Y
$$

har fördelning

---

Diskret:

$$
F_S(s)=\sum_{j\in S_Y} F_X(s-j)p_Y(j)
$$

---

Kontinuerlig:

$$
F_S(s)=\int_{-\infty}^{\infty} F_X(s-y)f_Y(y)dy
$$

---

Täthetsfunktion

Diskret:

$$
f_S(s)=\sum_{j\in S_Y} p_X(s-j)p_Y(j)
$$

---

Kontinuerlig:

$$
f_S(s)=
\int_{-\infty}^{\infty}
f_X(s-y)f_Y(y)dy
$$

---

Detta kallas **faltning** (*convolution*).

---

# Illustration

Stickprov från

$$
X\in U(-1,1)
$$

---

$$
E(X)=0
$$

$$
V(X)=\frac13
$$

---

Standardisering

$$
\sqrt{n}\frac{\bar X-E(X)}{\sqrt{V(X)}}
$$

![[Pasted image 20260305150338.png|697]]

![[Pasted image 20260305150356.png]]

![[Pasted image 20260305150413.png]]

![[Pasted image 20260305150455.png]]