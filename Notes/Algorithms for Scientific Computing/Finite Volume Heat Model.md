# Finite Volume Heat Model

To solve the Poisson equation numerically, we first discretize space.

The lecture models a metal plate as many small rectangular cells.

---

# Grid Representation

Each cell stores a temperature:

$$
T_{ij}
$$

where:

- $i$ indexes the horizontal direction
- $j$ indexes the vertical direction

---

# Heat Flow Principle

Experiments show:

$$\Large
q \propto \Delta T
$$

Heat flow is proportional to temperature difference.

If neighboring cells have different temperatures, heat flows between them.

---

# Heat Flow Across One Edge

For the left edge:

$$\Large
q_{ij}^{(\text{left})}
=
k_x
(T_{ij}-T_{i-1,j})
h_y
$$

where:

- $k_x$ is conductivity
- $h_y$ is edge length

---

# Total Heat Balance

Heat flows through all four edges:

- left
- right
- top
- bottom

At equilibrium:

$$\Large
q_{ij} + F_{ij} = 0
$$

where:

- $F_{ij}$ is external heating

---

# Resulting Discrete Equation

The discrete system becomes:

$$\Large
f_{ij}
=
-\frac{k}{h_x^2}
(2T_{ij}-T_{i-1,j}-T_{i+1,j})
-\frac{k}{h_y^2}
(2T_{ij}-T_{i,j-1}-T_{i,j+1})
$$

This is the discrete version of the Poisson equation.

---

# Key Idea

Continuous PDEs become systems of linear equations after discretization.

---
# Links
[[Algorithms for Scientific Computing]]