Summan

$$\Large
S=X+Y
$$

har fördelning

---

Diskret:

$$\Large
F_S(s)=\sum_{j\in S_Y} F_X(s-j)p_Y(j)
$$

---

Kontinuerlig:

$$\Large
F_S(s)=\int_{-\infty}^{\infty} F_X(s-y)f_Y(y)dy
$$

---

Täthetsfunktion

Diskret:

$$\Large
f_S(s)=\sum_{j\in S_Y} p_X(s-j)p_Y(j)
$$

---

Kontinuerlig:

$$\Large
f_S(s)=
\int_{-\infty}^{\infty}
f_X(s-y)f_Y(y)dy
$$

Detta kallas **faltning** (*convolution*).

---
