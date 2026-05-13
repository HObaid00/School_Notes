## Definition
När man inte längre  kan räkna upp de till något tal eller talen inte längre enbart är heltal, då duger inte längre diskreta fördelningar -> Kontinuerliga fördelning
* Typiskt integrera istället för summera
* Nu är alltid $$\Large P(X=x)=0$$ för alla $$\Large X \in S$$ s.f. ej meningsfull.
- Täthetsfunktion:
$$\Large 
f(x) = \frac{d}{dx} P(X ≤ x)
\iff
P(a \leq X \leq b) = \int_a^b f(x)dx
$$ om $$ \Large (a, b) \in S \quad P(a \leq X \leq b) = \int_{(a,b)\cap S} f(x) dx$$ mer allmänt.

## Skillnaden

### Diskret
$$\Large
\begin{array}s
P(X=x) > 0 \quad \text{för alla } x \in S \\
P(X \leq x) \not= P(X < x) \\
p(x) = P(X = x) \quad \text{(s.f.)}
\end{array}
$$
### Kontinuerlig
$$\Large
\begin{array}s
P(X = x) = 0 \quad \text{för alla } x \in S \\
P(X \leq x) = P(X < x) \\
f(x) = \frac{d}{dx} P(X \leq x) \quad \text{(t.f.)}
\end{array}
$$

## Täthetsfunktion
T.f. kan vara vilken funktion f som helst som uppfyller vilkoren
$$\Large
f(x) \geq 0 \text{ för alla } x \in S \text{ och } \int_\mathbb{R} f(x) dx = 1
$$

## Vanligast är dock
* (Kontinuerlig) [[Uniform dsitribution]]
* [[Exponentialfördelning]]
* [[Normalfördelning]]
* [[Weibullfördelning]]
* [[Gammafördelning]]
* ([[t-fördelning]])
* ([[Chi2-fördelning]])