## Find / Approximate a Function (1)
Problem:
- approximate a function that cannot be represented exactly: $f(x) \approx b(x)$
- using a representation $f(x) = \sum a_i \phi_i(x)$

Leads to question of approximation between functions:

$$\Large
\|f\|^2 = \int f(x)^2 \, dx
$$

Minimize:

$$\Large
\left\| b(x) - \sum a_i \phi_i(x) \right\|^2
$$

---
## Find / Approximate a Function (2)

More interesting setup:
- solve a partial differential equation, e.g.:

$$\Large
\frac{\partial^2}{\partial x^2} f(x) = b(x)
$$

(with initial and boundary conditions)

Wanted:
- function $f(x) = \sum a_i \phi_i(x)$ that “solves” the equation
- depending on choice of $\phi_i(x)$, only an approximate solution may be possible

---

### Leads to Finite Element Methods

- demand:

$$\Large
\int v(x)\left( b(x) - \frac{\partial^2}{\partial x^2} f(x) \right) dx = 0 \quad \text{for all } v
$$

- solution depends on:
  - choice of basis functions $\phi_i$
  - choice of test functions $v$

→ leads to a system of equations for $a_i$

---
