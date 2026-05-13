# Timers, OS Jobs, and Sleeping

In embedded systems, timers and the OS cooperate to save energy.

The OS keeps track of pending jobs. The HAL checks when the next job must run and decides whether the microcontroller can sleep.

Possible decisions:

1. If the next job is extremely soon, stay awake and busy-wait.
2. If the next job is soon, sleep lightly while keeping timers running.
3. If the next job is far away, use a deeper sleep mode and a coarser timer setup.

The goal is:

$$\Large
\text{sleep as deeply as possible, but still wake up on time}
$$

This is central for long battery life.

---

## Links

[[Edge Computing & IoT]]