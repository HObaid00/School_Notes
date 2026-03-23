# Real-Time Systems  
## Part 4: Memory and Real-Time

TUM School of CIT – Chair of Robotics, Artificial Intelligence and Real-Time Systems (I6)

---

# Content

- Cache  
  - Memory mapping refresher  
  - Basic operation  
  - Mapping strategies  
- SDRAM  
- Multi-core  
  - Coherence  
  - Consistency  

---

# 1. CPU and Memory – Naïve View

CPU connected to off-chip memory (SRAM, DDR2/3/4).

Signals:

- Address
- Data
- Control signals (CS, R/W, RAS, CAS, CLK)

![[Pasted image 20260304152207.png]]

---

# 2. Memory Hardware Issues

- Single large address space
- Multiple ICs implementing memory
- Different memory types:
  - Internal SRAM
  - External DRAM/SDRAM
  - Special Function Registers
  - Memory-mapped peripherals
  - Off-chip devices (e.g., displays)

## Address Decoding

Goal: generate **Chip Select (CS)** from address lines.

![[Pasted image 20260304152223.png]]

---

# 3. Simple Address Decoding Example

Given:

- 10 address lines
- 8-bit data bus
- Total memory: 1 KiB
- Individual chips: 128 bytes

Since:

$$
8 \times 128\text{ B} = 1024\text{ B} = 1\text{ KiB}
$$

We need 8 chips.

- 7 LSBs → internal chip address
- 3 MSBs → decoder → 8 CS signals

![[Pasted image 20260304152250.png]]

Example address ranges:

- Memory 0: 0x000 – 0x07F
- Memory 1: 0x080 – 0x0FF
- Memory 2: 0x100 – 0x17F
- Memory 3: 0x180 – 0x1FF

Example CS logic:

$$
CS_0 = \neg(\neg A7 \land \neg A8 \land \neg A9)
$$

---

# 4. Cache – Motivation

Modern processors use deep memory hierarchies:

- L1 hit: ~5–7 cycles
- L1→L2→L3 miss: up to 1000 cycles

Hierarchy:

- L1 cache
- L2 cache
- L3 cache
- Off-chip memory (DDR)

Trade-offs:

- Speed ↑ closer to CPU
- Size ↑ further away
- Cost per byte ↓ further away

![[Pasted image 20260304153547.png]]

---

# Typical Cache Sizes

Example PC:

- L1: 32 KiB
- L2: 256 KiB
- L3: 10 MiB
- RAM: 16 GiB

---

# 5. Cache – Basic Operation

- Data transferred in **cache lines** (e.g., 16 bytes)
- Whole block copied on miss

![[Pasted image 20260304153628.png]]

---

# Locality

## Spatial locality

Accessing address A implies nearby addresses likely accessed.

## Temporal locality

Recently accessed data likely reused soon.

If access is random → cache effectiveness decreases.

---

# Address Structure Example

Assume:

- 32-bit address
- Cache line = 16 bytes

Offset bits:

$$
\text{offset} \in [0000, 1111]
$$

Address structure:

- Tag
- Offset

Reading one address copies full block into cache.

![[Pasted image 20260304153657.png]]

---

# Cache Line Structure

Each slot contains:

- Valid bit (1 bit)
- Dirty bit (1 bit)
- Tag
- Data block (e.g., 16 bytes)

Example (16-bit address, 16B line):

Total bits:

$$
1 + 1 + 12 + 16 \times 8 = 142 \text{ bits}
$$

To store 128 bits of data.

---

# Write Policies

## Write Through (WT)

- Write to cache AND lower memory
- More writes
- Simpler
- Higher energy

## Write Back (WB)

- Write only to cache
- Write to lower memory on eviction
- Requires dirty bit
- Fewer writes
- More complex

---

# 6. Direct Mapped Cache

Each memory block maps to exactly one cache line.

Analogy:

- 10 parking slots
- Student ID determines slot (last digit)

Simple but inefficient.

![[Pasted image 20260304153742.png]]

---

Example:

2 cache lines  
8 bytes per line  
Total size = 16 bytes

Address format:

- 1 bit → line
- 3 bits → offset
- Remaining bits → tag

Example:

Address 0x80 (1000 0000₂):

- Line = 0
- Offset = 0
- Tag = 1000₂

---

## Direct Mapping – Timing Example

Sequence:

- Read @0x80 → miss
- Read @0x98 → miss
- Read @0x78 → miss
- Write @0x80 → hit (dirty)
- Read @0x90 → miss (write-back)

Assume:

- Hit = 2 cycles
- Lower memory access = 8 cycles

Total:

$$
8 + 8 + 8 + 2 + (8 + 8) = 42 \text{ cycles}
$$

![[Pasted image 20260304153800.png]]

---

# Cache Replacement Policies

- LRU – Least Recently Used
- LFU – Least Frequently Used
- FIFO – First In First Out

---

# Fully Associative Cache

- Data can be placed in any cache line
- Requires parallel tag comparison
- Uses LRU/FIFO counters

Advantages:

- No conflict misses
- Better performance

Disadvantages:

- Complex
- Large hardware overhead

![[Pasted image 20260304153939.png]]

---

# Fully Associative (FIFO / Round Robin)

- Replacement pointer
- Only misses change pointer
- Hits do not affect pointer

Simpler than LRU.

![[Pasted image 20260304154006.png]]

---

# Set Associative Cache

Hybrid between direct and fully associative.

- Cache divided into sets
- Data maps to a set
- Can occupy any line inside set

Example:

- 4 lines
- 2 sets
- 2-way set associative

Only 2 lines compared per set.

![[Pasted image 20260304154027.png]]

8-way set associative ≈ behavior close to fully associative.

---

# Why Cache Analysis is Difficult

- Unknown memory addresses
- Unified instruction/data cache
- Timing anomalies:
  - Sometimes a cache hit increases execution time
- Cache state explosion

Reference: Reineke et al. – Timing Anomalies

---

# Cache Summary

- Direct mapped
- Fully associative
- Set associative
- Write-through vs write-back
- LRU vs FIFO

---

# 7. RAM and Timing

Storage delays vary significantly.

Non-determinism due to:

- Cache
- Memory technology
- Refresh
- Access direction changes

Relevant topic: WCET (Worst Case Execution Time)

---

# SRAM

- Static RAM
- No refresh
- Typically on-chip
- 6 transistors per bit
- Fast
- Large cell → less density
- No clock required

---

# SDRAM

Synchronous Dynamic RAM.

- Clocked
- Requires refresh
- Capacitor-based storage
- Large capacity
- Low cost
- Slower than SRAM
- Used after cache miss

DDR = Double Data Rate  
Transfers on rising + falling clock edge.

---

# SDRAM Architecture

- Data stored in banks
- Each bank has row buffer
- Row activation (ACT)
- Precharge (PCH)

If different row accessed:

1. Precharge current row
2. Activate new row

![[Pasted image 20260304154049.png]]

---

# SDRAM Timing Penalties

- ACT cost
- PCH cost
- Direction switch penalty (read ↔ write)

For WCET:

If row state unknown:

Assume worst-case penalty for every access.

---

# SDRAM Addressing Example (4MB)

22-bit address:

- 10 bits row (1024 rows)
- 1 bit bank (2 banks)
- 9 bits column (512 columns)
- 2 bits byte selection

![[Pasted image 20260304154142.png]]

---

# SDRAM Advantages / Drawbacks

Advantages:

- Large storage
- Low cost
- Enables advanced apps (camera, radar)

Drawbacks:

- Difficult WCET analysis
- Refresh interference
- Row buffer effects

---

# 8. Multi-Core Architectures

- AMP – Asymmetric multiprocessing
- SMP – Symmetric multiprocessing

---

# Cache Coherence Problem

Initial:

Core 1 loads value A = 42  
Core 2 loads value A = 42  

Core 1 increments A → 43  

Core 2 still sees 42 → stale data

![[Pasted image 20260304154232.png]]

---

# Cache Coherence – SWMR Invariant

Single-Writer Multiple-Reader (SWMR):

At any time:

- Either one core can write
- Or multiple cores can read

Token-based idea:

- If core has all tokens → write
- If core has ≥1 token → read

---

# Data Value Invariant

Value at start of epoch must equal value at end of last read-write epoch.

Correct value propagation required.

---

# Memory Consistency Problem

Example:

Core 1:
```
store data = new;
store flag = set;
```

Core 2:
```
load r1 = flag;
if (r1 != set) goto L1;
load r2 = data;
```

Question:

What value can `r2` observe?

Due to reordering, possible to observe stale values if no memory barriers are used.

---

# Summary

Memory hierarchy affects real-time behavior:

- Cache unpredictability
- SDRAM activation/precharge
- Refresh
- Direction switching
- Multi-core coherence and consistency

All significantly complicate WCET analysis.