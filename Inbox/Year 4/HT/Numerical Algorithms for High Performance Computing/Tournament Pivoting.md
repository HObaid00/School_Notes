
## a) Structure evolution of matrix $A$

We consider a matrix $A \in \mathbb{R}^{8b \times b}$.

At each iteration, the algorithm performs two parallel loops:

1. First loop: Apply Gaussian elimination (GEPP) to blocks of size $2b \times b$
2. Second loop: Copy upper triangular parts into the next level

### Evolution idea

- Initially: matrix consists of stacked $b \times b$ blocks
- After first loop: each $2b \times b$ block becomes upper-triangular
- After second loop: only upper $b \times b$ parts are kept and compacted

This process repeats hierarchically.

### Description of block states

- **Upper-triangular blocks**: result of GEPP
- **Zero blocks**: eliminated entries
- **Unused blocks**: discarded after copying

![[Pasted image 20260409140739.png|697]]
- 3 stages (for $8b \to 4b \to 2b$ reduction)
- Mark blocks as:
  - "filled" (upper-triangular)
  - "zero"
  - "unused"

---

## b) Memory access model (EREW vs CREW)

- GEPP operates on **disjoint $2b \times b$ blocks**
  → satisfies **EREW (Exclusive Read Exclusive Write)**

- Copy phase:
  - Multiple CPUs may read/write overlapping regions
  → potential **CREW conflict**

### Fix using private memory

1. Each CPU copies one $b \times b$ block into private memory
2. Then writes it to target location

⇒ Ensures **EREW compliance**

---

## c) Data transfer analysis

Each CPU performs per iteration:

- Load: $2b \times b$ block
- Write: $b \times b$ block

### Total transfers per iteration:

$$\Large 2b^2 + b^2 = 3b^2$$

### Worst-case CPU

- CPU handling the top block participates in all iterations
- Number of iterations:

$$\Large k = \log_2 n$$

### Total transfers for that CPU:

$$\Large 3b^2 \cdot \log_2 n$$

### Memory requirement

Each CPU must store:

$$\Large 2b \times b = 2b^2 \text{ elements}$$

---

## d) Use in communication-avoiding LU

TournamentPEM is used to:

1. Select $b$ pivot rows from first $b$ columns
2. Apply row permutations
3. Perform LU without pivoting on selected rows

Then iterate on trailing matrix.

### Benefit

Reduces communication complexity:

- Tournament pivoting:

$$\Large O\left(\frac{n}{b} \log p_r\right)$$

- Classical pivoting:

$$\Large O(n \log p_r)$$

⇒ significantly less communication