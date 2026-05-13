## F 3: Stokastiska variabler

Eric Järpe  
ITE  
Högskolan i Halmstad  
23 september 2025

---

# Stokastiska variabler

## Definition

En **stokastisk variabel** är en reellvärd funktion på ett utfallsrum $\Omega$.

- Betecknas typiskt av $X(\omega)$, $Y(\omega)$, $Z(\omega)$ eller vanligare $X, Y, Z$.
- Motiverat då händelser oftast handlar om kvantiteter: antal, storlek, tid, …

---

### Värderum

Värdemängden $S$ för variabeln

$$
X : \Omega \to S \subseteq \mathbb{R}
$$

kallas **värderummet**.

---

### Diskret variabel

Variabeln är **diskret** om värderummet är uppräkneligt.

Då har variabeln en **sannolikhetsfunktion (s.f.)**

$$
p(x) = P(X = x), \quad x \in S
$$

---

### Kontinuerlig variabel

Variabeln är **kontinuerlig** om värderummet är kontinuerligt.

Då har den en **täthetsfunktion (t.f.)**

$$
f(x) = \frac{d}{dx}P(X \le x), \quad x \in S
$$

---

# Diskreta variabler

Vanligen är diskreta variabler **antal av olika slag**.

Villkoret:

$$
S \text{ är uppräknelig}
$$

Vi kan anta

$$
S = \{0,1,2,\dots\} = \mathbb{N}
$$

---

### Total sannolikhet

$$
P(X \in S) =
\sum_{k=0}^{\infty} p(k) = 1
$$

---

### Sannolikhet upp till $m$

$$
P(X \le m) =
\sum_{k=0}^{m} p(k)
$$

---

### Intervall

$$
P(a \le X \le b) =
\sum_{k=a}^{b} p(k)
$$

eller

$$
P(X \le b) - P(X \le a-1)
$$

---

### OBS

För diskreta variabler

$$
P(X \le x) \neq P(X < x)
$$

---

# Exempel

Vad är sannolikheten att

### a)

en fembarnsfamilj har $k$ pojkar och $5-k$ flickor?

---

### Lösning

$$
P(k \text{ pojkar}) =
\binom{5}{k} 0.5^k (1-0.5)^{5-k}
$$

Om

$$
X = \text{antal pojkar}
$$

så är $X$ en diskret variabel med s.f.

$$
p(x) =
\binom{5}{x} 0.5^x (1-0.5)^{5-x}
$$

eller

$$
p(x) =
\binom{5}{x}2^{-5}
$$

där

$$
x \in \{0,1,2,3,4,5\}
$$

---

### b)

$n$-barnsfamilj

$$
P(k \text{ pojkar}) =
\binom{n}{k}0.5^k(1-0.5)^{n-k}
$$

dvs

$$
p(x) =
\binom{n}{x}2^{-n}
$$

för

$$
x \in \{0,1,\dots,n\}
$$

---

### c)

Om

$$
P(\text{pojke}) = p
$$

så

$$
P(k \text{ pojkar}) =
\binom{n}{k}p^k(1-p)^{n-k}
$$

---

### d)

Antag

- pojke: $p$
- flicka: $q$
- icke-binär: $1-p-q$

---

Sannolikhet

$$
P(j \text{ pojkar och } k \text{ flickor})
$$

$$
=
\binom{n}{j}\binom{n-j}{k}
p^j q^k (1-p-q)^{n-j-k}
$$

---

Om

$$
(X,Y) = (\text{antal pojkar},\text{antal flickor})
$$

så är

$$
(X,Y)
$$

en **2-dimensionell diskret variabel**

med s.f.

$$
p(x,y) =
\frac{n!}{x!y!(n-x-y)!}
p^x q^y (1-p-q)^{n-x-y}
$$

där

$$
x,y \in \{0,1,\dots,n\}, \quad x+y \le n
$$

---

# Diskreta fördelningar

Sannolikhetsfunktionen måste uppfylla

$$
p(k) \ge 0
$$

och

$$
\sum_{k\in S} p(k)=1
$$

---

Vanliga diskreta fördelningar:

- Bernoullifördelning
- Diskret likformig
- Geometrisk
- Binomial
- Hypergeometrisk
- Poisson

---

# Bernoullifördelning

$$
X \in Bern(p), \quad p \in (0,1)
$$

Värderum

$$
S = \{0,1\}
$$

Sannolikhetsfunktion

$$
p(k) =
\begin{cases}
p & k=1 \\
1-p & k=0
\end{cases}
$$

---

## FIGUR ATT INFÖRA

Under **Bernoullifördelning**

Infoga **diagrammet för Bernoullifördelning**.

---

# Diskret likformig fördelning

$$
X \in U(n), \quad n \in \mathbb{Z}^+
$$

Värderum

$$
S = \{1,2,\dots,n\}
$$

Sannolikhetsfunktion

$$
p(k)=\frac{1}{n}
$$

![[Pasted image 20260305142523.png|697]]
---

# Geometrisk fördelning

$$
X \in Geo(p)
$$

Värderum

$$
S = \{0,1,2,\dots\}
$$

Sannolikhetsfunktion

$$
p(k) = (1-p)^k p
$$

![[Pasted image 20260305142607.png|697]]

---

# Binomialfördelning

$$
X \in Bin(n,p)
$$

Värderum

$$
S = \{0,1,\dots,n\}
$$

Sannolikhetsfunktion

$$
p(k) =
\binom{n}{k}
p^k(1-p)^{n-k}
$$

![[Pasted image 20260305142632.png|697]]

---

# Hypergeometrisk fördelning

$$
X \in Hyp(N,n,p)
$$

där

$$
p = \frac{v}{N}
$$

---

Värderum

$$
S = \{0,1,\dots,n\}
$$

---

Sannolikhetsfunktion

$$
p(k)=
\begin{cases}
\frac{\binom{v}{k}\binom{N-v}{n-k}}{\binom{N}{n}}
& 0\le k\le v, \; 0\le n-k \le N-v \\
0 & annars
\end{cases}
$$

![[Pasted image 20260305142704.png|697]]

---

# Poissonfördelning

$$
X \in Poi(\lambda)
$$

där

$$
\lambda \in \mathbb{R}^+
$$

---

Värderum

$$
S = \{0,1,2,\dots\}
$$

---

Sannolikhetsfunktion

$$
p(k)=
\frac{\lambda^k}{k!}e^{-\lambda}
$$

![[Pasted image 20260305142726.png|697]]

---

# Exempel

Antag att vi kastar **häftstift**.

Sannolikheten att det hamnar **spik ned** är

$$
0.37
$$

---

### a)

$$
X = \text{antal spik ned vid 100 kast}
$$

Värderum

$$
S_X=\{0,1,\dots,100\}
$$

Sannolikhetsfunktion

$$
p_X(k)=
\binom{100}{k}0.37^k0.63^{100-k}
$$

Alltså

$$
X \in Bin(100,0.37)
$$

---

### b)

$$
Y = \text{antal kast innan första spik ned}
$$

Värderum

$$
S_Y = \{0,1,2,\dots\}
$$

Sannolikhetsfunktion

$$
p_Y(k) = (1-0.37)^k 0.37
$$

Alltså

$$
Y \in Geo(0.37)
$$

---

# Kontinuerliga variabler

Vissa egenskaper som

- längd
- vikt
- tid
- hastighet

kan anta **alla positiva värden i $\mathbb{R}$**.

---

Då används **kontinuerliga fördelningar**.

Nu gäller

$$
P(X=x)=0
$$

för alla $x$.

---

Men

$$
P(a \le X \le b)
$$

är meningsfull.

---

### Intervallsannolikhet

$$
P(a \le X \le b) =
\int_a^b f(x)dx
$$

---

# Skillnader diskret / kontinuerlig

Diskret:

$$
P(X=x) > 0
$$

Kontinuerlig:

$$
P(X=x)=0
$$

---

Diskret:

$$
P(X\le x) \ne P(X<x)
$$

Kontinuerlig:

$$
P(X\le x) = P(X<x)
$$

---

Diskret:

$$
p(x)=P(X=x)
$$

Kontinuerlig:

$$
f(x)=\frac{d}{dx}P(X\le x)
$$

---

# Exempel

Antag

$$
f(x)=Cx\cos x
$$

med

$$
S=(0,\frac{\pi}{2})
$$

---

### a)

Verifiera att $f$ kan vara täthetsfunktion.

Villkor:

1.

$$
f(x) \ge 0
$$

2.

$$
\int_S f(x)dx = 1
$$

---

### b)

Beräkna konstanten $C$.

Resultat

$$
C = \frac{2}{\pi-2}
$$

---

### c)

$$
P\left(X \le \frac{\pi}{4}\right)
$$

---

Resultat

$$
0.4598
$$

---

# Kontinuerliga fördelningar

Vanliga:

- Likformig
- Exponential
- Normal
- Weibull
- Gamma
- t-fördelning
- $\chi^2$-fördelning

---

# Likformig fördelning

$$
X \in U(a,b)
$$

Värderum

$$
S=[a,b]
$$

Täthetsfunktion

$$
f(x)=
\begin{cases}
\frac{1}{b-a} & a \le x \le b \\
0 & annars
\end{cases}
$$

![[Pasted image 20260305142822.png]]

---

# Exponentialfördelning

$$
X \in Exp(\lambda)
$$

Värderum

$$
S=\mathbb{R}^+
$$

Täthetsfunktion

$$
f(x)=\lambda e^{-\lambda x}
$$

![[Pasted image 20260305142840.png]]

---

# Normalfördelning

$$
X \in N(\mu,\sigma^2)
$$

Täthetsfunktion

$$
f(x)=
\frac{1}{\sigma\sqrt{2\pi}}
e^{-(x-\mu)^2/(2\sigma^2)}
$$

![[Pasted image 20260305142856.png]]

---

# Weibullfördelning

$$
X \in Wei(\lambda,c)
$$

Täthetsfunktion

$$
f(x)=\lambda c (\lambda x)^{c-1}e^{-(\lambda x)^c}
$$

![[Pasted image 20260305142911.png]]

---

# Gammafördelning

$$
X \in Gamma(\lambda,c)
$$

Täthetsfunktion

$$
f(x)=
\frac{\lambda^c}{\Gamma(c)}
x^{c-1}e^{-\lambda x}
$$

där

$$
\Gamma(c)=\int_0^\infty x^{c-1}e^{-x}dx
$$

och

$$
\Gamma(c)=(c-1)!
$$

om

$$
c \in \mathbb{Z}^+
$$

![[Pasted image 20260305142929.png]]

---

# Fördelningsfunktioner

Fördelningsfunktionen

$$
F(x)=P(X \le x)
$$

---

### Samband

Diskret:

$$
F(x)=\sum_{k=-\infty}^{x}p(k)
$$

Kontinuerlig:

$$
F(x)=\int_{-\infty}^{x}f(t)dt
$$

---

### Egenskaper

1.

$$
\lim_{x\to-\infty}F(x)=0
$$

2.

$$
\lim_{x\to\infty}F(x)=1
$$

3.

$F(x)$ är högerkontinuerlig.

4.

$F(x)$ är växande.

---

### Intervall

$$
P(a < X \le b)=F(b)-F(a)
$$

---

### Definition

$\alpha$-kvantilen är talet $x_\alpha$ sådant att

$$
F(x_\alpha)=1-\alpha
$$

---

# Exempel

Vi anländer till en busshållplats där bussarna går var **20:e minut**.

Antag

$$
X \in U(0,20)
$$

---

Beräkna

$$
P(3 \le X \le 10)
$$

---

$$
P(3 \le X \le 10)
=
\int_3^{10}\frac{1}{20}dx
$$

---

$$
=
\frac{1}{20}(10-3)
$$

---

$$
=\frac{7}{20}=0.35
$$

---

# Exempel

Ett klassrum upplyses av **10 parallellkopplade lampor**.

För varje lampa

$$
P(X_i > 100)=0.8
$$

Livslängd antas **exponentialfördelad**.

---

$$
P(X_i \le x)=1-e^{-\lambda x}
$$

---

Eftersom

$$
P(X_i>100)=0.8
$$

får vi

$$
0.8=e^{-100\lambda}
$$

---

$$
\lambda=-\frac{\ln 0.8}{100}
$$

---

September:

$$
30\cdot24=720
$$

Totalt:

$$
744
$$

timmar.

---

Sannolikheten att det finns ljus:

$$
1-P(\text{alla lampor trasiga})
$$

---

$$
1-P(X_1<744)\cdots P(X_{10}<744)
$$

---

Resultat

$$
1-(0.8098)^{10}=0.8786
$$