# Varför statistik?

- Förkunskap för att förstå publicerade studier
- resultatrapportering
- underlag till beslutsfattare
- speciella krav för vissa yrken

Närmaste tillämpning: **exjobbet**.

---

## Statistisk undersökning

En statistisk undersökning består av

1. Planering  
2. Datainsamling  
3. Bearbetning  
4. Presentation  

---

För att kunna hävda att något är

- bättre
- snabbare
- signifikant

måste man skilja **verkliga egenskaper** från **slumpmässig variation**.

---

# Statistik

Statistisk undersökning avser en **population**.

Population = mängd av individer.

Observationer = realisationer av slumpvariabler.

---

## Typer av undersökningar

### Totalundersökning
Studerar hela populationen.

### Stickprovsundersökning
Vanligast.

---

### Jämförande undersökning

Exempel:

- visa att

$$\Large
\mu_1 < \mu_2
$$

eller

$$\Large
p_1 > p_2
$$

---

### Icke-jämförande undersökning

Exempel:

- skatta en parameter
- testa mot en konstant nivå

---

# Exempel

Molntjänster:

- **Sprend**
- **Hepp**

Mät

- uppladdningstid
- nedladdningstid

---

Hypotes

$$\Large
\mu_{\text{Upp-Sprend}} > \mu_{\text{Upp-Hepp}}
$$

och

$$\Large
\mu_{\text{Ned-Sprend}} > \mu_{\text{Ned-Hepp}}
$$

---


# Deskriptiv statistik

Observationer kan sammanfattas med

- skattningar
- frekvenstabeller
- diagram

---

Exempel på diagram

- stolpdiagram
- cirkeldiagram
- histogram
- boxplot

---

# Lägesmått

Antag stickprovet

$$\Large
x_1,x_2,\dots,x_n
$$

---

## Medelvärde

$$\Large
\bar{x} =
\frac{1}{n}\sum_{i=1}^{n} x_i
$$

---

Alternativt

$$\Large
\bar{x}=
\frac{1}{n}\sum_{j=1}^{m} x_{[j]}f_j
$$

---

## Typvärde

$$\Large
m_T = x_{i^*}
$$

där

$$\Large
i^*=\arg\max_i f_i
$$

---

# Exempel

Poäng:

```
14, 11, 7, 5, 11, 2, 10, 5, 11, 6
```

---

## Medelvärde

$$\Large
\bar{x}
=
\frac{1}{10}(14+11+7+5+11+2+10+5+11+6)
= 8.2$$
---

## Typvärde

Frekvenser

- A:1
- B:4
- C:0
- D:1
- E:2
- F:2

---

Typvärde

$$\Large
x_T=B
$$

---

# Median

Sorterat stickprov

$$\Large
x_{(1)},x_{(2)},\dots,x_{(n)}
$$

---

Median

$$\Large
md_X=
\begin{cases}
x_{(n+1)/2}, & n \text{ udda} \\
\frac{1}{2}(x_{(n/2)}+x_{(n/2+1)}), & n \text{ jämnt}
\end{cases}
$$

---

# Kvartiler

Första kvartilen $Q_1$

$$\Large
Q_1 = 
\begin{cases}
\frac{1}{2}(X_{(\frac{n}{4})}+X_{(\frac{n}{4}+1)}), & \text{ om n är delbart med 4} \\

\frac{1}{4}(3X_{(\frac{n+1}{4})}+X_{(\frac{n+1}{4}+1)}), & \text{ om n+1 är delbart med 4} \\

X_{\frac{n+2}{4}}, & \text{om n+2 är delbart med 3} \\

\frac{1}{4}(X_{(\frac{n+3}{4})-1}+3X_{(\frac{n+3}{4})}), & \text{ om n+3 är delbart med 4}

\end{cases}
$$

Tredje kvartilen $Q_3$

$$\Large
Q_3 = 
\begin{cases}
\frac{1}{2}(X_{(\frac{3n}{4})} + X_{(\frac{3n}{4}+1)}), & \text{ om n är delbart med 4} \\

\frac{1}{4}(X_{(\frac{3(n+1)}{4} - 1)} + 3X_{(\frac{3(n+1)}{4})}), & \text{ om n+1 är delbart med 4} \\

X_{\frac{n+2}{4} - 1}, & \text{om n+2 är delbart med 4} \\

\frac{1}{4}(3X_{(\frac{3(n+3)}{4}) - 2} + X_{(\frac{n+3}{4}-1)}), & \text{ om n+3 är delbart med 4}

\end{cases}
$$

(detaljerade formler beroende på $n$).

---

# Spridningsmått

## Stickprovsvarians

$$\Large
s_X^2
=
\frac{1}{n-1}
\left(
\sum_{i=1}^{n} x_i^2
-
n\bar{x}^2
\right)
$$

---

## Standardavvikelse

$$\Large
s_X=\sqrt{s_X^2}
$$

---

## Medelkvadratfel

$$\Large
\frac{s_X^2}{n}
$$

---

## Variationsbredd

$$\Large
R_X=x_{(n)}-x_{(1)}
$$

---

## Kvartilavstånd

$$\Large
Q=Q_3-Q_1
$$

---

Approximation

$$
s_X \approx \frac{2}{3}Q
$$

och om

$$
n\ge100
$$

$$
s_X \approx \frac{R}{3}
$$

---

# Beroendemått

## Stickprovskovarians

$$
c_{XY}
=
\frac{1}{n-1}
\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})
$$

---

Alternativ form

$$
c_{XY}
=
\frac{1}{n-1}
\left(
\sum x_i y_i
-
n\bar{x}\bar{y}
\right)
$$

---

## Stickprovskorrelation

$$
r_{XY}
=
\frac{\sum x_i y_i - n\bar{x}\bar{y}}
{s_X s_Y}
$$

---

# Histogram

1. Dela in utfallsrummet i intervall

$$
I_1,I_2,\dots,I_k
$$

---

2. Beräkna frekvenser

$$
f_1,f_2,\dots,f_k
$$

---

3. Relativa frekvenser

$$
r_i=\frac{f_i}{N}
$$

![[Pasted image 20260306142026.png]]

---

# Boxplot

Diagram som visar

- median
- kvartiler
- outliers

---

## Procedur

1. Samla observationer
2. Sortera
3. Beräkna median
4. Beräkna $Q_1$
5. Beräkna $Q_3$

---

## Outliers

Observationer där

$$
x-Q_3 > 1.5(Q_3-Q_1)
$$

eller

$$
Q_1-x > 1.5(Q_3-Q_1)
$$

---

# Exempel

Intrång i två nätverk:

```
A : 43,5,20,23,19,23,17,26,22,2,19,21,27,20,37,19,18,21
B : 67,39,55,51,30,41,97,7,49,58,63,63,53,4,81,61,52,47
```

---

## Medelvärden

$$
\bar{x}=21.2222
$$

$$
\bar{y}=51
$$

---

## Varians

$$
s_A^2=86.1830
$$

$$
s_B^2=504.7059
$$

---

## Standardavvikelser

$$
s_A=9.2835
$$

$$
s_B=22.4657
$$

---

## Medianer

$$
md_A=20.5
$$

$$
md_B=52.5
$$

---

## Typvärden

$$
t_A=19
$$

$$
t_B=63
$$

---

## Variationsbredd

$$
R_A=41
$$

$$
R_B=93
$$

---

## Kvartiler

A:

$$
Q_1=19,\quad Q_3=23
$$

B:

$$
Q_1=41,\quad Q_3=63
$$

---

## Outliers

A:

```
2, 5, 37, 43
```

B:

```
4, 7, 97
```

![[Pasted image 20260306142113.png]]

---

## Slutsats

Medianen för intrång är större i nätverk **B** än i **A**.

---

# Kovarians och korrelation

## Kovarians

$$
c_{XY}
=
30.2941
$$

---

## Korrelation

$$
r_{XY}
=
0.1453
$$
