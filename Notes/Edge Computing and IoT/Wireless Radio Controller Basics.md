# Wireless Radio Controller Basics

A wireless radio is often one of the most energy-expensive parts of an IoT device.

Typical radio states include:

- Off
- Sleep
- Idle
- Receive
- Transmit

State transitions take time and energy. For example, waking the radio from sleep may require oscillator startup and synchronization before receiving or transmitting is possible.

A simple energy model is:

$$\Large
E = P \cdot t
$$

where $E$ is energy, $P$ is power, and $t$ is time.

Even if transmission is short, frequent wake-ups can dominate the total energy budget.

---

## Links

[[Edge Computing & IoT]]
