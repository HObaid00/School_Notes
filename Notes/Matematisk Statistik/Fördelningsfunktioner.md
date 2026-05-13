## Definition
Funktionen
$$\Large
F(x) = P(X \leq x) 
$$
kallas X **fördelningsfunktion** (gäller både diskreta  och kontinuerliga variabler!)

## Samband med Sannolikhets funktion / Täthets funktion
### Diskret Variabel X
$$\Large
F(x) = \sum_{k=-\infty}^x p(k)
$$
## Kontinuerlig Variabel X
$$\Large
F(x) = \int_{k=-\infty}^x f(t)dt
$$
## Vilkor
Funktionen *F* kan vara vilken funktion som helst som uppfyller vilkoren:
1. $$\Large \lim_{x \rightarrow -\infty} F(x)=0$$
2. $$\Large \lim_{x \rightarrow \infty} F(x)=1$$
3. Högerkontinuerlig (càdlàg) för alla $$\Large x \in S$$
4. $$\Large F(x) \text{ växande på } S$$
## För alla
$$\Large
a, b \in \mathbb{R} : a < b \text{ är } P(a < X \le b) = F(b) - F(a)
$$

## Kvantil Definition
$$\Large
\alpha\text{-kvantil (100}\alpha \text{ är det tal }x_\alpha \text{ sådant att }F(x_\alpha) = 1 - \alpha
$$
