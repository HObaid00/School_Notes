Given:
- a set of values: $f_i, f_{ij}, \dots$ (1D, 2D, $\dots$)
- at points $x_i, x_{ij}, \dots$

Wanted:
- function $f(x) = \sum a_i \phi_i(x)$ such that

$$\Large
\sum (f_i - f(x_i))^2 + \gamma \|L f\| \;\; \text{is minimal}
$$

with $L f = f'$, $L f = f''$, or similar.

- compute coefficients $a_i$ (depend on parameter $\gamma$)

**Important aspects:**
- more or less data $f_i$ available than required (over- or underdetermined)
- frequent approach to predict value $f(x)$  
  → related to classification and learning (“big data”)
- solution depends on clever choice of the basis functions $\phi_i$  
  → how many functions, and how should they look like?

---

