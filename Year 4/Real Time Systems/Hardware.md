# Real-Time Systems  
## Part 3: Embedded Hardware

TUM School of CIT – Chair of Robotics, Artificial Intelligence and Real-Time Systems (I6)

---

# 1. Embedded Computing Systems

## Categories

- General purpose computers  
  - Extended with appropriate HW/SW  
  - Desktop / Laptop / Single Board Computer  

- Microcontrollers / Microcontroller Boards  
- DSP (Digital Signal Processor)  
- FPGA  
- (GPUs intentionally excluded)

---

# 2. Microprocessor vs. Microcontroller

---
## Microprocessor

Core components:

- Control Unit (CU)
- Arithmetic Logic Unit (ALU)
- Registers

Only CPU core is integrated.  
External components required:

- RAM
- Storage
- I/O interfaces
- System bus

![[Pasted image 20260303190137.png]]

---

## Microcomputer System

A microprocessor embedded into a full system including:

- RAM
- Graphics
- PCIe
- USB
- SATA
- Ethernet
- Chipset

![[Pasted image 20260303190157.png]]

---

## Microcontroller for Real-Time Computing

Integrated on one chip:

- Processor core
- RAM
- Flash
- Clock
- System bus
- Peripherals (SPI, I2C, CAN, ADC, DAC, PWM, etc.)

![[Pasted image 20260303190224.png]]

---

# 3. Single Board Computers (SBC)

## With Microcontroller

Example:
- STM NUCLEO F767ZI
- ARM Cortex-M core

Use cases:
- Prototyping → evaluation boards
- Large scale production → custom PCB
- Medium scale → trade-offs

---

## Example: ESP32

- 240 MHz
- 512 kB SRAM
- 4 MB ROM
- WiFi + Bluetooth
- UART / I2C / SPI / DAC / ADC
- ~10€

Alternative:
- Ubuntu 22.04 with RT Kernel patch

---
## Custom SBC with Microcontrollers

Used in robotics and industrial systems.

---

# 4. Example: dsPIC33F (Microchip)

- 16-bit devices
- Modified Harvard architecture
- 3.3V operation (5V tolerant I/O)
- 40 MIPS @ 80 MHz
- On-chip Flash, EEPROM, SRAM
- Digital I/O, Analog inputs
- Timers, PWM, encoder
- UART, CAN, SPI

---

## Same Silicon – Different Packages

- Thin quad flat pack (TQFP)
- MicroLeadFrame™
- Dual in-line package (DIP)

Same silicon, different packages

---

## Block Diagram

Internal interconnections between:

- CPU
- Buses
- ADC
- Timers
- CAN
- PWM
- Memory

![[Pasted image 20260303195325.png]]

---

## Independent Hardware Peripherals

CPU communicates with peripherals via memory-mapped dual-ported RAM.

Examples:
- CAN
- 10-bit ADC
- Input capture
- Output compare
- I²C
- SPI
- Timers
- QEI
- UART

![[Pasted image 20260303195415.png]]

---

# 5. Microprocessor vs. Microcontroller (Comparison)

| Feature | Microprocessor | Microcontroller |
|----------|----------------|----------------|
| Application | General computing | Appliances, specialized |
| Speed | Very fast | Slower |
| External parts | Many | Few |
| Energy use | High | Low |
| Cost | High | Low |
| Vendors | Intel, AMD | ST, TI, Microchip |

---

# 6. DSP – Digital Signal Processor

Optimized for:

- MAC operations
- Filtering
- Control algorithms
- Frequency analysis

Features:
- x/y memory
- Barrel shifter
- Special instructions

Hybrid version:
- Digital Signal Controller

---

# 7. ASIC – Application Specific Integrated Circuit

- Fully application-specific hardware
- Cannot be changed after manufacturing
- High development cost
- Economical only for large quantities
- Developed using VHDL

Once fabricated:
- Functionality fixed

* Micro-controllers, DSP processors, general purpose processors and memories are examples of an ASIC.
* However, many ASICS are also hidden devices within embedded systems and not for general sale.
* Once an ASIC (or the Intel core-i7) is manufactured, its functionality is fixed and cannot be changed anymore.


---

# 8. FPGA – Field Programmable Gate Array

Bridges gap between:

- Microprocessors/DSP
- ASIC

Characteristics:

- Look-up tables + flip-flops
- Configurable via VHDL / Verilog
- Used for prototypes / low volume
- Soft-core processors available

---

## ASIC vs FPGA

ASIC:
- Low unit cost (high volume)
- High upfront cost
- Fixed design

FPGA:
- Fast time-to-market
- Field programmable
- Higher unit cost

![[Pasted image 20260304145122.png]]

---

# 9. PSoC Example (Cypress/Infineon)

Example: PSoC 5LP

- ARM Cortex-M3 (up to 80 MHz)
- DMA controller
- Digital filter processor
- Programmable digital & analog peripherals
- ADC, DAC, OpAmp, filters
- Flexible routing

---

# 10. Embedded Systems Applications

- Household appliances
- Entertainment electronics
- Communication systems
- Healthcare
- Automotive
- Industrial automation
- Ubiquitous computing

---

# 11. Requirements for Embedded Systems

- Interface requirements
- Mechanical requirements
- Electrical requirements
- Reliability requirements
- Real-time requirements

---

# 12. Real-Time Requirement

Worst Case Response Time:

$$
\text{WCRT} = \text{WCET} + \text{latency}_1 + \text{latency}_2
$$

Example:
> Brakes must be applied within 30 ms from pedal force.

![[Pasted image 20260304145154.png]]

---

# 13. Temporal Determinism vs Performance

Mechanisms problematic for RT:

- Virtual memory
- Asynchronous I/O
- Recursive functions
- Speculative execution
- Branch prediction
- Caches

---

## Branch Prediction

- Loads most likely branch
- Flushes pipeline on misprediction

---

## Caches

- Improve average performance
- Cache miss → stall
- Difficult for WCET analysis

---

# 14. Performance Metrics

- MIPS – Millions of Instructions per Second
- MFLOPS – Millions of Floating Point Operations per Second
- SPEC benchmarks

---

# 15. Summary

Hard real-time requires:

- Cycle-countable hardware
- Predictable timing
- Known resource requirements

---

# 16. PLC (Programmable Logic Controller)

German: SPS

- Factory automation
- 24V typical
- Modular or compact
- Communication buses: PROFINET, EtherCAT, CANopen
- Programming:
  - Ladder logic
  - Function block diagram
  - Structured text
  - EN 61131

![[Pasted image 20260304145244.png]]

---

# 17. Processor Architecture

Defines:

- Data representation
- Data storage
- Operations
- Instruction format
- Data access

---

# 18. Data Representation

Bus widths:
- 8-bit
- 16-bit
- 32-bit
- 64-bit

Assembler abbreviations:
- B (byte)
- H (halfword)
- W (word)
- D (double word)

---

## IEEE 754 (32-bit floating point)

Structure:
- 1 sign bit
- 8 exponent bits
- 23 fraction bits

Example (slide 45):

Hex:
```
0x3E200000
```

---

# 19. Address Space Organization

- Registers (general, floating point, special)
- Single address space:
  - Memory
  - Stack
  - Heap
  - I/O

---

# 20. Instruction Set

Types:

- Data movement
- Arithmetic & logic
- Shift/rotate
- Floating point
- Control transfer
- System control

Instruction format examples:

3-address:
```
ADD R3, R1, R2
```

2-address:
```
LOAD R1, A
```

---

# 21. RISC vs CISC

## RISC (ARM)

- Simple instructions
- Fixed length (32-bit)
- Few addressing modes
- Load/store architecture
- Deterministic timing

## CISC (x86)

- Complex instructions
- Variable timing
- Difficult for RT analysis

---

# 22. Addressing Modes

- Immediate:
  ```
  ADD R1, #6
  ```

- Direct:
  ```
  LOAD R1, @100
  ```

- Register indirect:
  ```
  LOAD R2, @R1
  ```

---

# 23. Memory Architecture

## Memory Map

32-bit address space:

$$
2^{32} \text{ Bytes} = 4\text{ GB}
$$

Includes:
- Flash
- RAM
- Peripherals

---

## Stack (LIFO)

Function call:

1. Push parameters
2. Push return address
3. Push locals

Returning local variable address → undefined behavior.

---

## Heap

- Dynamic memory (malloc/new)
- Fragmentation problematic
- Garbage collection problematic
- Avoid in hard RT systems

---

# 24. CPU Operation

Two phases:

1. Fetch / Decode
2. Execute

Fetch cycle:

- AR ← PC
- DR ← M
- IR ← DR

![[Pasted image 20260304145319.png]]

---

# 25. Pipeline

5 stages:

1. Fetch
2. Decode
3. Execute
4. Memory access
5. Write-back

Hazards:

- Resource hazard
- Data hazard
- Control hazard

Pipeline + branch prediction complicate WCET.

---

# 26. Interrupts

Mechanisms:

- Polling
- Interrupts

Polling:
- High CPU usage
- Predictable

Interrupt:
- Efficient
- Non-deterministic interruption

---

## ISR Rules

- Must preserve processor state
- Use `volatile` for shared variables
- Can occur between any two instructions

Example:

```c
volatile uint32 counter = 0;

void ISR(void) {
    counter++;
}
```

---

# 27. I/O Interfaces

## GPIO

- Digital input/output
- Pull-up/pull-down required

![[Pasted image 20260304145943.png]]

![[Pasted image 20260304150011.png]]

Switch bounce visible at high resolution.

![[Pasted image 20260304150040.png]]

---

## ADC

- Sample & hold
- Anti-aliasing filter required

Nyquist:

$$
f_{sample} > 2 f_{signal}
$$

---

## PWM

Duty cycle:

$$
D = \frac{t_{on}}{t_{on} + t_{off}}
$$

Frequency choice:
- Too low → ripple
- Too high → EMC issues

![[Pasted image 20260304150158.png]]

---

# 28. Sensors

- Accelerometer
- Gyroscope
- Strain gauge
- Encoder
- Motor driver

---

## Encoder

Quadrature encoder:
- Two phase-shifted signals
- Direction detection via up/down counter

![[Pasted image 20260304151957.png]]

![[Pasted image 20260304152018.png]]

---

## H-Bridge

Used to drive motors.

- Allows polarity switching
- Requires free-wheeling diodes
- Driven by PWM
- MOSFET switches

![[Pasted image 20260304152036.png]]

---

# Literature

- Blaauw – Computer Architecture
- Gordon Bell – Computer Engineering
- Lee & Seshia – Introduction to Embedded Systems
- Hennessy & Patterson – Computer Architecture
- T.R. Padmanabhan – Introduction to Microcontrollers

---

# Questions

- Difference between microprocessor and microcontroller?
- Benefits/drawbacks of polling vs interrupts?
- What does a processor architecture define?