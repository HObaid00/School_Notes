Michael Bader  
TUM – SCCS  
Winter 2025/2026  

---

# Part I  
## (Cache-)Efficient (Parallel) Algorithms for Structured Grids

---

## Analysis of Cache Usage for 2D/3D Stencil Computation

We assume:

- 2D or 3D Cartesian mesh with  
  $$
  N = n^d
  $$
  grid points.
- Stencil only accesses nearest neighbours.
  - Typically  
    $$
    c_M := 2d + 1
    $$
    or  
    $$
    c_M := 3^d
    $$
    accesses to variables per stencil  
    (plus access to stencil weights, if stored in variables).
- $c_F$ floating-point operations per stencil,  
  $$
  c_F \in \mathcal{O}(c_M).
  $$

We examine:

- Number of memory transfers in the Parallel External Memory model  
  (equivalent to cache misses).
- Different implementations and algorithms.
- Ratio of communication to computation.

---

## Straightforward Loop-Based Implementation

Example (Gauss–Seidel-type relaxation step):

```c
for i = 1 to n do
  for j = 1 to n do
    u[i,j] = 0.25 * (
        u[i-1,j] + u[i+1,j]
      + u[i,j-1] + u[i,j+1]
    );
```

### Algorithm in the (Parallel) External Memory Model

- $u[i,j-1]$, $u[i,j]$, and $u[i,j+1]$ are stored contiguously in memory.
- Strategy: keep 3 rows $u[i-1,:]$, $u[i,:]$, $u[i+1,:]$ in cache.
  - Requires cache size:
    $$
    M > 3n \text{ floats}.
    $$
- Load new row $u[i+1,:]$ before start of the $j$-loop  
  → $\frac{n}{L}$ transfers.

Total:
$$
\frac{n^2}{L} = \frac{N}{L}
$$
transfers  
(subject to $M > 3n$).

---

## Straightforward Loop-Based Implementation (Temporal Locality)

Idealized analysis — only temporal locality:

- $u[i,j-1]$ and $u[i,j]$ were used in previous $j$-iteration  
  → accessed from cache.
- $u[i-1,j]$ accessed in previous $i$-iteration.  
  In cache only if:
  $$
  M > n
  $$
  (otherwise capacity miss).
- $u[i,j+1]$ and $u[i+1,j]$ not accessed before  
  → must consider spatial locality (cache lines).

Copy picture from **Slide 5**.

```C
for i from 1 to n do
	for j from 1 to n do {
		u[ i , j ] = 0.25*(u[ i −1,j]+u[ i +1,j]+u[ i , j −1]+u[i , j +1])
	}
```

---

## Straightforward Loop-Based Implementation (Spatial Locality)

Consider small cache:
$$
M < n.
$$

Spatial locality for $u[i-1,j]$, $u[i,j+1]$, $u[i+1,j]$:

- $u[i-1,j]$ and $u[i+1,j]$ often in same cache line as
  $u[i-1,j-1]$, $u[i+1,j-1]$.
  → cache miss only every $L$-th iteration.
- Same for $u[i,j+1]$.

On average:

- Three cache misses every $L$-th iteration.

Total:
$$
\frac{3N}{L} = \frac{3n^2}{L}
$$
(for $M < n$).

Copy picture from **Slide 6**.
```C
for ii from 1 to n by b do
	for jj from 1 to n by b do
		for i from ii to ii +b−1 do
			for j from jj to jj +b−1 do {
				u[ i , j ] = 0.25*(u[ i −1,j]+u[ i +1,j]
			  + u[ i , j −1]+u[i , j +1])
			}
```


---

## Loop-Based Implementation with Blocking

```c
for ii = 1 to n step b do
  for jj = 1 to n step b do
    for i = ii to ii+b-1 do
      for j = jj to jj+b-1 do
        u[i,j] = 0.25 * (
            u[i-1,j] + u[i+1,j]
          + u[i,j-1] + u[i,j+1]
        );
```

### Number of Cache Line Transfers

- Choose $b$ such that:
  $$
  M > 3b
  $$
- Then:
  $$
  \approx \frac{N}{L}
  $$
  transfers.
- No further dependence on $M$ (besides constraint on $b$).

⚠ Blocking changes update order.

Copy picture from **Slide 7**.

---

## Blocking in the Parallel External Memory Model

Parallel version:

```c
for ii = 1 to n step b do in parallel
  for jj = 1 to n step b do in parallel
    for i = ii to ii+b-1 do
      for j = jj to jj+b-1 do
        stencil update
```

Assume:
$$
\frac{n}{b} \times \frac{n}{b}
$$
processors.

Each processor reads:
$$
(b+2) \times (b+2)
$$
elements (including ghost layer).

More exact formula:
$$
\left(\frac{n}{b}\right)^2 \cdot \left\lceil \frac{b+2}{L} \right\rceil^2
\approx
\frac{(b+2)^2}{b^2} \cdot \frac{N}{L}
$$
cache line transfers.

Copy picture from **Slide 8**.

---

## Extension to 3D Stencils

### Simple loops

- If cache holds 3 planes:
  $$
  M > 3n^2 \Rightarrow \frac{N}{L} \text{ transfers}
  $$
- If cache holds less than 1 plane:
  $$
  M < n^2 \Rightarrow \frac{3N}{L}
  $$
- If cache holds less than 1 row:
  $$
  M < n
  $$
  - $5N/L$ transfers (if $c_M = 6$)
  - $9N/L$ transfers (if $c_M = 3^3 = 27$)

### With blocking

- Cache must hold 3 planes of a $b^3$ block:
  $$
  M > 3b^2
  $$
- Then:
  $$
  \approx \frac{N}{L}
  $$
  transfers.

Copy picture from **Slide 9**.

---

# Part II  
## (Cache-)Efficient Approaches for Multiple Grid Traversals

---

## Further Increase of Cache Reuse

Multiple stencil evaluations:

```c
for t = 1 to m do
  for i = 1 to n do
    for j = 1 to n do
      stencil update
```

Possible approaches:

- Blocking in space and time?
- Precedence constraints of stencil updates?

![[Pasted image 20260301212729.png]]

---

## Region of Influence for Stencil Updates

1D example.

- Start with one block loaded into cache.
- Perform all updates without additional cache transfers.
- Valid region narrows by stencil size each step.
- Leads to trapezoidal update regions.
- More complex in 2D and 3D.

![[Pasted image 20260301212753.png]]

---

## Time Skewing (1D Example)

Choose trapezoid size:
$$
S \times T
$$

- Need:
  $$
  S + T
  $$
  grid points in cache.
- Goal: avoid cache transfers for $T-1$ traversals.

Ideal case:
$$
\frac{N}{S} \cdot \frac{S/L}{T-1}
=
\mathcal{O}\left(\frac{N}{L T}\right)
$$
transfers per iteration.

![[Pasted image 20260301212811.png]]

---

## Divide & Conquer: Space Split

Applicable if spatial domain is at least twice number of time steps.

Note precedence between left and right subdomain.

![[Pasted image 20260301212829.png]]

---

## Divide & Conquer: Time Split

Applied if region is narrow  
(spatial domain < twice number of time steps).


---

## Cache Oblivious Stencil Traversal (Frigo & Strumpen, 2005)

### Base Procedure

```c
COstencil1D(int t0, int t1, int x0, int s0, int x1, int s1)
{
  int travs = t1 - t0;

  if (travs < 1) return; // error

  if (travs == 1) { // base case
    for (x = x0; x < x1; x++)
      stencil(t0, x);
  }

  // recursive cases...
}
```

### Recursive Strategy

If region is wide → space cut:

```c
xm = (2*(x0+x1) + (2+s0+s1)*travs)/4;

COstencil1D(t0,t1,x0,s0,xm,-1);
COstencil1D(t0,t1,xm,-1,x1,s1);
```

Else → time cut:

```c
ts = travs/2;

COstencil1D(t0,t0+ts,x0,s0,x1,s1);
COstencil1D(t0+ts,t1,
            x0+s0*ts, s0,
            x1+s1*ts, s1);
```

---

## Cache Oblivious Complexity

- 1D: $\mathcal{O}(M)$ grid points in cache.
- 2D: $\mathcal{O}(\sqrt{M}) \times \mathcal{O}(\sqrt{M})$.
- Roughly half of:
  - $\mathcal{O}(M)$ (1D)
  - $\mathcal{O}(\sqrt{M})$ (2D)
  time steps executable on cached data.

Result:
$$
\mathcal{O}\left(\frac{N}{L \sqrt[d]{M}}\right)
$$
cache misses  
(in ideal cache model).

---

## References

- Frigo & Strumpen (2005), *Cache Oblivious Stencil Computations*, ICS.
- Frigo & Strumpen (2007), *Memory Behavior of Cache Oblivious Stencil Computations*, J. Supercomput.
- Datta et al. (2009), *Optimization and Performance Modeling of Stencil Computations*, SIAM Review.

---

# Part III  
## Parallelisation

---

## Example: Multiple Ghost Layers

3-point stencil in 1D:

- Trapezoidal dependency regions.
- For each additional stencil traversal without communication:
  enlarge ghost layer by 1.

Steps:

1. Send ghost layers  
2. Update local region  
3. Update boundary region  

→ overlap (1) and (2).
![[Pasted image 20260301213806.png]]


---

## Improved Ghost Layer Strategy

Observation:

- Some values computed redundantly by both processors.
- Improvement: send updated unknowns.
- More complex boundary exchange.

Steps:

1. Perform two local steps  
2. Send required values  
3. Update remaining local region  
4. Update remaining boundary region  

→ overlap (2) and (3).

![[Pasted image 20260301212915.png]]

---

## Literature: Matrix Powers Kernel

Generalizations:

- 2D and 3D
- Unstructured grids / sparse matrices
- Polynomials in system matrix $A$

References:

- Hoemmen: *Communication-avoiding Krylov subspace methods* (PhD thesis).
- Mohiyuddin et al., SC’09.
- Demmel et al., IPDPS 2008.