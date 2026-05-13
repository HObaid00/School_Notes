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

## Links

[[Edge Computing & IoT]]
