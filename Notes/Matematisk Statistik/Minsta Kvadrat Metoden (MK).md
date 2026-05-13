---
aliases:
  - Least Square Error (LSE)
---

Används för att hitta den **bästa anpassade linjen eller funktionen** till data genom att minimera summan  av kvadratfel

Minimera:
$$\Large
Q(θ) = \arg\min_{\theta} Σ (x_i − μ(θ))² $$
## Steg för att hitta MK

1. Modellera Problemet: $$\Large (x_1, \ y_1), (x_2, \ y_2), \dots,(x_n, \ y_n) \Rightarrow \ y = ax+b$$
2. Definera felet (residualer): $$\Large e_i = y_i - (ax_i + b)$$
3. Kvadrera felen: $$\Large e_i^2 = (y_i - (ax_i + b))^2$$
4. Skapa målfunktionen (summera av kvadraterna): $$\Large S(a, b) = \sum_{i=1}^n (y_i - (ax_i + b))^2$$
5. Derivera med avseende på parametrarna: 
$$\Large \frac{\partial S}{\partial a} = 0, \quad\frac{\partial S}{\partial b} = 0$$
6. Lös normalekvationerna: $$\Large \begin{array}a \sum x_i y_i = a \sum x_i^2 + b \sum x_i \\ \sum y_i = a \sum x_i + nb \end{array}$$
7. Lös ut $a$ och $b$: $$

$$
1. Tolkning 
	* $a$: lutning (hur snabbt y förändras)
	* $b$: skärning med y-axeln
	* Linjen $y = ax +b$ är den som **minimerar kvadrerade fel**

# Länkar
[[Matematisk Statistik]]