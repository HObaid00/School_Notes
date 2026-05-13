**Michael Bader**  
TUM – SCCS  
Winter 2025/2026  

---

# Part I – Parallel Architectures

## Manycore CPU – Intel Xeon Phi (2012)

- Coprocessor (PCI bus extension card)
- ≈ 60 cores
- 4 hardware threads per core
- Simpler cores, but wider vector units
- SIMD width: 8 double-precision floats
- Used in Tianhe-2 supercomputer (2013)
- Knights Landing (2017): standalone CPU version

---

## Fujitsu A64FX (Fugaku Supercomputer)

- Architecture: Arm v8.2 + SVE
- 48 cores + 2–4 assistant cores
- Clock: 1.8–2.2 GHz
- SIMD width: up to 512 bits  
  → 8 double-precision floats
- FP16 / INT16 / INT8 support (AI)


---

# GPGPU – NVIDIA Fermi (2010)

## Hardware Execution Model

CUDA hierarchy:

- Kernel grid
- Thread blocks
- Streaming Multiprocessors (SMs)
- CUDA cores
- Warps (32 threads)

Key idea:
- Threads in a warp execute the same instruction path (SIMT).

---

## Fermi Architecture

- 512 CUDA cores
- 16 Streaming Multiprocessors (32 cores each)
- 384-bit memory interface
- Up to 6 GB GDDR5
- Unified L2 cache
- PCI-Express host interface

Each SM:
- 32 CUDA processors
- Integer ALU (32-bit precision)
- Floating-point unit (IEEE 754-2008)
- Fused multiply-add (FMA)
- 16 load/store units
- 64 KB shared memory / L1 cache (configurable)
- Register file: 32,768 × 32-bit

![[Pasted image 20260301192011.png]]

---

## Memory Hierarchy (Fermi)

- Unified memory request path
- Per-SM configurable:
  - 48 KB shared + 16 KB L1 cache
  - or 16 KB shared + 48 KB L1 cache
- Unified L2 cache (768 KB)

Key trend:
→ GPUs moving closer to CPU-style memory hierarchies.

![[Pasted image 20260301192032.png]]

---

# Follow-Up GPU Generations

## Volta

- Introduced Tensor Cores
- 8 tensor cores per SM
- Tensor operation:
  $$
  D = AB + C
  $$
  - $A, B$: 16-bit float
  - $C, D$: 32-bit float

## NVLink

- Introduced with Pascal (2016)
- Improved GPU interconnect
- Direct memory access across GPUs

![[Pasted image 20260301192115.png]]

---

## Ampere & Hopper

- Further architectural scaling
- Increased tensor performance
- Larger SMs
- Improved interconnect

*(Copy architecture overviews on slides 11–12.)*

---

# Future Parallel Architectures

Trends:

- Massive parallelism required
- Vector computing importance
  → multiple FPUs executing same operation
- Hybrid / heterogeneous architectures
- Memory hierarchy complexity
- Power efficiency constraints
- Heat management

---

# Vector Computing Paradigms

## 1. Classical Vector Processors

- Many ALUs
- Pipelined vector arguments
- Peak in 1980s
- Replaced by CPU clusters

## 2. SIMD (Single Instruction Multiple Data)

- Same operation on multiple operands
- Compiler vectorization
- Intrinsics possible

## 3. SIMT (Single Instruction Multiple Threads)

- GPU model
- Warp scheduler imposes instruction stream

---

# HPC Algorithmic Principles

Three key principles:

## 1. Improve Data Locality

- Cache-aware / cache-oblivious algorithms
- Communication-avoiding methods

## 2. Maximise Parallelism

- Instruction-level
- Core-level
- Chip-level
- Node-level

Reduce:
- Dependencies
- Synchronisation

## 3. Optimise Asymptotic Complexity

- Large-scale problems amplify complexity differences
- Consider parallel complexity
- Avoid scalability bottlenecks

---

# Part II – Performance Evaluation

---

# Speed-Up

Let:

- $T(p)$ = execution time on $p$ processors

Speed-up:

$$\Large
S(p) = \frac{T(1)}{T(p)}
$$

Typically:

$$\Large
1 \le S(p) \le p
$$

Absolute vs relative speed-up:

- Absolute: best sequential vs best parallel
- Relative: same algorithm on different processor counts

---

# Parallel Efficiency

$$\Large
E(p) = \frac{S(p)}{p}
$$

- $0 \le E(p) \le 1$
- Measures deviation from ideal linear scaling

---

# Scalability

Strong scalability:
- Fixed problem size
- Increase processors

Weak scalability:
- Increase problem size proportionally to processor count

---

# Amdahl’s Law

Assume:

- Sequential fraction $s$, $0 \le s \le 1$
- Perfect parallelisation for $1-s$

Execution time:

$$\Large
T(p)
=
sT(1)
+
\frac{1-s}{p}T(1)
$$

Speed-up:

$$\Large
S(p)
=
\frac{1}{s + \frac{1-s}{p}}
$$

Limit:

$$\Large
\lim_{p \to \infty} S(p) = \frac{1}{s}
$$

Conclusion:
→ Sequential part bounds scalability.

---

# Gustafson’s Law

Assume scaled problem size.

Let:

- $T(p) = 1$
- Sequential fraction $\sigma$

Then:

$$\Large
T(1) = \sigma + p(1-\sigma)
$$

Speed-up:

$$\Large
S(p)
=
\sigma + p(1-\sigma)
=
p - \sigma(p-1)
$$

Efficiency:

$$\Large
E(p)
=
\frac{S(p)}{p}
=
\frac{\sigma}{p} + (1-\sigma)
\to 1-\sigma
$$

More realistic for large-scale computing.

---

# Compute-Bound vs Memory-Bound

Arithmetic intensity:

$$\Large
\text{AI}
=
\frac{\text{Flops}}{\text{Bytes}}
$$

## Memory-Bound

- AI below critical ratio
- CPU waits for memory
- Improve by reducing memory traffic

## Compute-Bound

- Enough work to hide memory latency
- Improve by reducing operations

---

# Roofline Model

Axes (log-log):

- x-axis: Operational intensity (Flops/Byte)
- y-axis: Performance (GFlop/s)

Bandwidth limit:

$$
\text{Performance}
=
b \cdot a
$$

where:

- $b$ = bandwidth (GB/s)
- $a$ = arithmetic intensity

Peak performance ceiling:
- Horizontal line

---

## Interpretation

- Left of ridge point → memory-bound
- Right → compute-bound
- Performance ceilings:
  - NUMA effects
  - Missing vectorization
  - No instruction-level parallelism
  - No FMA usage

Improving cache usage increases effective arithmetic intensity.

![[RooflineModel.png]]

---

# Summary

Modern HPC systems:

- Manycore CPUs
- GPUs with SIMT
- Tensor cores
- Complex memory hierarchies

Performance analysis requires:

- Speed-up and efficiency
- Amdahl vs Gustafson
- Arithmetic intensity
- Roofline model

Algorithm design must optimise:

- Data locality
- Parallelism
- Asymptotic complexity