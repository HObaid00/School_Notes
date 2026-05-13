# IoT Devices: Raspberry Pi vs ESP32

IoT courses often use both **Raspberry Pi** devices and **ESP32 microcontrollers** because they represent different points in the design space.

A **Raspberry Pi** is close to a small Linux PC. It can run a full operating system, web servers, databases, and many development tools.

An **ESP32** is a microcontroller. It is much more limited, but it consumes less power and is better suited for embedded sensing and actuation.

| Device type | Example | Best for |
|---|---|---|
| Linux single-board computer | Raspberry Pi | Gateway, local server, prototyping, edge node |
| Microcontroller | ESP32 | Battery-aware sensing, actuation, low-level hardware control |

The design trade-off is:

$$\Large
\text{more computing power} \Longleftrightarrow \text{more energy consumption}
$$

---

## Comparison Sheet

![[Pasted image 20260511173534.png]]

---

## Links

[[Edge Computing & IoT]]