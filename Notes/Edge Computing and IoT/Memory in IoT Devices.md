# Memory in IoT Devices

Memory is one of the most important constraints in embedded IoT systems.

Common memory types are:

| Memory type | Volatile? | Typical use |
|---|---:|---|
| RAM | Yes | Variables, stacks, buffers |
| Flash | No | Program code and persistent data |
| EEPROM | No | Small persistent configuration data |
| ROM | No | Fixed code or data programmed during production |

**RAM** is usually the scarcest resource. A sensor node may have only a few kilobytes of RAM, so large buffers, many threads, and dynamic allocation can be dangerous.

Example: If a device has $8\,\text{kB}$ RAM, a few large packet buffers can already consume a significant part of memory.

---

## Links

[[Edge Computing & IoT]]