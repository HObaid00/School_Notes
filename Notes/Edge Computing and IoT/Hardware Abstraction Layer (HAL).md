# Hardware Abstraction Layer (HAL)

A **Hardware Abstraction Layer (HAL)** hides low-level hardware details behind a cleaner software interface.

Without a HAL, application code must directly manipulate registers, interrupts, timers, and device-specific behavior. With a HAL, the application can use higher-level operations such as:

```c
sensor_read();
radio_send(packet);
timer_set(deadline);
```

A typical embedded stack is: 

$$\Large
\text{hardware} \rightarrow \text{HAL} \rightarrow \text{runtime / OS} \rightarrow \text{libraries} \rightarrow \text{application}
$$

Not every IoT system has all these layers. Very small systems may merge layers to save memory.

---

## Links

[[Edge Computing & IoT]]
