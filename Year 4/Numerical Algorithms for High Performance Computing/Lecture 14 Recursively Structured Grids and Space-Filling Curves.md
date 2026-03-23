Michael Bader  
TUM – SCCS  
Winter 2025/2026  

---

# Part I  
## From Quadtrees to Space-Filling Curves

---

# Quadtrees to Describe Geometric Objects

- Start with an initial square (covering entire domain).
- Recursive subdivision into four subsquares.
- Adaptive refinement possible.
- Terminate if square lies completely inside or outside domain.

![[Pasted image 20260303132304.png]]

---

# Storing a Quadtree – Sequentialisation

- Sequentialise cells via **depth-first traversal**.
- Relative numbering of children determines order.
- Leads to **Morton order**.

![[Pasted image 20260303132320.png]]

---

# Morton Order

Binary representation:

- Odd bits → vertical position.
- Even bits → horizontal position.

Bit interleaving defines traversal order.

---

# Morton Order and Cantor’s Mapping

Bit interleaving idea:

Interleave bits of two coordinates.

Cantor (1877):

- Bijective mapping:
  $$
  [0,1] \rightarrow [0,1]^2
  $$
- Same cardinality of interval and square.

Question:
- Is there a **continuous** mapping?
  → leads to space-filling curves.

---

# Preserving Neighbourship (2D)

Goal:

- Sequential neighbors remain geometric neighbors.
- Uniform $4 \times 4$ grid example.

Leads to special child numbering (Hilbert-like).

![[Pasted image 20260303132339.png]]

---

# Part II  
## Space-Filling Curves

---

# Definition of a Space-Filling Curve

Given continuous, surjective mapping:

$$
f : I \to Q \subset \mathbb{R}^n
$$

Then image $f(I)$ is space-filling if:

$$
|Q| > 0
$$

Where:

- $I \subset \mathbb{R}$ compact, typically $[0,1]$.
- Surjective:
  $$
  Q = f(I)
  $$

Theorem (Netto, 1879):

- No bijective space-filling mapping if $Q$ smooth manifold.

---

# Construction of the Hilbert Curve

Iterative construction:

1. Split square into 4 subsquares.
2. Construct subcurve in each subsquare.
3. Join subcurves appropriately.
4. Repeat recursively.

![[Pasted image 20260303132355.png]]

---

# Grammar for the Hilbert Curve

Non-terminals:
```
{H, A, B, C}
```

Start symbol:
```
H
```

Terminals:
```
{↑, ↓, ←, →}
```

Productions:

```
H ← A ↑ H → H ↓ B
A ← H → A ↑ A ← C
B ← C ← B ↓ B → H
C ← B ↓ C ← C ↑ A
```

- Replacement is simultaneous (L-system).
- Arrows define turtle-graphics drawing.

![[Pasted image 20260303132415.png]]

---

# Definition of Hilbert Mapping

For each:

$$
t \in I = [0,1]
$$

Define nested intervals:

$$
I \supset [a_1,b_1] \supset \dots \supset [a_n,b_n] \supset \dots
$$

Each step divides interval by 4.

Correspondence:

- Interval sequence ↔ sequence of subsquares.
- Converges to unique point:

$$
q \in Q = [0,1] \times [0,1]
$$

Define:

$$
h(t) = q
$$

Theorem:

$$
h : I \to Q
$$

defines a space-filling curve.

---

# Properties of Hilbert Mapping

We must show:

1. $h$ well-defined.
2. $h$ surjective.
3. $h$ continuous.

Surjectivity:

- For any $q \in Q$, construct subsquare sequence.
- Corresponds to interval sequence.
- Hence:
  $$
  q = h(t)
  $$

Continuity:
- Follows from Hölder continuity.

---

# 3D Hilbert Curves

Extension to 3D via recursive construction.

![[Pasted image 20260303132442.png]]

---

# Part III  
## Parallelisation Using Space-Filling Curves

---

# Generic Space-Filling Heuristic

Bartholdi & Platzman (1988):

1. Map 2D domain via SFC to unit interval.
2. Solve easier 1D problem.

For parallelisation:

1. Generate sequential order via SFC.
2. Perform 1D partitioning.
   - Split list into equal-sized segments.

---

# Hilbert-Curve Partitions (Cartesian Grid)

Properties:

- Curve splits domain into left/right sets.
- Boundary vertices appear sequentially.
- Produces compact partitions.

![[Pasted image 20260303132508.png]]

---

# Hilbert Orders on Quadtrees

Question:

- Can grammar generate adaptive Hilbert orders?

Extended grammar includes parentheses to mark level changes.

Non-terminals:
```
{H, A, B, C}
```

Terminals:
```
{↑, ↓, ←, →, (, )}
```

Productions:

```
H ← (A ↑ H → H ↓ B)
A ← (H → A ↑ A ← C)
B ← (C ← B ↓ B → H)
C ← (B ↓ C ← C ↑ A)
```

---

# Hölder Continuity

A function:

$$
f : I \to \mathbb{R}^n
$$

is continuous if:

For every $\varepsilon > 0$ there exists $\delta > 0$:

$$
|t_1 - t_2| < \delta
\Rightarrow
\|f(t_1) - f(t_2)\|_2 < \varepsilon
$$

Hölder continuity:

$$
\|f(t_1) - f(t_2)\|_2
\le
C |t_1 - t_2|^r
$$

- $r=1$ → Lipschitz.
- Hölder ⇒ uniform continuity.

---

# Hölder Continuity and Parallelisation

Interpretation:

- $\|f(t_1) - f(t_2)\|_2$ → geometric distance.
- $|t_1 - t_2|$ → 1D index distance.
- Also proportional to partition volume.

Thus:

Hölder continuity relates:

- **Partition size**
- **Geometric diameter**

→ Quantifies partition compactness.

---

# Hölder Continuity of Hilbert Curve

Proof sketch:

Choose $n$ such that:

$$
4^{-(n+1)} < |t_1 - t_2| < 4^{-n}
$$

At level $n$:

- Interval length: $4^{-n}$
- Subsquare edge length: $2^{-n}$

Then:

$$
\|h(t_1) - h(t_2)\|_2
\le
2^{-n}\sqrt{5}
$$

Since:

$$
2 \cdot 2^{-n} < \sqrt{|t_1 - t_2|}
$$

Result:

$$
\|h(t_1) - h(t_2)\|_2
\le
\frac{\sqrt{5}}{2}
|t_1 - t_2|^{1/2}
$$

Thus:

- Hilbert curve is Hölder continuous with exponent:

$$
r = \frac{1}{2}
$$

---

# Part IV  
## Refinement Trees and Encoding

---

# Hilbert-Order Bitstream Encoding

Quadtree encoded as bitstream following Hilbert order.

![[Pasted image 20260303132541.png]]

---

# Refinement-Tree Encoding

Tree nodes store:

- Number of leaves/subtree nodes.

Allows:

- Efficient skipping of subtrees during partitioning.
- Determine partition boundaries via leaf indices.

![[Pasted image 20260303132554.png]]

---

# REFTREE Algorithm (Partitioning)

Given attributed quadtree:

- Track first and last leaf of subtree.
- Compare with partition index range.
- Skip or traverse subtree accordingly.

Disadvantage:

- Required info scattered in stream.

Solution:

- Modified depth-first ordering.

![[Pasted image 20260303132618.png]]

---

# Parallelisation vs Partitioning with SFC

Besides partitioning:

- Data exchange at partition boundaries.
- Synchronize refinement status.
- Exploit **stack property** of Hilbert curves.

![[Pasted image 20260303132645.png]]

---

# Determining Left and Right

Extended turtle grammars:

Non-terminals:
```
{H, B, L, R, E, T}
```

Production examples:

```
H: H T / B L
B: T L / H R
L: E L / H R
R: L R / T E
E: T L / H R
T: T B / H R
```

Used to determine orientation changes during recursion.

![[Pasted image 20260303132707.png]]