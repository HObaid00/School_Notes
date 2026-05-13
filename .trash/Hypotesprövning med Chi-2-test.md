# Matematisk statistik
Eric Järpe

## F 14: Hypotesprövning med $\chi^2$-test

Eric Järpe  
Akademin för informationsteknologi  
Högskolan i Halmstad  
17 december 2025

---

# Proceduren vid hypotestest

## Test av fördelning (kvalitativt test)

### 1 Hypotes

$$
H_0 : F = F_0
$$

$$
H_1 : F \ne F_0
$$

---

### 2 Signifikansnivå

$$
\alpha
$$

---

### 3 Stickprov

$$
x_1,x_2,\dots,x_N
$$

där

$$
X \in F
$$

---

### 4 Klassindelning

$$
(I_1,I_2,\dots,I_K)
$$

med frekvenstabell

$$
(O_1,O_2,\dots,O_K)
$$

---

### 5 Testfunktion

$$
U=
\sum_{k=1}^{K}
\frac{(E_k-O_k)^2}{E_k}
$$

---

där

$$
E_k = E(\#I_k \mid H_0)
$$

---

och

$$
E_k = N P(X \in I_k \mid H_0)
$$

---

Under $H_0$

$$
U \in \chi^2_{K-1}
$$

---

### 6 Villkor

$$
A_\alpha = \{u > \chi^2_{\alpha,K-1}\}
$$

---

### 7 Beslut

Förkasta om

$$
A_\alpha
$$

annars inte.

---

### 8 p-värde

$$
p=\alpha
$$

så att

$$
\chi^2_{\alpha,K-1}=u
$$

---

# Exempel: Brottsutredningarna

Tiden för brottsutredning varierar mellan olika polisdistrikt.

Vid polisstationen i Grönköping har den genomsnittliga utredningstiden $\bar{x}$ beräknats baserat på 100 fall.

---

Fråga:

Kan man med **1% felmarginal** säga att utredningstiden för ett ännu ej observerat fall **inte är normalfördelad**?

---

## Observerade tider

```
3.7 7.5 7.7 5.0 9.8 12.8 11.2 7.0 8.8 8.8
4.8 11.4 10.2 11.4 16.0 8.8 10.4 7.3 11.6 9.2
8.3 11.5 8.8 6.3 5.3 8.6 9.0 8.9 11.7 6.4
3.9 13.5 11.1 11.3 7.8 12.6 8.1 11.6 7.1 15.1
13.5 7.0 7.6 10.3 8.7 11.6 9.2 7.1 10.6 8.7
8.3 3.8 6.8 7.0 5.6 4.4 7.1 6.8 5.1 7.6
15.2 6.7 9.9 7.6 7.3 10.2 4.0 9.3 6.6 8.6
7.9 8.6 10.9 7.4 8.7 12.8 6.3 8.5 8.8 6.6
17.3 8.3 7.6 9.2 8.5 7.1 15.3 10.6 15.6 17.4
13.9 7.8 11.6 5.1 8.8 3.9 8.7 10.6 6.7 7.9
```

---

# Lösning

Stickprovsstatistik

$$
\bar{x}=9
$$

$$
s^2=9
$$

---

Test

$$
H_0: X \in N(9,9)
$$

$$
H_1: X \notin N(9,9)
$$

---

## Klassindelning

$$
(-\infty,5),\;
[5,7),\;
[7,9),\;
[9,11),\;
[11,13),\;
[13,15),\;
[15,\infty)
$$

---

## Observerade frekvenser

$$
(O_1,O_2,\dots,O_7)
$$

```
6, 22, 28, 15, 15, 6, 8
```

---

## Förväntade frekvenser

$$
E_k = N P(X\in I_k|H_0)
$$

```
9.18, 16.13, 24.75, 24.75, 16.13, 6.85, 2.28
```

---

# Teststatistika

$$
u=
\frac{(6-9.18)^2}{9.18}
+
\frac{(22-16.13)^2}{16.13}
+
\frac{(28-24.75)^2}{24.75}
+
\frac{(15-24.75)^2}{24.75}
+
\frac{(15-16.13)^2}{16.13}
+
\frac{(6-6.85)^2}{6.85}
+
\frac{(8-2.28)^2}{2.28}
$$

---

Resultat

$$
u=22.0061
$$

---

## Kritiskt värde

$$
\chi^2_{0.01,6}=16.8119
$$

---

Eftersom

$$
22.0061 > 16.8119
$$

förkastas $H_0$.

---

# Slutsats

Utredningstiden **är inte normalfördelad**.
