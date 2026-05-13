## Tolkning
### Exempel - Regn: 
Låt

- $A = \{\text{det regnar}\}$
- $B = \{\text{temperaturen är } > 15^\circ\}$

$$\Large
A \cap B = \text{ det regnar och temperaturen är } > 15^\circ.
$$


$$ \Large
A \cup B^* = \text{ det regnar eller temperaturen är } \le 15^\circ.

$$

### Exempel – Banksy

Banksy är en berömd men anonym graffitikonstnär.

Låt

- $B_1 = \{\text{Banksy är i Halmstad}\}$
- $B_2 = \{\text{Banksy är i Göteborg}\}$
- $B_3 = \{\text{Banksy är i Bristol}\}$

Utfallsrum:
$$\Large
\Omega = \{\text{Banksy är någonstans}\}
$$


En **partition** är en uppdelning av $\Omega$ i disjunkta delmängder.

$$\Large
\begin{array}
B_1 \cap B_2 = \emptyset\\


B_1 \cap B_3 = \emptyset \\

B_2 \cap B_3 = \emptyset
\end{array}
$$
Men

$$\Large
B_1 \cup B_2 \cup B_3 \ne \Omega
$$

Partition:

$$\Large
\{B_1, B_2, B_3, (B_1 \cup B_2 \cup B_3)^*\}
$$


## Definition
En sannolikhetsmått $P(\cdot)$ är definerat av att
1. för varje $$\Large A \subseteq \Omega$$ är $$\Large 0 \leq P(A) \leq 1$$
2. $$\Large P(\Omega)=1$$
3. Om $$\Large A_1, \ A_2, \dots$$ disjunkta så $$\Large P(A_1 \ \cup \ A_2 \ \cup \dots) = P(A_1)+P(A_2)+\dots$$
## Satser
### I 
$$\Large
P(A^*) = P(\Omega) - P(A) = 1 - P(A)
$$
### II
$$ \Large
P(A \cup B) =
P(A) + P(B) - P(A \cap B)
$$
## Likformigt Sannolikhetsmåt
Då P är ett **likformigt** sannolikhetsmåt på ett ändligt utfallsrum $\Omega$ med $$ \Large |\Omega| = n$$ om $$\Large P(\omega_i) = \frac{1}{n}$$ för varje $$\Large i = 1, \ 2, \dots, \ n.$$
## Kombinatorik
### Fakultet
$$\Large
n! = 1\cdot2\cdot\dots \cdot n
$$
med
$$\Large
0! = 1
$$
### Binomialkoefficient
Utan återläggning:
$$\Large
\binom{n}{k} = \frac{n!}{k!(n-k)!}
$$
Med återlägning
$$\Large
n^k = n_1\cdot n_2\cdot \dots \cdot n_k \quad \text{ k times}
$$

## Dragning av kulor
Antag 
* $v$ vita
* $s$ svarta
drar $n$ stycken

### Utan återläggning
$$\Large
P(\text{k vita}) =
\frac{\binom{v}{k}\binom{s}{n-k}}{\binom{v+s}{n}}
$$
### Med återläggning
$$\Large

P(\text{k vita}) =
\binom{n}{k}
\frac{v^k s^{n-k}}{(v+s)^n}
$$
## Binomialsatsen
$$\Large
(x+y)^n =
\sum_{k=0}^{n}
\binom{n}{k}
x^k y^{n-k}
$$