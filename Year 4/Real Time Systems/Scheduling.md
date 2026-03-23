# Real-Time Systems  
## Part 6: Scheduling

TUM School of CIT – Chair of Robotics, Artificial Intelligence and Real-Time Systems (I6)

---

# Task Execution Model

Task states:

- READY
- RUN
- WAIT

Transitions:

- activation
- dispatching
- preemption
- signal wait

![[Pasted image 20260304170906.png]]

---

# 1. Scheduler and Dispatcher

## Scheduler

The **scheduler** performs resource allocation.

Responsibilities:

- Assign CPU time to tasks
- Decide which task should execute next

---

## Dispatcher

The **dispatcher** executes the scheduler's decision.

Responsibilities:

- Perform **context switching**
- Switch to **user mode**
- Jump to the correct program location to resume execution

![[Pasted image 20260304170845.png]]

---

# 2. Scheduling Problems

Define:

- $T = \{T_1, T_2, ..., T_n\}$ → set of processes/tasks
- $P = \{P_1, P_2, ..., P_n\}$ → set of processors
- $R = \{R_1, R_2, ..., R_n\}$ → set of resources

Goal:

Assign processors from P and resources from R to processes from T in order to complete all processes under the specified constraints

---

# 3. Task Constraints

Typical constraints:

- **Timing constraints** (deadlines)
- **Precedence constraints**
- **Resource constraints**

---

# 4. Temporal Characterization of Tasks

For task $T_i$:

- $a_i$ – arrival time (release time)
- $s_i$ – start time
- $f_i$ – finishing time
- $d_i$ – absolute deadline
- $C_i$ – computation time

---

## Derived Timing Metrics

### Relative Deadline

$$
D_i = d_i - a_i
$$

---

### Response Time

$$
R_i = f_i - a_i
$$

---

### Lateness

$$
L_i = f_i - d_i
$$

---

### Tardiness

$$
E_i = \max(0, L_i)
$$

---

### Slack Time (Laxity)

$$
X_i = d_i - a_i - C_i
$$

Other task attributes:

- Criticality (hard / firm / soft)
- Task value (importance)

---

# 5. Precedence Constraints

Tasks may depend on other tasks.

Represented using an **acyclic precedence graph**.

Example dependency chain:

- $T_1 \rightarrow T_2$
- $T_2 \rightarrow T_3$

![[Pasted image 20260304171124.png]]

---

# 6. Task Types

## Periodic Tasks

Released at regular intervals.

Example:

$$
T_i = (C_i, P_i)
$$

where $P_i$ is the period.

---

## Aperiodic Tasks

- Irregular arrival times
- No fixed period

---

## Sporadic Tasks

- Random arrival times
- Minimum inter-arrival time guaranteed

---

# 7. Scheduling Categories

Scheduling algorithms may be:

- **Preemptive** or **non-preemptive**
- **Static** or **dynamic**
- **Offline** or **online**
- **Optimal** or **heuristic**

---

# 8. Guarantee-Based Algorithms

## Hard Real-Time Systems

Characteristics:

- Often computed **offline**
- Use complex optimal algorithms
- No runtime scheduling overhead

Limitations:

- Inflexible
- Depend on accurate environment modeling

---

## Dynamic Real-Time Systems

Scheduling decisions occur at runtime.

Process:

1. Task arrives
2. **Acceptance test** performed
3. If schedulable → task accepted
4. Otherwise → task rejected

![[Pasted image 20260304171147.png]]

---

# Domino Effect

Adding a task may cause cascading deadline failures.

Result:

- System rejects the new task.

![[Pasted image 20260304171207.png]]

---

# 9. Scheduling Anomalies

Unexpected effects may occur when:

- Adding processors
- Reducing execution time
- Relaxing precedence constraints

These may **increase total completion time**.

![[Pasted image 20260304171300.png]]

---

# Key Insight

Seemingly beneficial improvements such as:

- Faster processors
- Additional CPUs
- Reduced execution times

may **increase overall completion time**.

This phenomenon is called **scheduling anomaly**.

---

# 10. Best-Effort Algorithms

Used for **soft real-time systems**.

Characteristics:

- Missed deadlines degrade performance
- Tasks are not rejected
- System tries to meet deadlines whenever possible

---

# 11. Aperiodic Task Scheduling

Aperiodic tasks:

- Have irregular arrival times
- May have soft or hard deadlines

---

# 12. Scheduling Problem Classification

Scheduling problems are often represented as:

```
a | b | c
```

Where:

- **a** → machine environment (number of processors)
- **b** → task/resource characteristics
- **c** → optimality criterion

Example:

```
3 | no_preem | Σ f_i
```

 Metrics for performance evaluation / cost functions:
 * average response time: $\bar{t}_r = \frac{1}{n}\sum_{i=1}^n(f_i - a_i)$
 * total completion time: $\max\limits_{i} (f_i) - \min\limits_{i} (a_i)$
 * weighted sum of completion times: $t_w = \sum_{i=1}^n w_i f_i$
 * maximum lateness: $L_max = \max\limits_i (f_i - d_i)$
 * maximum number of late tasks:  $N_{late} = \sum_{i=1}^n miss (f_i)$

---

# 13. Performance Metrics

## Average Response Time

$$
\bar{t_r} = \frac{1}{n}\sum_{i=1}^{n}(f_i - a_i)
$$

---

## Total Completion Time

$$
\max_i(f_i) - \min_i(a_i)
$$

---

## Weighted Completion Time

$$
t_w = \sum_{i=1}^{n} w_i f_i
$$

---

## Maximum Lateness

$$
L_{max} = \max_i(f_i - d_i)
$$

---

## Number of Late Tasks

$$
N_{late} = \sum_{i=1}^{n} miss(f_i)
$$

![[Pasted image 20260304175855.png]]

---

# 14. Utility Functions

Different real-time systems evaluate task completion differently.

Examples:

- Non-real-time
- Soft real-time
- On-time systems
- Firm real-time systems

![[Pasted image 20260304175908.png]]

---

# 15. Jackson's Algorithm (EDD)

Problem:

```
1 | sync | Lmax
```

Tasks arrive simultaneously.

Goal:

Minimize **maximum lateness**.

---

## Earliest Due Date Rule

Schedule tasks in **ascending order of deadlines**.

This strategy is **optimal** for minimizing lateness.

---

## Optimality Condition

A feasible schedule exists if:

$$
f_i \le d_i
$$

Worst-case finishing time:

$$
f_i = \sum_{k=1}^{i} C_k
$$

---

## Feasibility Condition

For hard real-time tasks:

$$
\sum_{k=1}^{i} C_k \le d_i
$$

Jacksons Algorithm:
![[Pasted image 20260304175953.png]]
![[Pasted image 20260304180001.png]]

---

# 16. Horn's Algorithm (EDF)

Problem:

```
1 | preem | Lmax
```

Tasks may arrive asynchronously.

Solution:

**Earliest Deadline First (EDF)**.

---

## EDF Rule

At every scheduling decision:

Execute the task with the **earliest absolute deadline**.

---

## Optimality

EDF minimizes **maximum lateness** for independent tasks.

Task definition:

$$
T_i = (a_i, C_i, d_i)
$$

![[Pasted image 20260304180142.png]]

---

# EDF Schedulability Test

Remaining execution time:

$$
f_i = \sum_{k=1}^{i} c_k(t)
$$

Feasible if:

$$
\sum_{k=1}^{i} c_k(t) \le d_i
$$

![[Pasted image 20260304180214.png]]

---

# 17. Non-Preemptive Scheduling Challenges

In non-preemptive systems:

- Tasks cannot be interrupted
- Idle time insertion may be required

However:

Arrival times must be known beforehand.

![[Pasted image 20260304180232.png]]

---

# Complexity of Scheduling

Brute-force search:

- Tree depth = $n$
- Possible schedules = $n!$

Complexity:

$$
O(n \cdot n!)
$$

This becomes impractical for large task sets.

---

# 18. Bratley's Algorithm

Problem:

```
1 | no_preem | feasible
```

Approach:

- Branch-and-bound search
- Prune branches when deadline violations occur

Branch is abandoned if:

- Deadline already missed
- A feasible schedule is found

![[Pasted image 20260304180300.png]]

---

# 19. Heuristic Scheduling Functions

Used to guide scheduling search.

Examples:

- **FCFS** – First Come First Served
- **SJF** – Shortest Job First
- **EDF** – Earliest Deadline First
- **ESTF** – Earliest Start Time First

Limitations:

- Not guaranteed optimal
- May miss feasible schedules

---

# 20. Static Scheduling with Precedence Constraints

Problem:

```
1 | PREC, SYNC | Lmax
```

Solution:

**Latest Deadline First (LDF)**.

Procedure:

- Build scheduling queue **from tail to head**
- Choose task with **largest deadline**

📌 Copy example on slide 52.

---

# EDF vs LDF

Example comparison:

- **EDF**: schedule by earliest deadline
- **LDF**: schedule backward by latest deadline

![[Pasted image 20260304180319.png]]

---

# 21. Dynamic Scheduling with Precedence Constraints

Problem:

```
1 | PREC, PREEM | Lmax
```

Steps:

1. Convert dependent tasks into independent tasks
2. Modify timing parameters
3. Apply **EDF scheduling**

---

## Parameter Transformation

Arrival time adjustment:

$$
a_2^* = a_1 + C_1
$$

Deadline adjustment:

$$
d_1^* = d_2 - C_2
$$

After transformation:

Apply **EDF (Horn's algorithm)**.

![[Pasted image 20260304180350.png]]

---

# 22. Comparison of Scheduling Algorithms

| Scenario | Algorithm | Optimal |
|--------|--------|--------|
| synchronous activation | EDD (Jackson) | Yes |
| asynchronous preemptive | EDF (Horn) | Yes |
| asynchronous non-preemptive | tree search | Yes |
| precedence constraints | LDF | Yes |
| dynamic precedence constraints | EDF* | Yes |
| heuristic search | heuristic tree search | No |
![[Pasted image 20260304180418.png]]

---

# Literature

Giorgio C. Buttazzo  
**Hard Real-Time Computing Systems**  
Springer, 3rd Edition, 2011