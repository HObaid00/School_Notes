# Matematisk statistik
Eric Järpe

## F 8: Simulering

Eric Järpe  
ITE  
Högskolan i Halmstad  
24 oktober 2025

---

# Simulering

- Beräkning av egenskaper för variabler och stokastiska system kan bli svåra (t.o.m. omöjliga) med analytiska metoder.
- Punktskattning ett alternativ.
- Behöver dock slumptal.
- Undersökningar som ger observationer dyra och omständiga.
- Simuleringar bekvämare och mer kontrollerbara.

---

### Slumptal

- **TRNG** – äkta slumptal (dock ofta svårtillgängliga).
- **PRNG** – pseudo-slumptal.

Kvaliteten på slumptalen är viktig.

---

### Programvara

Kan använda

- **R**
- Matlab
- andra beräkningsmiljöer

---

# Simulering med R

För att komma igång rekommenderas dokumentet **get staRted** på kurshemsidan.

Mer dokumentation:

https://www.r-project.org

---

### Slumptalsfunktion

```
runif(n,a,b)
```

ger

$$
n
$$

realiseringar av

$$
X\in U(a,b)
$$

---

### PRNG-generatorer

Exempel på generatorer:

- Mersenne Twister (standard)
- Wichman–Hill
- Marsaglia–Multicarry
- Super-Duper
- Knuth-TAOCP-2002

---

# Inversionsmetoden

## Algoritm

**Uppgift:** simulera $n$ observationer av $X$ med fördelningsfunktion $F_X$.

**In:** $n, F_X$  
**Ut:** $x_1,x_2,\dots,x_n$

---

### Steg

1. Generera slumptal

$$
u_1,u_2,\dots,u_n
$$

från

$$
U(0,1)
$$

---

2. Beräkna

$$
x_1 = F_X^{-1}(u_1)
$$

$$
x_2 = F_X^{-1}(u_2)
$$

$$
\dots
$$

$$
x_n = F_X^{-1}(u_n)
$$

---

### Kommentar

Metoden fungerar bra för

- likformig fördelning
- exponentialfördelning
- Weibullfördelning

---

### Diskreta variabler

Använd **generaliserad invers**

$$
F^{-1}(y)=\min\{x: F(x)\ge y\}
$$

---

# Normalfördelning

För normalfördelning används **Box–Müllers metod**.

---

## Algoritm

**Uppgift:** simulera $2n$ observationer av

$$
X\in N(0,1)
$$

---

**In:** $n$

**Ut:** $x_1,x_2,\dots,x_{2n}$

---

### Steg 1

Generera

$$
u_1,u_2,\dots,u_{2n}
$$

från

$$
U(0,1)
$$

---

### Steg 2

För

$$
i=1,2,\dots,n
$$

beräkna

$$
x_{2i-1}
=
\cos(2\pi u_{2i-1})
\sqrt{-2\ln(u_{2i})}
$$

---

$$
x_{2i}
=
\sin(2\pi u_{2i-1})
\sqrt{-2\ln(u_{2i})}
$$

---

### Allmän normalfördelning

Simulera

$$
X\in N(\mu,\sigma)
$$

via

$$
x=\mu+\sigma y
$$

där

$$
y\in N(0,1)
$$

---

# Exempel

Simulera en

a) **1-dimensionell Brownsk rörelse**

(slumpvandring med normalfördelade innovationer)

---

b) **Cauchyprocess**

En sekvens

$$
y_1,y_2,y_3,\dots
$$

där

$$
y_t=\sum_{k=1}^{\lfloor t \rfloor} x_k
$$

och

$$
x_k \in Cauchy(0,1)
$$

---

## Lösning (a)

Givet

$$
u_1,u_2,\dots,u_{2n}
$$

generera

$$
z_1,z_2,\dots,z_{2n}
$$

med **Box-Müller**.

---

Skapa därefter

$$
x_t=\sum_{i=1}^{t} z_i
$$

vilket ger en **Brownsk rörelse**.

![[Pasted image 20260306141423.png]]

---

## Lösning (b)

Täthetsfunktion för Cauchy:

$$
f(x)=\frac{1}{\pi(1+x^2)}
$$

---

Fördelningsfunktion

$$
F(x)=
\int_{-\infty}^{x}\frac{dt}{\pi(1+t^2)}
$$

---

$$
=
\frac{1}{\pi}\arctan(x)+\frac{1}{2}
$$

---

Invers funktion

$$
F^{-1}(y)=\tan\left(\pi\left(y-\frac12\right)\right)
$$

---

Så givet

$$
u_1,u_2,\dots,u_n
$$

definieras

$$
x_t=\sum_{i=1}^{t}F^{-1}(u_i)
$$

![[Pasted image 20260306141503.png]]

---

# Exempel

Simulera väntevärdet av **stopptiden Cusum**

---

Stopptid

$$
\tau
=
\min\{t\in\mathbb{Z}^+ : a_t>1+\mu\}
$$

---

där

$$
a_0=0
$$

och

$$
a_t=\max(0,a_{t-1})+z_t
$$

---

där

$$
z_t\in N(\mu,1)
$$

och variablerna är oberoende.

---

## Lösning

1. Generera

$$
z_1,z_2,\dots,z_n
$$

med **Box-Müller**.

---

2. Beräkna

$$
a_t
$$

rekursivt.

---

3. Bestäm

$$
\tau_k
=
\min\{t: a_t>1+\mu\}
$$

---

4. Upprepa proceduren

$$
k=1,2,\dots,1000
$$

---

5. Skatta väntevärdet

$$
\hat{\mu}_\tau
=
\bar{\tau}
=
\frac{1}{1000}
\sum_{k=1}^{1000}\tau_k
$$

---

6. Upprepa hela proceduren för

$$
\mu=0,0.1,0.2,\dots,5
$$

![[Pasted image 20260306141536.png]]