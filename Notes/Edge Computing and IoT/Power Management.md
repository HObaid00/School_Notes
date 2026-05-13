# Power Management

**Power management** is the process of reducing energy use by switching hardware into lower-power states whenever possible.

Microcontrollers often support modes such as:

- Active mode
- Idle mode
- Standby mode
- Power-save mode
- Deep sleep mode

The deeper the sleep mode, the lower the power consumption, but the longer or more complex the wake-up process may be.

A typical average-energy calculation is:

$$\Large
E_{total} = E_{sleep} + E_{sense} + E_{process} + E_{radio}
$$

For battery-powered IoT, the design should minimize both active time and unnecessary wake-ups.

---

## Links

[[Edge Computing & IoT]]
