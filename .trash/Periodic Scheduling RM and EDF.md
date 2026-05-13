## Periodic Scheduling: RM and EDF

Periodic real-time systems often run tasks with deadlines. Two classic scheduling algorithms are **Rate Monotonic (RM)** and **Earliest Deadline First (EDF)**.

**Rate Monotonic** assigns higher priority to tasks with shorter periods.

**Earliest Deadline First** dynamically gives priority to the task whose deadline is earliest.

A simple task utilization formula is:

$$\Large
U = \sum_i \frac{C_i}{T_i}
$$

where $C_i$ is the computation time of task $i$, and $T_i$ is its period.

If utilization is too high, tasks may miss deadlines.

In IoT, periodic scheduling is useful for regular sampling, but event-driven processing is often better for energy saving.

---

## Links

[[Edge Computing & IoT]]