Michael Bader  
TUM – SCCS  
Winter 2025/2026  

---

# Part I  
## Parallelization of Steepest Descent

---

# Minimization of Quadratic Forms

Solve linear system via minimization:

$$
f(x) = \frac{1}{2} x^T A x - b^T x + c,
\qquad A = A^T \text{ positive definite}
$$

Gradient:

$$
f'(x) =
\begin{pmatrix}
\frac{\partial f}{\partial x_1} \\
\vdots \\
\frac{\partial f}{\partial x_n}
\end{pmatrix}
$$

Here:

$$
f'(x) = Ax - b
$$

Thus:

$$
f'(x)=0 \iff Ax=b
$$

⇒ Solving $Ax=b$ is equivalent to a minimisation problem.

![[Pasted image 20260303124600.png]]

---

# Direction of Steepest Descent

- $f'(x)$: direction of steepest ascent.
- Residual:
  $$
  r = b - Ax
  $$
- Since $f'(x)=Ax-b=-r$, the residual is direction of steepest descent.

Update rule:

$$
x^{(i+1)} = x^{(i)} + \alpha r^{(i)}
$$

Choose $\alpha$ such that $f(x^{(i+1)})$ minimal:

$$
\frac{\partial}{\partial \alpha} f(x^{(i+1)}) = 0
$$

Result:

$$
\alpha_i =
\frac{(r^{(i)})^T r^{(i)}}
     {(r^{(i)})^T A r^{(i)}}
=
\frac{\langle r^{(i)}, r^{(i)} \rangle}
     {\langle r^{(i)}, A r^{(i)} \rangle}
$$

![[Pasted image 20260303124617.png]]

---

# Steepest Descent – Algorithm

1. $r^{(i)} = b - A x^{(i)}$
2. 
   $$
   \alpha_i =
   \frac{\langle r^{(i)}, r^{(i)} \rangle}
        {\langle r^{(i)}, A r^{(i)} \rangle}
   $$
3. $x^{(i+1)} = x^{(i)} + \alpha_i r^{(i)}$

## Parallel Implementation?

Per iteration:

- Two parallel SpMVs:
  - $Ax^{(i)}$
  - $A r^{(i)}$
- Each SpMV:
  - fanout → local SpMV → fanin → accumulate
- Two scalar products → global reductions.
- Update of $x$ depends on reduction.

![[Pasted image 20260303132202.png]]

---

# Propagation of Error and Residual

Error:

$$
e^{(i+1)} = e^{(i)} - \alpha_i r^{(i)}
$$

Residual propagation:

$$
r^{(i+1)} = r^{(i)} - \alpha_i A r^{(i)}
$$

Steepest descent with propagated residuals:

1. Compute $A r^{(i)}$.
2. 
   $$
   \alpha_i =
   \frac{\langle r^{(i)}, r^{(i)} \rangle}
        {\langle r^{(i)}, A r^{(i)} \rangle}
   $$
3. $x^{(i+1)} = x^{(i)} + \alpha_i r^{(i)}$
4. $r^{(i+1)} = r^{(i)} - \alpha_i A r^{(i)}$

---

# Parallel Steepest Descent – Improved Form

Rearranged loop:

1. $x := x + \alpha r$
2. $r := r - \alpha w$
3. $w := A r$  (parallel SpMV)
4. $\rho = \langle r,r \rangle$  (global reduction)
5. $\sigma = \langle w,r \rangle$ (merge with step 4)
6. $\alpha = \rho/\sigma$

Comments:

- One SpMV per iteration.
- One combined global reduction.

---

# Pipelined Steepest Descent

Idea:

Precompute via recurrence.

Given:

$$
r^{(i+1)} = r^{(i)} - \alpha_i w^{(i)}
$$

Multiply by $A$:

$$
w^{(i+1)} = A r^{(i+1)}
= w^{(i)} - \alpha_i t^{(i)}
$$

where:

$$
t^{(i)} = A w^{(i)}
$$

New loop:

1. $t^{(i)} = A w^{(i)}$ (SpMV)
2. Compute $\alpha_i$ (2 reductions)
3. Update $x, r, w$

Step 2 no longer depends on step 1 → potential overlap.

---

# Part II  
## Parallel Conjugate Gradients

---

# From Steepest Descent to CG

Use $A$-orthogonal search directions:

$$
x^{(i+1)} = x^{(i)} + \alpha_i p^{(i)}
$$

with

$$
\alpha_i =
\frac{(r^{(i)})^T r^{(i)}}
     {(p^{(i)})^T A p^{(i)}}
$$

Search direction update:

$$
p^{(i)} = r^{(i)} + \beta_i p^{(i-1)}
$$

$$
\beta_i =
\frac{(r^{(i)})^T r^{(i)}}
     {(r^{(i-1)})^T r^{(i-1)}}
$$

---

# Conjugate Gradients – Algorithm

Initial:

$$
p^{(0)} = r^{(0)} = b - A x^{(0)}
$$

Loop:

1. 
   $$
   \alpha_i =
   \frac{\langle r^{(i)}, r^{(i)} \rangle}
        {\langle p^{(i)}, A p^{(i)} \rangle}
   $$
2. $x^{(i+1)} = x^{(i)} + \alpha_i p^{(i)}$
3. $r^{(i+1)} = r^{(i)} - \alpha_i A p^{(i)}$
4. 
   $$
   \beta_{i+1} =
   \frac{\langle r^{(i+1)}, r^{(i+1)} \rangle}
        {\langle r^{(i)}, r^{(i)} \rangle}
   $$
5. $p^{(i+1)} = r^{(i+1)} + \beta_{i+1} p^{(i)}$

---

# Parallel CG – Basic Implementation

Per iteration:

- 1 parallel SpMV: $s^{(i)} = A p^{(i)}$
- 2 dot products:
  - $\langle r^{(i)}, r^{(i)} \rangle$
  - $\langle p^{(i)}, s^{(i)} \rangle$
- Global synchronisation.
- Update vectors.
- Another reduction for $\beta$.

→ Two global reductions per iteration.

---

# Chronopoulos & Gear Variant

Rearranges computations:

- Compute dot products together.
- Express $\beta$ via alternative formula:

$$
\beta_i =
\frac{\alpha_i^2 \langle s^{(i)}, s^{(i)} \rangle
      - \langle r^{(i)}, r^{(i)} \rangle}
     {\langle r^{(i)}, r^{(i)} \rangle}
$$

Allows:

- Merge dot products.
- Reduce synchronisation points.

---

# Pipelined CG (Ghysels & Vanroose)

Introduce additional recurrences:

- $s = A p$
- $w = A r$
- $z = A s = A^2 p$

Key idea:

Overlap:

- Dot products
- SpMV

Requires asynchronous Allreduce.

![[Pasted image 20260303133934.png]]

---

# Preconditioned CG

With $M^{-1}$:

$$
\tilde r^{(i)} = M^{-1} r^{(i)}
$$

Algorithm:

1. 
   $$
   \alpha_i =
   \frac{(r^{(i)})^T M^{-1} r^{(i)}}
        {(p^{(i)})^T A p^{(i)}}
   $$
2. Update $x, r$.
3. 
   $$
   \beta_{i+1} =
   \frac{(r^{(i+1)})^T M^{-1} r^{(i+1)}}
        {(r^{(i)})^T M^{-1} r^{(i)}}
   $$

Parallel issues:

- SpMV with $A$.
- Application of $M^{-1}$.
- Two reductions.

---

# Gropp’s Asynchronous PCG

Overlaps:

- Dot product $\langle p, s \rangle$
- Preconditioner application $M^{-1}s$

and

- Dot product $\langle r, u \rangle$
- SpMV $A u$

Requires asynchronous global communication.

![[Pasted image 20260303134000.png]]

---

# Part III  
## Predict-and-Recompute CG (Chen & Carson, 2020)

Starting from preconditioned CG.

Observation:

Recursive update of

$$
\nu_k = \langle \tilde r^{(k)}, r^{(k)} \rangle
$$

Prediction:

$$
\nu_k' =
\nu_{k-1}
- 2\alpha_{k-1} \sigma_{k-1}
+ \alpha_{k-1}^2 \gamma_{k-1}
$$

with:

$$
\sigma_k = \langle \tilde r^{(k)}, s^{(k)} \rangle,
\qquad
\gamma_k = \langle \tilde s^{(k)}, s^{(k)} \rangle
$$

Problem:

- Pure recurrence → numerical instability.
- $\nu_k'$ may become negative.

Solution:

- Use $\nu_k'$ as predictor.
- Recompute
  $$
  \nu_k = \langle \tilde r^{(k)}, r^{(k)} \rangle
  $$
  explicitly.

---

# Predict-and-Recompute CG

Key steps:

1. Predict $\nu_k'$.
2. Compute:
   - $\mu_k = \langle p^{(k)}, s^{(k)} \rangle$
   - $\sigma_k$
   - $\gamma_k$
   - $\nu_k$
3. 
   $$
   \alpha_k = \frac{\nu_k}{\mu_k}
   $$

Maintains numerical stability close to standard CG.

---

# Pipelined Predict-and-Recompute CG

Add recurrences:

$$
s_k = w_k + \beta_k s_{k-1}
$$

$$
w_k = w_{k-1} - \alpha_{k-1} u_{k-1}
$$

with additional vectors:

- $u_k = A \tilde s_k$
- $w_k = A \tilde r_k$

Overlap:

- SpMV
- Preconditioner
- Global reductions

Only one global reduction per iteration.

---

# Summary: Communication-Avoiding CG

Key ideas:

- Introduce recurrences for vectors multiplied with $A$, $M^{-1}$.
- Overlap global reductions with SpMV.
- Reduce number of synchronisations.

Challenges:

- Numerical stability.
- Rounding error amplification.

Remedy:

- Predict via recurrence.
- Recompute critical scalars explicitly.