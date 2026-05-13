# Matematisk statistik

**Eric Järpe**  
**F 9: Beskrivande statistik**  
ITE, Högskolan i Halmstad  
3 november 2025

---

---

## Statistik

- Statistisk undersökning avser en ändlig eller oändlig population (målgrupp).
- Populationen är en mängd bestående av individer.
- Man gör observationer, dvs realiserar slumpmässiga värden av elementen.
- Exempel på datainsamling:
  - mäter
  - räknar
  - laddar ned från internet
- **Totalundersökning**: mindre behov av statistik.
- **Stickprovsundersökning**: vanligast.

### Typer av undersökningar

- **Jämförande undersökning**
  - t.ex. “A bättre än B”
  - kartlägga beroenden
  - troligaste historiken/utvecklingen
  - typiskt multivariat
- **Icke-jämförande undersökning**
  - skatta en parameter
  - testa mot konstant nivå
  - typiskt en-sampel-analys

### Exempel

Antag att man vill jämföra produktegenskaper som exekveringstid, hastighet eller kapacitet, och bevisa att $\mu_1 < \mu_2$, $\mu_1 > \mu_2$ eller $\mu_1 \neq \mu_2$.

Eller förändring av en sannolikhet, t.ex. opinionsundersökning, och bevisa att $p_1 < p_2$, $p_1 > p_2$ eller $p_1 \neq p_2$.

Eller kolla ett antagande om fördelning eller oberoende, t.ex. inte bevisa att $F \neq F_0$ eller $X \not\perp Y$.

#### Exempel 1
Den nya molntjänsten Hepp överför stora filer. Den ska benchmarkas mot Sprend. Man tar reda på upp- och nedladdningstider för Sprend, $X$, och för Hepp, $Y$. Man vill pröva hypotesen $\mu_{\text{Upp-Sprend}} > \mu_{\text{Upp-Hepp}}$ respektive $\mu_{\text{Ned-Sprend}} > \mu_{\text{Ned-Hepp}}$.

#### Exempel 2
Vid regressionsanalys är en förutsättning att vissa variabler är normalfördelade. Man vill granska detta genom att pröva hypotesen $F \neq N$.

---

## Definition av stickprov

Ett stickprov på variabeln $X$ är oberoende variabler $X_1, X_2, \dots, X_n$ med samma fördelning som $X$.

- $x = (x_1, x_2, \dots, x_n)$ är observerat stickprov.
- $X = (X_1, X_2, \dots, X_n)$ är stokastiskt stickprov.

### Viktiga begrepp

- **punktskattning** – skatta värdet av en parameter
- **intervallskattning** – bilda ett intervall som innehåller parametern med given säkerhet
- **hypotestest** – försök bevisa ett påstående om en parameter
- **regressionsanalys**
- **change-point detection**
- **överlevnadsanalys**

---

## Datatyper

### Slumpvariabel

#### Kvalitativ
- **Nominalskala** (kategorisk)  
  Exempel: ögonfärg
- **Ordinalskala** (ordning)  
  Exempel: betyg

#### Kvantitativ (numerisk)
- **Intervallskala** (ordning + differens)  
  Exempel: temperatur i $^\circ\text{C}$
- **Kvotskala** (ordning + intervall + nollpunkt)  
  Exempel: tid, vikt, antal individer

### Exempel

1. Variabeln längd som amatörlängdhopparen Skuttvard hoppar noteras till  
   a) $3.1207\ldots, 3.0819\ldots, 3.1332\ldots, 2.8877\ldots$ – kontinuerliga kvotdata  
   b) $3.12, 3.08, 3.13, 2.89$ – diskreta eller kontinuerliga kvotdata

2. En tillverkare av kretskort väljer slumpmässigt DDR4-komponenter från Mouser Electronics, Corsair, Kingston, Crucial Pro eller Samsung. Variabeln DDR4-tillverkare har **nominalskala**.

3. På gymnasiet betygssätts ämnen med A, B, C, D, E, F. Ett slumpmässigt valt betyg är **ordinaldata**.

4. Temperaturen som mäts i grader Celsius är **intervallskala**.

### Kommentarer

- Majoriteten av metoder för beslutsteori behandlar kvotdata.
- Ofta är de även möjliga att tillämpa på intervalldata.
- Den del av statistiken som handlar om nominal- och ordinaldata kallas **icke-parametriska metoder**.

---

## Deskriptiv statistik

- Att bara presentera observationerna kan bli rörigt och oöverskådligt.
- Man kan sammanfatta genom att beräkna skattningar, t.ex. medelvärden.
- Man kan gruppera data och beräkna frekvenser.
- Man kan visa plottar:
  - stolpdiagram
  - cirkeldiagram
  - histogram
  - boxplot
  - flödesscheman

---

## Lägesmått

Antag att man observerat stickprovet $x_1, x_2, \dots, x_n$.

Det observerade värderummet blir $x_{[1]}, x_{[2]}, \dots, x_{[m]}$ och frekvenserna $f_1, f_2, \dots, f_m$, där

$$\Large f_j = \#\{i : x_i = x_{[j]}\}$$

### Medelvärde

$$\Large \bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i = \frac{1}{n}\sum_{j=1}^{m} x_{[j]} f_j$$

### Typvärde

$$\Large m_T = x_{i^*} : i^* = \arg\max_i f_i$$

den mest frekventa observationen.

### Exempel

På gymnasiet betygssätts ämnen med A, B, C, D, E, F.

För 10 elever observeras provräkningsresultaten:

$14, 11, 7, 5, 11, 2, 10, 5, 11, 6$

Dessa ger betygen:

$A, B, D, E, B, F, B, F, B, E$

#### Lösning

a) Medelvärdespoängen:

$$\Large \bar{x} = \frac{1}{10}(14 + 11 + 7 + 5 + 11 + 2 + 10 + 5 + 11 + 6) = 8.2$$

b) Typvärdet av betyget:

$$\Large x_T = \arg\max(A:1,\; B:4,\; C:0,\; D:1,\; E:2,\; F:2) = B$$

---

## Median och kvartiler

Antag att det sorterade stickprovet är $x_{(1)}, x_{(2)}, \dots, x_{(n)}$.

### Median

$$\Large \mathrm{md}_X =
\begin{cases}
x_{\left(\frac{n+1}{2}\right)}, & \text{om } n \text{ är udda} \\
\frac{1}{2}\left(x_{\left(\frac{n}{2}\right)} + x_{\left(\frac{n}{2}+1\right)}\right), & \text{om } n \text{ är jämnt}
\end{cases}$$

### Första kvartilen

$$\Large Q_1 =
\begin{cases}
\frac{1}{2}\left(x_{\left(\frac{n}{4}\right)} + x_{\left(\frac{n}{4}+1\right)}\right), & \text{om } n \text{ är delbart med } 4 \\[6pt]
\frac{1}{4}\left(3x_{\left(\frac{n+1}{4}\right)} + x_{\left(\frac{n+1}{4}+1\right)}\right), & \text{om } n+1 \text{ är delbart med } 4 \\[6pt]
x_{\left(\frac{n+2}{4}\right)}, & \text{om } n+2 \text{ är delbart med } 4 \\[6pt]
\frac{1}{4}\left(x_{\left(\frac{n+3}{4}-1\right)} + 3x_{\left(\frac{n+3}{4}\right)}\right), & \text{om } n+3 \text{ är delbart med } 4
\end{cases}$$

### Tredje kvartilen

$$\Large Q_3 =
\begin{cases}

\frac{1}{2} 
\left( x_{\left( \frac{3n}{4}\right)} + 
x_{\left(\frac{3n}{4}+1\right)}\right), 
& \text{om } n \text{ är delbart med } 4 \\[6pt]

\frac{1}{4}
\left(x_{\left(\frac{3(n+1)}{4} -1 \right) } + 
3x_{\left(\frac{3(n+1)}{4}+1\right)}\right), 
& \text{om } n+1 \text{ är delbart med } 4 \\[6pt]

x_{\left(\frac{3(n+2)}{4}-1\right)}, & \text{om } n+2 \text{ är delbart med } 4 \\[6pt]

\frac{1}{4}\left(3x_{\left(\frac{3(n+3)}{4}-2\right)} + x_{\left(\frac{3(n+3)}{4}-1\right)}\right), & \text{om } n+3 \text{ är delbart med } 4

\end{cases}
$$

---

## Spridningsmått

Antag att man observerat stickprovet $x_1, x_2, \dots, x_n$ och motsvarande parade stickprov $y_1, y_2, \dots, y_n$.

### Stickprovsvarians

$$\Large s_X^2 = \frac{1}{n-1}\left(\sum_{i=1}^{n} x_i^2 - n\bar{x}^2\right)$$

### Stickprovsstandardavvikelse

$$\Large s_X = \sqrt{s_X^2}$$

### Medelkvadratfel

$$\Large \mathrm{MSE} = \frac{s_X^2}{n}$$

### Variationsbredd

$$\Large R_X = x_{(n)} - x_{(1)}$$

### Kvartilavstånd

$$\Large Q = Q_3 - Q_1$$

### Observation

- $s_X \approx \frac{2}{3}Q$
- om $n \geq 100$ så är $s_X \approx \frac{1}{3}R$

---

## Beroendemått

Antag att man observerat stickprovet $x_1, x_2, \dots, x_n$ och motsvarande parade stickprovet $y_1, y_2, \dots, y_n$.

### Stickprovskovarians

$$\Large c_{XY} = \frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})$$

### Stickprovskorrelation

$$\Large r_{XY} = \frac{\sum_{i=1}^{n} x_i y_i - n\bar{x}\bar{y}}{s_X s_Y}$$

### Observation

$$\Large c_{XY} = \frac{1}{n-1}\left(\sum_{i=1}^{n} x_i y_i - n\bar{x}\bar{y}\right)$$

---

## Deskriptiv statistik – histogram

- Dela in utfallsrummet i delintervall $I_1, I_2, \dots, I_k$
- **Frekvenser**: antal observationer inom respektive delintervall $f_1, f_2, \dots, f_k$
- **Relativa frekvenser**: andelen observationer i delintervall är $r_1, r_2, \dots, r_k$, där

$$\Large r_i = \frac{f_i}{N}$$

där $N$ är totala antalet observationer.

### Frekvenstabell

| Delintervall | 1 | 2 | $\dots$ | $k$ |
|---|---:|---:|---:|---:|
| Frekvens | $f_1$ | $f_2$ | $\dots$ | $f_k$ |
| Relativa frekvenser | $r_1$ | $r_2$ | $\dots$ | $r_k$ |

### Histogram

Histogrammet är plotten av frekvenserna eller de relativa frekvenserna.
![[Pasted image 20260423194644.png|697]]

---

## Boxplot

- Diagram med median, kvartiler och outliers för jämförelse.

### Procedur

1. Gör $n \geq 5$ observationer $(x_1, x_2, \dots, x_n)$
2. Sortera observationerna
3. Beräkna medianen $\mathrm{md}$
4. Beräkna första kvartilen $Q_1$
5. Beräkna tredje kvartilen $Q_3$
6. Beräkna outliers

Alla $x$ så att

$$\Large x - Q_3 > 1.5(Q_3 - Q_1)$$

eller

$$\Large Q_1 - x > 1.5(Q_3 - Q_1)$$

kallas outliers.

Alla andra observationer kallas inliers.

7. Rita boxplotten
   - rektangel med kortsidorna i $Q_1$ och $Q_3$
   - mittstreck i $\mathrm{md}$
   - morrhår i $W_1 = \min(\text{inliers})$ och $W_3 = \max(\text{inliers})$
   - små cirklar för outliers

---

## Exempel: två datornätverk

Två likstora datornätverk har olika skydd mot intrång: A och B.

De har registrerat hur många intrång som registreras under 18 månader:

- $A$: 43, 5, 20, 23, 19, 23, 17, 26, 22, 2, 19, 21, 27, 20, 37, 19, 18, 21
- $B$: 67, 39, 55, 51, 30, 41, 97, 7, 49, 58, 63, 63, 53, 4, 81, 61, 52, 47

Man ska:

a. beräkna frekvenstabeller  
b. skatta fördelningen för intrångsförsök  
c. skatta väntevärden  
d. skatta varianser och standardavvikelser  
e. beräkna medelkvadratfel  
f. beräkna medianer  
g. beräkna typvärden  
h. beräkna variationsbredder och jämföra grov- med finskattning av $\sigma$  
i. beräkna kvartiler, morrhår, inliers, outliers och göra boxplot  
j. skatta kovarians och korrelation

---

## Lösning a: frekvenstabeller

| Antal intrång | A: antal obs | A: % | B: antal obs | B: % |
|---|---:|---:|---:|---:|
| 0–10 | 2 | 11 | 2 | 11 |
| 11–20 | 7 | 39 | 0 | 0 |
| 21–30 | 7 | 39 | 1 | 6 |
| 31–40 | 1 | 6 | 1 | 6 |
| 41–50 | 1 | 6 | 3 | 17 |
| 51–60 | 0 | 0 | 5 | 28 |
| 61–70 | 0 | 0 | 4 | 22 |
| 71–80 | 0 | 0 | 0 | 0 |
| 81–90 | 0 | 0 | 1 | 6 |
| 91–100 | 0 | 0 | 1 | 6 |

---

## Lösning b: skatta fördelningen

Samma frekvenstabell används för att uppskatta fördelningen för intrångsförsök i nätverk A respektive B.

---

## Lösning c: medelvärden

$$\Large \bar{x} = \frac{1}{18}\sum_{i=1}^{18} x_i = \frac{382}{18} = 21.2222$$

$$\Large \bar{y} = \frac{1}{18}\sum_{i=1}^{18} y_i = \frac{918}{18} = 51$$

---

## Lösning d: varianser och standardavvikelser

$$\Large s_A^2 = \frac{1}{18-1}\left(\sum_{i=1}^{18} x_i^2 - 18\bar{x}^2\right)
= \frac{1}{17}\left(9572 - 18(21.2222\ldots)^2\right) = 86.1830$$

$$\Large s_A = \sqrt{86.1830\ldots} = 9.2835$$

$$\Large s_B^2 = \frac{1}{18-1}\left(\sum_{i=1}^{18} y_i^2 - 18\bar{y}^2\right)
= \frac{1}{17}(55398 - 18 \cdot 51^2) = 504.7059$$

$$\Large s_B = \sqrt{504.7059\ldots} = 22.4657$$

---

## Lösning e: medelkvadratfel

$$\Large \mathrm{MSE}_A = \frac{s_X^2}{n} = \frac{86.1830\ldots}{18} = 4.7879$$

$$\Large \mathrm{MSE}_B = \frac{s_Y^2}{n} = \frac{504.7059\ldots}{18} = 28.0392$$

---

## Lösning f: medianer

Sorterade data:

- $\text{Sort}(A)$: 2, 5, 17, 18, 19, 19, 19, 20, 20, 21, 21, 22, 23, 23, 26, 27, 37, 43
- $\text{Sort}(B)$: 4, 7, 30, 39, 41, 47, 49, 51, 52, 53, 55, 58, 61, 63, 63, 67, 81, 97

Medianerna blir:

$$\Large \mathrm{md}_A = \frac{x_{(9)} + x_{(10)}}{2} = \frac{20 + 21}{2} = 20.5$$

$$\Large \mathrm{md}_B = \frac{y_{(9)} + y_{(10)}}{2} = \frac{52 + 53}{2} = 52.5$$

---

## Lösning g: typvärden

- $t_A = 19$
- $t_B = 63$

---

## Lösning h: variationsbredder

$$\Large R_A = x_{(18)} - x_{(1)} = 43 - 2 = 41$$

Det ger

$$\Large \frac{41}{3} = 14.33$$

att jämföras med $s_A = 9.2835$, vilket är en kraftig överskattning eftersom $n = 18 < 100$.

$$\Large R_B = y_{(18)} - y_{(1)} = 97 - 4 = 93$$

Det ger

$$\Large \frac{93}{3} = 31$$

att jämföras med $s_B = 22.4657$.

---

## Lösning i: kvartiler, morrhår, inliers, outliers och boxplot

### För A

$$\Large \mathrm{md}_A = 20.5$$

$$\Large Q_{A,1} = x_{\left(\frac{18+2}{4}\right)} = 19$$

$$\Large Q_{A,3} = x_{\left(\frac{3(18+2)}{4} - 1\right)} = 23$$

Kvartilavstånd:

$$\Large Q = Q_{A,3} - Q_{A,1} = 23 - 19 = 4$$

Outliergräns:

$$\Large 1.5Q = 6$$

Övre outliers:
- $43 - 23 = 20 > 6$
- $37 - 23 = 14 > 6$

Nedre outliers:
- $19 - 2 = 17 > 6$
- $19 - 5 = 14 > 6$

Alltså:

- $W_{A,1} = 17$
- $W_{A,3} = 27$
- Outliers: 2, 5, 37, 43

### För B

$$\Large \mathrm{md}_B = 52.5$$

$$\Large Q_{B,1} = y_{\left(\frac{18+2}{4}\right)} = 41$$

$$\Large Q_{B,3} = y_{\left(\frac{3(18+2)}{4} - 1\right)} = 63$$

Kvartilavstånd:

$$\Large Q = 63 - 41 = 22$$

Outliergräns:

$$\Large 1.5Q = 33$$

Övre outliers:
- $97 - 63 = 34 > 33$

Nedre outliers:
- $41 - 4 = 37 > 33$
- $41 - 7 = 34 > 33$

Alltså:

- $W_{B,1} = 30$
- $W_{B,3} = 81$
- Outliers: 4, 7, 97

### Svar

Ja, medianantalet intrång är större hos B än hos A.

---

## Lösning j: kovarians och korrelation

$$\Large c_{XY} = \frac{1}{18-1}\left(\sum_{i=1}^{18} x_i y_i - 18\bar{x}\bar{y}\right)
= \frac{1}{17}\left(19997 - 18 \cdot 21.2222\ldots \cdot 22.4656\ldots\right)
= \frac{515}{17} = 30.2941$$

$$\Large r_{XY} = \frac{c_{XY}}{s_X s_Y}
= \frac{30.2941\ldots}{9.2834\ldots \cdot 22.4656\ldots}
= 0.1453$$

**OBS:** Förutsätter parat stickprov.