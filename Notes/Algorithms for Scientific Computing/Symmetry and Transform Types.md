# Symmetry and Transform Types

Different transforms are associated with different symmetry properties.

The symmetry determines which basis functions are most natural.

---

# Even Symmetry

Even symmetry means:

$$\Large
f_n = f_{-n}
$$

Even signals are naturally represented using cosine functions because:

$$
\cos(-x)=\cos(x)
$$

This leads to the:

- Discrete Cosine Transform (DCT)

---

# Odd Symmetry

Odd symmetry means:

$$\Large
f_n = -f_{-n}
$$

Odd signals are naturally represented using sine functions because:

$$
\sin(-x)=-\sin(x)
$$

This leads to the:

- Discrete Sine Transform (DST)

---

# Transform Overview

| Symmetry | Transform |
|---|---|
| Real-valued | RDFT |
| Even symmetry | DCT |
| Odd symmetry | DST |

---

# Boundary Interpretation

The symmetry determines how data behaves at boundaries.

For the DST:

$$
f_0=f_N=0
$$

This corresponds to fixed endpoints.

For the DCT, boundaries are mirrored instead.

---

# Physical Interpretation

Different boundary conditions appear naturally in physics.

Examples:

| Boundary Type | Typical Transform |
|---|---|
| Fixed ends | DST |
| Reflective boundaries | DCT |

For example:

- A vibrating string fixed at both ends naturally uses sine waves.
- Heat reflection problems often use cosine expansions.

---

# Multiple Variants

There are many DCT and DST variants because boundaries can be handled differently.

The lecture notes mention:

- 8 DCT variants
- 8 DST variants

for a total of:

$$\Large 16$$

possible symmetry/boundary combinations.

---
# Links
[[Algorithms for Scientific Computing]]