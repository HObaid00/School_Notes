## Definition
Om $(X,Y)$ är en diskret variabel så är dess **sammansatta s.f.**

$$\Large
p_{X,Y}(j,k) = P(X=j, Y=k)
$$

där

$$\Large
S_X, S_Y \subseteq \mathbb{N}
$$

---

## Sannolikhet för mängd

För varje

$$\Large
A \subseteq S_X \times S_Y
$$

är

$$\Large
P((X,Y)\in A) =
\sum_{(j,k)\in A} p_{X,Y}(j,k)
$$

---

## Normalisering

$$\Large
\sum_{(j,k)\in S_X \times S_Y} p_{X,Y}(j,k) = 1
$$

---

## Fördelningsfunktion

$$\Large
F(x,y) =
\sum_{j=0}^{x}\sum_{k=0}^{y} p_{X,Y}(j,k)
$$

---

## Marginalsannolikheter

$$\Large
P(X=j) = \sum_{k\in S_Y} p_{X,Y}(j,k)
$$

$$\Large
P(Y=k) = \sum_{j\in S_X} p_{X,Y}(j,k)
$$

---
