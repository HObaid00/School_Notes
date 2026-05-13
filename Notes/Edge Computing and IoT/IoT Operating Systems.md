# IoT Operating Systems

An **IoT operating system** is an operating system designed for small, low-power, memory-constrained devices.

Unlike desktop operating systems, IoT operating systems are optimized for:

- Low RAM usage
- Low flash usage
- Low energy consumption
- Hardware interrupts
- Sensor and radio access
- Real-time or near-real-time behavior

Examples include TinyOS, RIOT, Contiki, FreeRTOS, Zephyr, Apache Mynewt, and embedded Linux variants.

The main design problem is that many IoT devices cannot afford the heavy abstractions used by normal PC operating systems.

---

## Constrained Device Classes

IoT devices can be grouped by resource constraints.

| Class | Typical resources | Meaning |
|---|---|---|
| Class 0 | Very tiny RAM and ROM | Usually cannot run a full IP stack directly |
| Class 1 | Around tens of kB RAM and around 100 kB ROM | Can run small IoT OS and constrained networking |
| Class 2 | More capable embedded devices | Can support more complete protocols and applications |

The smaller the class, the more careful the software design must be.

A normal programming assumption such as "just create another thread" may be impossible on tiny devices because each thread needs memory for its stack.

---

## Reactive Processing

**Reactive processing** means that the system sleeps most of the time and only performs work when an event occurs.

The typical cycle is:

$$\Large
\text{sense} \rightarrow \text{process/react} \rightarrow \text{communicate} \rightarrow \text{sleep}
$$

In wireless sensor networks, processing is usually triggered by:

- A timer event
- A sensor interrupt
- A received radio packet
- A button press
- A hardware interrupt

This is different from a normal desktop program that may run continuously or rely on periodic scheduling.

Reactive processing saves energy because the CPU and radio can sleep whenever there is no useful work.

---

## Interrupts, Callbacks, and Delegates

In a reactive system, hardware events are often handled through **interrupts** and **callbacks**.

An interrupt is a signal from hardware that tells the CPU: "something important happened".

A callback is a function registered by the application so the operating system can call it when a specific event occurs.

Example idea:

```c
on_temperature_ready(reading) {
    process(reading);
}

```

The application registers `on_temperature_ready`, then the OS calls it when the sensors has data.

This model avoids creating a separate thread for every event. It is efficient, but callbacks must be short because long callbacks can delay other events.

---

## Run-to-Completion Model

In the **run-to-completion** model, an event handler starts, executes its work, and finishes before the next event handler runs.

This simplifies concurrency because two handlers are usually not modifying the same data at exactly the same time.

The advantage is simpler programming:

$$\Large
\text{no simultaneous handlers} \Rightarrow \text{less need for locks}
$$

The disadvantage is that a long-running handler can block later events.

Example: If a sensor callback performs a long network operation, incoming radio packets may be delayed or lost. Therefore, event handlers should usually do minimal work and schedule longer work separately.

---

## Scheduling vs Reactive Operating Systems

A traditional operating system often uses **scheduling**: it decides which process or thread runs at a given time.

A reactive IoT OS often avoids full preemptive scheduling and instead processes events from an event queue.

| Model | How work starts | Advantage | Disadvantage |
|---|---|---|---|
| Reactive | Event occurs | Energy efficient, simple | Long handlers reduce responsiveness |
| Scheduled | Scheduler chooses task | Better multitasking | More memory and synchronization overhead |

Preemptive scheduling can interrupt one task to run another. This improves responsiveness but makes programs harder to reason about because shared data may change unexpectedly.

---

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