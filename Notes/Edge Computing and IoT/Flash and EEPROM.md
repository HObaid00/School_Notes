# Flash and EEPROM

**Flash memory** stores program code and persistent data even when power is removed. It is larger than EEPROM but has constraints:

- Writes are slower than reads.
- Cells tolerate only a limited number of writes.
- Erase operations often happen in pages, not individual bytes.
- Writing can often only change bits in one direction until an erase is performed.

**EEPROM** is also persistent but usually smaller. It can often erase individual cells and is useful for configuration values.

Design implication: Do not write frequently changing values to flash or EEPROM without wear management.

Example: A counter updated every second could wear out persistent memory quickly.

---

## Links

[[Edge Computing & IoT]]