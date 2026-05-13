## Definition

Händelserna $A$ och $B$ kallas **oberoende** ($A \perp B$)

om

$$
P(A \cap B) = P(A)P(B)
$$

Om $A$ och $B$ **ej oberoende** ($A \not\perp B$)

så kallas $A$ och $B$ **beroende**.

---

## Observation

Additionssatsen-variant:

$$
P(A \cup B)
$$

om

$$
A \perp B
$$

så gäller

$$
P(A \cup B) = P(A) + P(B) - P(A)P(B)
$$

---

# Sannolikhetslära

## Definition

Om

$$
P(B) > 0
$$

så är den **betingade sannolikheten** av $A$ givet $B$

$$
P(A|B) = \frac{P(A \cap B)}{P(B)}
$$

---

## Tolkning

Den betingade sannolikheten är **inte arean av $A$ i förhållande till $\Omega$**  
utan **arean av $A \cap B$ i förhållande till $B$**.

---

## Observation

Om

$$
A \perp B
$$

så gäller

$$
P(A|B) = P(A)
$$


---

## Multiplikationsregel

$$
P(A \cap B) = P(A|B)P(B)
$$

och

$$
P(A \cap B) = P(B|A)P(A)
$$

---

## Viktigt

$$
P(A|B) \neq P(B|A)
$$

---

# Bayes sats

## Sats

Om

$$
\{B_1, B_2, ..., B_n\}
$$

är en **partition av $\Omega$**

så gäller

$$
P(B_k|A) =
\frac{P(A|B_k)P(B_k)}
{\sum_{i=1}^{n} P(A|B_i)P(B_i)}
$$

---

# Exempel

En student läser en kurs där en **valfri lab är obligatorisk**.

Labbarna väljs enligt:

$$
P(\text{lab 1}) = 0.41
$$

$$
P(\text{lab 2}) = 0.34
$$

$$
P(\text{lab 3}) = 0.24
$$

och baserat på resultat från tidigare år är

$$
P(T|\text{lab 1}) = 0.37
$$

$$
P(T|\text{lab 2}) = 0.45
$$

$$
P(T|\text{lab 3}) = 0.63
$$

där

$$
T = \{\text{studenten klarar tentan}\}
$$

---

## a)

Hur stor är studentens chans att klara kursen?

---

### Lösning

$$
P(T) =
P((T \cap \ell_1) \cup (T \cap \ell_2) \cup (T \cap \ell_3))
$$

$$
= P(T|\ell_1)P(\ell_1)
+ P(T|\ell_2)P(\ell_2)
+ P(T|\ell_3)P(\ell_3)
$$

$$
= 0.37 \cdot 0.41
+ 0.45 \cdot 0.34
+ 0.63 \cdot 0.25
$$

$$
= 0.4622
$$

---

## b)

Vilken lab ska studenten välja för att ha störst chans att klara tentan?

---

### Lösning

$$
P(T|\ell_3) = 0.63
$$

är större än

$$
P(T|\ell_2) = 0.45
$$

och

$$
P(T|\ell_1) = 0.37
$$

Alltså bör studenten välja **lab 3**.

---

## c)

Studenten får veta att en kompis klarade tentan förra året.

Vad är sannolikheten att denne gjorde **lab 1 eller lab 2**?

---

### Lösning

$$
P(\ell_1 \cup \ell_2 | T)
=
1 - P(\ell_3 | T)
$$

---

Beräkning:

$$
P(\ell_1 \cup \ell_2 | T)
=
1 -
\frac{P(\ell_3 \cap T)}
{P(T \cap (\ell_1 \cup \ell_2 \cup \ell_3))}
$$

---

$$
=
1 -
\frac{P(\ell_3 \cap T)}
{P(T \cap \ell_1) + P(T \cap \ell_2) + P(T \cap \ell_3)}
$$

---

$$
=
1 -
\frac{P(\ell_3 \cap T)}
{P(T|\ell_1)P(\ell_1)
+ P(T|\ell_2)P(\ell_2)
+ P(T|\ell_3)P(\ell_3)}
$$

---

Insättning av värden:

$$
=
1 -
\frac{0.63 \cdot 0.25}{0.4622}
$$

$$
= 0.6592
$$
