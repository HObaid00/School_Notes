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

## Links

[[Edge Computing & IoT]]