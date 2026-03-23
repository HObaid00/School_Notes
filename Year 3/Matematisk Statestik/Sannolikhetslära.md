# Sannolikhetsteori

### Experiment

Fenomen eller förlopp som man vill beräkna sannolikheter för.

---

### Utfall

De olika möjliga resultaten

$$
\omega_1, \omega_2, ...
$$

---

### Utfallsrum

Mängden av alla utfall

$$
\Omega
$$

---

### Händelse

Union av vissa utfall

$$
A, B, ...
$$

---

![[Pasted image 20260305131143.png]]
- utfallsrummet $\Omega$
- mängderna $A$, $B$, $C$

---

### Diskret eller kontinuerligt utfallsrum

Om antal utfall är **uppräkneligt** → diskret utfallsrum.

Annars → kontinuerligt.

---

### Mängdoperationer

Union:

$$
A \cup B
$$

Snitt:

$$
A \cap B
$$

Komplement:

$$
A^*
$$

Differens:

$$
A \setminus B
$$

Notation:

- $\emptyset$ — tomma mängden
- $a \in A$ — tillhörighet
- $A \subseteq B$ — delmängd
- $|A|$ — antal element

---

# Mängdlära – Exempel

Låt

$$
A = \{1,2,3\}
$$

$$
B = \{3,4\}
$$

$$
\Omega = \{1,2,3,4,5\}
$$

Beräkna:

### Union

$$
A \cup B = \{1,2,3,4\}
$$

### Snitt

$$
A \cap B = \{3\}
$$

### Komplement

$$
A^* = \{4,5\}
$$

### Differens

$$
A \setminus B = \{1,2\}
$$

### Kardinalitet

$$
|A \cup B^*| = 4
$$

Frågor:

$$
A \subseteq B?
$$

Nej.

$$
5 \in A^* ?
$$

Ja.

---

# Mängdlära

### Beskrivande notation

$$
\{1,2,3\} = \{x : x \text{ är ett positivt heltal och } 1 \le x \le 3\}
$$

---

# Talmängder

- $\mathbb{Z}$ — heltalen
- $\mathbb{Z}^+$ — positiva heltal
- $\mathbb{N}$ — icke-negativa heltal
- $\mathbb{Q}$ — rationella tal
- $\mathbb{R}$ — reella tal
- $\mathbb{R}^+$ — positiva reella tal

---

# Intervallbeteckningar

$$
(a,b) = \{x \in \mathbb{R} : a < x < b\}
$$

$$
(a,b] = \{x \in \mathbb{R} : a < x \le b\}
$$

$$
[a,b) = \{x \in \mathbb{R} : a \le x < b\}
$$

$$
[a,b] = \{x \in \mathbb{R} : a \le x \le b\}
$$

$$
(a,\infty)
$$

$$
(-\infty,b]
$$

---

# Lite mer notation

### Summa

$$
a_1 + a_2 + ... + a_n =
\sum_{i=1}^{n} a_i
$$

---

### Produkt

$$
a_1 a_2 ... a_n =
\prod_{i=1}^{n} a_i
$$

---

### Union

$$
A_1 \cup A_2 \cup ... \cup A_n =
\bigcup_{i=1}^{n} A_i
$$

---

### Snitt

$$
A_1 \cap A_2 \cap ... \cap A_n =
\bigcap_{i=1}^{n} A_i
$$

---

### Disjunkta mängder

Om

$$
A \cap B = \emptyset
$$

så kallas mängderna **disjunkta**.

---

# De Morgans lagar

$$
(\bigcup_{i=1}^{n} A_i)^* =
\bigcap_{i=1}^{n} A_i^*
$$

$$
(\bigcap_{i=1}^{n} A_i)^* =
\bigcup_{i=1}^{n} A_i^*
$$

---

# Additionssatsen

$$
|A \cup B| = |A| + |B| - |A \cap B|
$$

---

# Komplementsatsen

$$
|A^*| = |\Omega| - |A|
$$

---

# Grundläggande sannolikhetslära

### Exempel

Låt

- $A = \{\text{det regnar}\}$
- $B = \{\text{temperaturen är } > 15^\circ\}$

---

### Tolkning

$$
A \cap B
$$

= det regnar **och** temperaturen är $> 15^\circ$.

---

$$
A \cup B^*
$$

= det regnar **eller** temperaturen är $\le 15^\circ$.

---

# Exempel – Banksy

Banksy är en berömd men anonym graffitikonstnär.

Låt

- $B_1 = \{\text{Banksy är i Halmstad}\}$
- $B_2 = \{\text{Banksy är i Göteborg}\}$
- $B_3 = \{\text{Banksy är i Bristol}\}$

---

Utfallsrum:

$$
\Omega = \{\text{Banksy är någonstans}\}
$$

---

En **partition** är en uppdelning av $\Omega$ i disjunkta delmängder.

$$
B_1 \cap B_2 = \emptyset
$$

$$
B_1 \cap B_3 = \emptyset
$$

$$
B_2 \cap B_3 = \emptyset
$$

Men

$$
B_1 \cup B_2 \cup B_3 \ne \Omega
$$

Partition:

$$
\{B_1, B_2, B_3, (B_1 \cup B_2 \cup B_3)^*\}
$$

---

# Definition

Ett sannolikhetsmått $P(\cdot)$ definieras av:

1.

$$
0 \le P(A) \le 1
$$

2.

$$
P(\Omega) = 1
$$

3.

Om $A_1, A_2, ...$ är disjunkta:

$$
P(A_1 \cup A_2 \cup ...) =
P(A_1) + P(A_2) + ...
$$

---

# Sats

$$
P(A^*) = 1 - P(A)
$$

---

# Sats

$$
P(A \cup B) =
P(A) + P(B) - P(A \cap B)
$$

---

# Exempel

Johannes åker ibland spontant till Gullevi för att spela fotboll.

Givet:

$$
P(\text{glömt bollen}) = 0.1
$$

$$
P(\text{planen upptagen}) = 0.3
$$

$$
P(\text{glömt bollen och planen upptagen}) = 0.05
$$

---

Låt

- $A = \{\text{glömt bollen}\}$
- $B = \{\text{planen upptagen}\}$

Vi vill veta

$$
P(A^* \cap B^*)
$$

---

Beräkning

$$
P(A^* \cap B^*) =
(1-P(A)) + (1-P(B)) - (1-P(A\cap B))
$$

$$
= 0.9 + 0.7 - 0.95 = 0.65
$$

---

# Likformigt sannolikhetsmått

Om utfallsrummet är ändligt med $|\Omega| = n$

$$
P(\omega_i) = \frac{1}{n}
$$

---

# Klassisk sannolikhetsdefinition

För händelsen $A$

$$
P(A) =
\frac{|A|}{|\Omega|}
$$

---

# Kombinatorik

### Fakultet

$$
n!
$$

med

$$
0! = 1
$$

---

### Binomialkoefficient

$$
\binom{n}{k}
$$

---

# Dragning av kulor

Antag

- $v$ vita
- $s$ svarta

drar $n$ stycken.

---

### Utan återläggning

$$
P(\text{k vita}) =
\frac{\binom{v}{k}\binom{s}{n-k}}{\binom{v+s}{n}}
$$

---

### Med återläggning

$$
P(\text{k vita}) =
\binom{n}{k}
\frac{v^k s^{n-k}}{(v+s)^n}
$$

---

# Binomialsatsen

$$
(x+y)^n =
\sum_{k=0}^{n}
\binom{n}{k}
x^k y^{n-k}
$$

---

# Exempel – Fembarnsfamilj

Antag

$$
P(\text{pojke}) = P(\text{flicka}) = 0.5
$$

Totalt:

$$
2^5 = 32
$$

---

### 1 pojke, 4 flickor

$$
\binom{5}{1} = 5
$$

$$
P = \frac{5}{32}
$$

---

### 2 pojkar, 3 flickor

$$
\binom{5}{2} = 10
$$

$$
P = \frac{10}{32}
$$

---

### Övriga kombinationer

$$
P(3\ pojkar) = \frac{10}{32}
$$

$$
P(4\ pojkar) = \frac{5}{32}
$$

$$
P(5\ pojkar) = \frac{1}{32}
$$

---

# Lotteriexempel

100 lotter:

- 1 → 100000 kr
- 2 → bostadsrätter
- 2 → kolonilotter
- 5 → cyklar
- 5 → 100 kr

Kalle köper **5 lotter**.

---

### a) minst 3 cyklar

$$
P = 0.0006
$$

---

### b) 200 kr, 1 cykel, 1 kolonilott

$$
P = 0.0001
$$

---

### c) bostad eller pengar

$$
P = 0.4162
$$

---

### d) något överhuvudtaget

$$
P = 0.5643
$$