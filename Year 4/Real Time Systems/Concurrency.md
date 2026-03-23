# Real-Time Systems  
## Part 7: Concurrency, Threads, Processes and Resource Access Protocols

TUM School of CIT – Chair of Robotics, Artificial Intelligence and Real-Time Systems (I6)

---

# 1. Concurrency

## Definition

Common meaning:

Concurrent events are **not causally dependent** on each other.  
Events (or sequences of events) are concurrent if none causes another.

Meaning in computer science:

Concurrency describes the property of code to be **runnable in parallel instead of sequentially**.

Instructions can run in parallel (pseudo-parallel) if they are **not dependent on each other's results**.

Types:

- **Multiprocessing**: Parallel execution of several independent processes on one or multiple processors.
- **Multithreading**: Parallel execution of sub-sequences within a process.

---

# Contents

- Introduction
- Processes
- Threads
- Resource access protocols

---

# 2. Motivation for Multiprocessor Computers

Limits of processor improvements:

**Moore’s Law**

> Number of transistors on a chip doubles roughly every two years, increasing performance.

However, two major limitations appear:

### Memory Wall

Memory speed does not scale with processor speed.

### Power Wall

Higher clock frequencies generate excessive heat that cannot be dissipated.

---

# Causes of Performance Degradation

Important delays arise from:

- Memory access
- Thread switching
- Thread synchronization

---

# 3. Processes

## Definition

A **process** is an abstraction of a program being executed.

A process includes:

- Code
- Stack
- CPU registers
- Memory mapping (MMU registers)
- File information
- Access rights
- Kernel stack

Processes can create new processes:

- **Parent process**
- **Child process**

![[Pasted image 20260304180601.png]]

---

# Process Execution

Process execution requires resources:

- CPU time
- Memory
- Other hardware resources

Execution time depends on:

- CPU performance
- Resource availability
- Input parameters
- Delay due to other processes

---

# Process States

Typical process states:

- Non-existing
- Created
- Ready
- Running
- Suspended
- Blocked
- Terminated

![[Pasted image 20260304180614.png]]

---

# Process Types

### Preemptable Process

Execution can be suspended.

Types:

- Fully preemptable
- Preemption only at predefined points

---

### Periodic Process

Released at a fixed frequency:

$$
p
$$

---

### Aperiodic Process

Irregular activation times.

- Soft deadline or none
- No minimum inter-arrival time

---

### Sporadic Process

Event-driven processes with hard deadlines.

Properties:

- Triggered by external signals
- Have a minimum inter-arrival time.

---

# Implementation Questions

When implementing concurrent systems:

- Which resources are required?
- What are the execution durations?
- How do processes communicate?
- When should processes be scheduled?
- How should processes synchronize?

---

# 4. Threads

Processes require large memory structures.

Process context includes:

- CPU state
- File descriptors
- Device state

Context switching between processes is expensive.

Therefore **threads** are used.

Threads:

- Share the same address space
- Require less management overhead
- Enable parallel execution paths within a program

---

# Reasons for Concurrency in Real-Time Systems

Real-time systems often:

- Run on distributed hardware
- Execute real-time and non-real-time tasks simultaneously
- Have strict response-time requirements
- Model parallel physical processes

---

# Multithreaded Processors

Processors may support **multiple threads simultaneously**.

Characteristics:

- Multiple thread contexts stored in registers
- Instructions from different threads feed the pipeline
- Latencies do not stall the processor

This differs from normal **context switching**, which requires storing state in memory.

---

# 5. Multithreading Techniques

## Fine-Grained Multithreading (Cycle-by-Cycle Interleaving)

- Instructions from different threads are interleaved every cycle
- Next instruction of same thread executed only after pipeline exit

---

## Coarse-Grained Multithreading (Block Interleaving)

- A thread runs until a blocking event occurs

Example blocking events:

- Cache miss
- Data dependency

---

# Processor Pipeline

Machine instructions are executed in several stages.

Typical pipeline stages:

1. Instruction Fetch
2. Instruction Decode
3. Execute (ALU)
4. Memory Access
5. Write Back

![[Pasted image 20260304180641.png]]

---

# Improving Pipeline Efficiency

Problem:

With only one thread, a new instruction can only be loaded every:

$$
n
$$

cycles, where:

$$
n = \text{pipeline length}
$$

Solution:

**Explicit-dependence lookahead**

The compiler marks independent instructions so the pipeline can execute them without waiting.

---

# Cycle-by-Cycle Interleaving

Advantages:

- No pipeline dependencies
- No pipeline flush after branch misprediction
- Less hardware required
- Faster context switching

Disadvantages:

- Less efficient than block interleaving.

---

# Block Interleaving

Types of switching:

### Static Switching

- Explicit context-switch instruction
- Based on instruction groups

Example triggers:

- Load
- Store
- Branch instructions

---

### Dynamic Switching

Switch occurs when:

- Cache miss occurs
- Signal/interrupt arrives
- Value dependency detected
- Conditional switch conditions met

---

# Concurrency Use Case: Interrupts

Interrupts are commonly used for:

- Interaction with external hardware

Example:

A thermometer triggers an interrupt when a **critical temperature level** is reached.

![[Pasted image 20260304180709.png]]

---

# Processes vs Threads

Processes:

- Separate memory spaces
- Higher management overhead
- Strong isolation

Threads:

- Shared memory
- Faster switching
- Lower overhead

Advantages of threads:

- Efficient communication via shared memory

Disadvantage:

- Shared data may cause **conflicts**.

---

# 6. Critical Sections

Shared resources cannot be accessed simultaneously by competing processes.

A **critical section** is code that must be executed with **mutual exclusion**.

---

# Protecting Critical Sections

Examples from everyday life:

- Railroad signals
- Traffic lights
- Room locks
- Ticket distribution

In software:

**Semaphores** are commonly used.

---

# Mutual Exclusion

Critical section protection ensures:

- Only one process enters a region at a time.

Example problem:

**Reader–Writer Problem**

- Multiple readers allowed
- Writer requires exclusive access

![[Pasted image 20260304180725.png]]

---

# Critical Section Example

Two processes accessing a shared buffer:

- Sensor data producer
- Data plotting consumer

![[Pasted image 20260304180741.png]]

---

# Requirements for Mutual Exclusion

A correct solution must satisfy:

1. Only one process enters the critical section
2. No assumptions about processor speed or number
3. Processes outside critical sections must not block others
4. Waiting time must be finite

---

# 7. Resource Access Protocols

Protocols for managing shared resources:

- Non-Preemptive Protocol (NPP)
- Highest Locker Priority (HLP)
- Priority Inheritance Protocol (PIP)
- Priority Ceiling Protocol (PCP)

---

# Resource Definition

A **resource** is any structure used by processes:

Examples:

- Data structures
- Variables
- Memory regions
- Files
- Device registers

Types:

- Private resource
- Shared resource
- Exclusive resource (protected)

---

# Semaphores

Semaphores are kernel data structures.

Operations:

- `wait(S_k)`
- `signal(S_k)`

Rules:

- Each exclusive resource has a semaphore
- Critical section starts with `wait()` and ends with `signal()`
- Each semaphore maintains a process queue.

![[Pasted image 20260304182855.png]]

---

# Synchronization Example

Processes synchronize access to a shared buffer using semaphores.

![[Pasted image 20260304182908.png]]

---

# 8. Concurrency Problems

## Race Conditions

Occurs when multiple threads read/write shared data.

Result depends on execution order.

Solution:

- Critical sections
- Mutual exclusion

---

## Starvation

A process is indefinitely denied required resources.

Solution:

- Fair waiting queues.

---

## Priority Inversion

A high-priority task waits for a low-priority task holding a resource.

---

# 9. Non-Preemptive Protocol (NPP)

Properties:

- No preemption allowed during critical sections
- Process entering critical section receives highest priority

Priority assignment:

$$
p_i(R_k) = \max_h \{P_h\}
$$

Priority resets after leaving the critical section.

![[Pasted image 20260304182921.png]]

---

# Blocking Time (NPP)

Assume:

$$
P_i > P_j
$$

Blocking time:

$$
B_i = \max \{ \delta_{j,k} \}
$$

Meaning:

A task can be blocked by the **longest critical section of a lower priority task**.

![[Pasted image 20260304183013.png]]

---

# 10. Highest Locker Priority Protocol (HLP)

When a process locks resource $R_k$:

It receives the **highest priority among processes using that resource**.

Dynamic priority:

$$
p_i(R_k) = \max_h \{P_h \mid T_h \text{ uses } R_k \}
$$

Simplified version:

Assign a **priority ceiling**:

$$
C(R_k) = \max_h \{P_h \mid T_h \text{ uses } R_k \}
$$

Process receives priority $C(R_k)$ during critical section.

![[Pasted image 20260304183038.png]]

---

# 11. Priority Inheritance Protocol (PIP)

Idea:

If a high-priority process is blocked by a lower-priority process:

The blocking process **inherits the higher priority**.

Priority rule:

$$
p_j(R_k) =
\max \left\{ P_j,\; \max_h \{P_h \mid T_h \text{ blocked on } R_k \} \right\}
$$

After leaving the critical section:

Priority returns to normal.

Priority inheritance is **transitive**.

![[Pasted image 20260304183100.png]]

---

## Blocking Types

### Direct Blocking

High-priority task waits for a lower-priority task holding a resource.

---

### Push-Through Blocking

Medium-priority task blocked because a lower-priority task inherited a higher priority.

---

# Transitive Priority Inheritance

If:

- $T_3$ blocks $T_2$
- $T_2$ blocks $T_1$

Then:

$$
T_3
$$

inherits the priority of

$$
T_1
$$

📌 Copy diagram on slide 58.

---

# 12. Deadlocks

Deadlocks occur when tasks wait for each other's resources.

Example:

```
T1: wait(Sa) → wait(Sb)
T2: wait(Sb) → wait(Sa)
```

Neither process can proceed.

![[Pasted image 20260304183110.png]]

---

# 13. Priority Ceiling Protocol (PCP)

Goal:

Prevent:

- Priority inversion
- Deadlocks
- Chained blocking

Rules:

1. Each resource has a **priority ceiling**.
2. A process may enter a critical section only if its priority is higher than the ceilings of all locked semaphores.

Example:

If

$$
C(a) = P_1,\quad C(b) = P_1,\quad C(c) = P_2
$$

then tasks must respect these ceilings.

![[Pasted image 20260304183129.png]]

---

# Comparison of Protocols

| Protocol | #Blocking | Pessimism | Blocking Instant | Transparency | Deadlock Prevention | Implementation |
|--------|--------|--------|--------|--------|--------|--------|
| NPP | 1 | High | On arrival | Yes | Yes | Easy |
| HLP | 1 | Medium | On arrival | No | Yes | Easy |
| PIP | >1 | Low | On access | Yes | No | Hard |
| PCP | 1 | Medium | On access | No | Yes | Medium |

Transparent protocols:

- NPP
- PIP

These work with standard semaphore primitives.

Protocols using ceilings:

- HLP
- PCP

Require additional system calls.

---

# Literature

- Giorgio C. Buttazzo – *Hard Real-Time Computing Systems*
- Ungerer et al. – Survey of Processors with Explicit Multithreading
- Agarwal – *Performance Tradeoffs in Multithreaded Processors*