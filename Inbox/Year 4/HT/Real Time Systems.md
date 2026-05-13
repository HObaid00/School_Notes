## Organisation

This lecture covers:

- **IN2060 – Real-Time Systems**
- **IN8014 – Embedded Networked Systems**

- Lecture: Thursday, 16:00–18:00  
  Hörsaal 2, "Interims II" (5416.01.003), Campus Garching  
- Exercises: 18:15–19:30 (starting mid November)  
- No pre-recorded videos from last winter term  
- Material available via **Moodle (moodle.tum.de)**  


---

## Exam

- Exam date: ~12.02.2026 (subject to change; check TUMonline)
- Resit exam: likely mid August 2026

---

## BBC micro:bit

Features:

- 32-bit ARM Cortex M0
- 25 LED matrix
- Status LED
- 2 buttons
- Reset button
- 20-pin header
- 3-axis accelerometer
- 3D magnetometer
- Bluetooth
- Battery connector
- Dimensions: 40 × 50 mm
- Weight: 8 g

Limited number available on loan.  
Available at Reichelt (~27 EUR).  
Alternative hardware allowed.

---

## Measurements in Embedded Real-Time Systems

Oscilloscopes are essential for:

- Measuring fast-changing analog/digital signals
- Verifying software timing behavior

Example tasks:
- Blink LED at 50 Hz → measure:
  - Period
  - Jitter
  - Voltage levels
  - Current
  - Rise time
- Debug SPI communication:
  - Clock
  - Data
  - Chip Select
  - Polarity
  - Drift
  - Signal levels

Cost: 300 – 30,000 EUR+

---

## Lecture Contents

1. Introduction to Real-Time Systems  
2. Time and Clocks  
3. Hardware  
4. Communication  
5. Real-Time Operating Systems  
6. Concurrency / Processes  
7. Scheduling  
8. Real-Time Programming Languages  
9. Fault-Tolerant Systems  
10. Modelling / Tools  
11. Control Engineering (briefly)

---

# Chapter 1: Introduction to Real-Time Systems

## Content

- Definition of real-time system
- Classification
- Modeling, design, analysis
- Semi-complex example
- Real-time systems in daily life

---

## Convention

- Time is a property of the physical world.
- Influencing environment with computers → cyber-physical / real-time systems.
- Computers embedded into physical processes → embedded systems.

---

## Definition: Embedded System

A computer system with a dedicated function within a larger mechanical or electrical system, often with real-time constraints.

Characteristics:
- Integrated into a complete device
- Limited processing power
- Limited storage
- Cost-optimized hardware

---

## Definition: Real-Time Computer System (Kopetz)

A computer system where correctness depends on:

- Logical correctness **AND**
- The physical time at which the result is produced.

A real-time computer system is part of a larger **real-time / cyber-physical system**.

---

## Definition: Cyber-Physical System (Lee/Seshia)

Integration of computation with physical processes.

- Embedded computers and networks monitor and control physical processes.
- Behavior determined by cyber + physical components.
- Computation takes time.
- As physical processes are time-dependent, we use:
  
> cyber-physical system ≈ real-time system

---

## What Is Special About Real-Time Systems?

- Integration of computation and physical processes
- Measurement and manipulation over time
- Correctness depends on timing
- Computing time is not detached from physical time

---

## Nomenclature

- Operator cluster → Human operator
- Computational cluster → Real-time computer system
- Controlled cluster → Physical plant/machine

Interfaces:
- Human-machine interface
- Instrumentation interface
- Sensors / actuators

![[Pasted image 20260303183948.png]]

---

## Deadlines

- **Deadline**: instant when result must be produced
- **Soft deadline**: result still useful after deadline
- **Firm deadline**: no utility after deadline
- **Hard deadline**: severe consequences if missed

Examples:
- Train crossing → hard
- Video streaming → soft/firm
- Email/web browsing → soft

---

## Real-Time Data

At time \( t \):

- System state defined by significant state variables
- Significant variables = **real-time entities (RT-entities)**

Observation:

$$
\text{Observation} = \langle \text{Name}, t_{obs}, \text{Value} \rangle
$$

Especially relevant in distributed systems.

---

## Sphere of Control

- Subsystem 1 can change RT-entity
- Subsystem 2 can observe RT-entity
- Representation and units must be considered

![[Pasted image 20260303184058.png]]

---

## Time Problems in Real-Time Systems

### Measurement Problems
- Discretization
- Clock drift
- Synchronization
- Time keeping

### Execution Problems
- Determinism
- Parallelism
- Process synchronization

Time is the only universal reference available everywhere.

---

## Resulting Properties

### Time Requirements
- Temporal accuracy (not too early, not too late)
- Guaranteed response times
- Event synchronization
- NOT about maximum speed

### System Characteristics
- Many I/O interfaces
- Fault tolerance required
- Often distributed

---

## Temporal Determinism vs Performance

Unpredictable performance optimizations may be disallowed:

- Cache
- Pipelines
- DMA (shared resource)
- Asynchronous I/O
- Recursive functions (e.g. factorial)

Determinism is often more important than average performance.

---

## Classification of Real-Time Systems

### By Consequence
- Hard real-time
- Soft real-time

### By Execution Model
- Time-triggered (periodic)
- Event-driven (aperiodic)

---

## Hard vs Soft Real-Time

### Soft Real-Time
- Deadline misses degrade service
- Example: Video streaming

### Hard Real-Time
- Deadline miss → severe consequences
- Example: Rocket control, traffic lights

---

## Execution Models

### Time-Triggered
- Static schedule
- Global clock required
- WCET estimation needed
- Deterministic behavior

### Event-Driven
- Triggered by events
- Dynamic scheduling
- Guaranteed response times required

---

# Modeling, Design and Analysis

## Modeling

- Representation of relevant system properties
- Continuous dynamics
- Discrete dynamics
- Hybrid systems
- State machines
- Concurrent models of computation

Tools:
- Pencil & paper
- Matlab / Simulink
- Ansys SCADE
- Ptolemy

---

## Design

Hardware:
- Processor
- Memory architecture
- I/O

Software:
- OS
- Concurrency
- Scheduling
- Code generation

---

## Analysis

- Invariants
- Reachability
- Model checking
- Execution time
- Fault tolerance

Formal specifications required.

---

# Real-Time Systems in Everyday Life

## Example: Car

### Engine Control
- Fuel & ignition timing
- Response times < 1 ms
- Traction control

### Airbag
- Sensor fusion (accelerometers, gyroscopes, etc.)
- Reaction time ≈ 1 ms
- Redundancy required

---

## Other Examples

- Elevator control
- Traffic lights
- Thermostat / HVAC
- Mobile phones
- Mobile robots
- Industrial automation
- Kitchen appliances

> Real-time does NOT mean “as fast as possible”.

---
# Lecture Part 2: Time and Clocks

---

# 1. What is Time?

Time can only be observed implicitly by the change of states in systems.

Historically:
- Time interval between two successive peaks of the Sun’s day
- One sun second ≈ 1/86400 of that range
- Second [s] is the SI unit of time
- Time is continuous

Timeline:
- past — presence — future

---

# 2. Computers and Time

Time must be **digitized (discretized)** for computer usage.

## Atomic Clock

- Based on hyperfine transition frequency of Cesium-133
- Definition:
  
  $$
  1\,\text{s} = 9\,192\,631\,770 \text{ periods}
  $$

- Deviation ≈ 1 second in 300,000 years

## Computer Clocks

- Based on quartz crystal oscillation
- Accuracy much lower:
  - ≈ 1 s/day (standard watches)

---

# 3. Digital Time in Computers

Discrete timeline:

- Indexed instants: \( i, i+1, i+2 \)
- Smallest unit: **granule**

![[Pasted image 20260303184419.png]]

---

# 4. Reminder: Definition Real-Time Computer System

A real-time computer system is one where correctness depends on:

- Logical result **and**
- The physical time at which the result is produced.

(Hermann Kopetz)

---

# 5. Definition Real-Time System / Cyber-Physical System

A real-time computer system is part of a larger real-time system.

Cyber-physical system:
- Integration of computation and physical processes
- Embedded computers monitor and control physical processes

---

# 6. Cluster Model of Real-Time Systems

Clusters:
- Operator cluster → Human operator
- Computational cluster → Real-time computer system
- Controlled cluster → Physical plant

The RT computer system must react to stimuli from its environment.

**Deadline:** instant when result must be produced.

![[Pasted image 20260303184503.png]]

---

# 7. Deadlines

- **Deadline:** instant when result must be produced
- **Soft deadline:** result still useful afterward
- **Firm deadline:** no utility afterward
- **Hard deadline:** severe consequences if missed

---

# 8. Purpose of Time Measurement

In cyber-physical systems:

- Derive physical states (e.g., speed from position change over time)
- Time-dependent actuator commands
- Enforce event ordering
- Fault analysis

---

# 9. Functional Requirements of RT Systems

Observations of RT-entities form a **real-time image** stored in an RT database.

Update models:
- Time-triggered (TT)
- Event-triggered (ET)

RT image is only temporally accurate depending on system dynamics.

![[Pasted image 20260303184819.png]]

![[Pasted image 20260303184842.png]]

![[Pasted image 20260303184902.png]]

---

# 10. Time Measurement in Computers

Digital clock:
- Counter incremented by periodic physical oscillation
- Frequency: \( f \) (microticks per second)
- Granularity:  

  $$
  g = \frac{1}{f}
  $$

Terminology:
- Microtick
- Granule

![[Pasted image 20260303184930.png]]

---

# 11. Time Standards

## International Atomic Time (TAI)

- Chronoscopic (no leap seconds)
- Epoch: Jan 1, 1958
- Problem: Astronomic day = 86400.002 s

## Coordinated Universal Time (UTC)

- Adjusted with leap seconds
- Not chronoscopic
- TAI ahead by ~37 s

## UNIX Time

- Seconds since Jan 1, 1970 (UTC)
- No leap seconds counted

---

# 12. Reference Clock (Thought Experiment)

Assume perfect reference clock \( z \).

Assign absolute timestamps:

$$
z(e)
$$

Used to evaluate other clocks.

---

# 13. Clock Errors

## Discretization Errors
- Granularity error
- Counter error (e.g., EMI, silicon faults)
- Drift

## Drift Rate

Perfect clock:
$$
\rho = 0
$$

Typical drift rates:

| Clock Type | Drift Rate [s/s] |
|------------|------------------|
| Quartz     | \(10^{-5}\) |
| Pendulum   | \(10^{-6}\) |
| Atomic     | \(1.5 \cdot 10^{-14}\) |

Drift accumulates without resynchronization.

---

# 14. Temporal Model

Time:
- Infinite ordered set \( \{T\} \)
- Instants totally ordered
- Events occur at instants
- Events have no duration

Relations:
- \( p = q \) (simultaneous)
- \( p < q \)
- \( q < p \)

Mutually exclusive.

---

# 15. Causal Order

- Temporal order necessary but not sufficient
- Causal order stronger than temporal order

---

# 16. Distributed Clocks

Each node has a clock.

## Offset

Time difference between microticks:

$$
offset_i^{kl} = |z(microtick_i^k) - z(microtick_i^l)|
$$

## Precision

Maximum offset within ensemble:

$$
\Pi = \max_{t_1 \le i \le t_2} \left( \max_{1 \le k,l \le n} offset_i^{kl} \right)
$$

---

# 17. Accuracy vs Precision

## Precision
- Internal property
- Max difference between clocks

## Accuracy
- Offset relative to external reference

If all clocks have accuracy \( A \):

$$
\Pi \le 2A
$$

Reverse not necessarily true.

---

# 18. Internal Clock Synchronization

Parameters:

- \( R_{int} \): resynchronization interval
- \( \Phi \): convergence function
- \( \Gamma \): drift offset

Condition:

$$
\Phi + \Gamma \le \Pi
$$

![[Pasted image 20260303185022.png]]

---

# 19. Byzantine Errors

Arbitrary faulty behavior.

Synchronization possible only if:

$$
N \ge 3k + 1
$$

Where:
- \( N \): total clocks
- \( k \): faulty clocks

(Lamport & Smith, 1985)

![[Pasted image 20260303185045.png]]

---

# 20. Global Time of an Ensemble

If precision \( \Pi \) holds:

Use every \( n \)-th microtick as macrotick.

Reasonableness condition:

$$
g > \Pi
$$

Bound:

$$
|t^k(e) - t^l(e)| \le 1
$$

---

# 21. Fundamental Limits of Time Measurement

1. Time stamps may differ by 1 tick.
2. True interval bounded by:

   $$
   (d_{obs} - 2g) < d_{true} < (d_{obs} + 2g)
   $$

3. Temporal order recoverable if difference ≥ \( 2g \).

---

# 22. Central Master Synchronization

Clock deviation:

$$
\delta t = |t_M - (t_S + t_{latency})|
$$

Precision:

$$
P_{central} = e + \Gamma
$$

Not fault tolerant.

![[Pasted image 20260303185114.png]]

---

# 23. Fault-Tolerant Synchronization

Phases:
1. Acquire global time counters
2. Error detection + compute correction
3. Adjust local clock

Lower bound precision:

$$
P = e \left(1 - \frac{1}{N}\right)
$$

(Lundelius & Lynch, 1984)

---

# 24. Cristian’s Algorithm

Procedure:
- Client requests time from server
- Server replies with timestamp \( T \)
- Client sets time:

$$
T + \frac{t_r}{2}
$$

Assumes symmetric delay.

![[Pasted image 20260303185157.png]]

---

# 25. State vs Rate Correction

## State Correction
- Immediate adjustment
- Risk: time discontinuities

## Rate Correction
- Adjust clock speed
- Change microticks per macrotick

---

# 26. External Clock Synchronization

Global time linked to external reference.

Time gateway:
- Receives external time
- Forwards correction to cluster

---

# 27. IEEE 1588 (PTP)

Precision Time Protocol.

Assumes symmetric delay.

Transit time:

$$
T_{transit} = \frac{1}{2}(T'_2 - T_2 - T_1 + T'_1)
$$

Offset:

$$
\Delta T = T_1 - T'_1
$$

Overall correction:

$$
T_{slave,new} = T_{slave} + T_{transit} + \Delta T
$$

![[Pasted image 20260303185341.png]]

---

# 28. Network Time Protocol (NTP)

- Developed by David Mills
- Synchronizes within milliseconds of UTC
- Stratum hierarchy (0–15)

Delay:

$$
\delta = (t_4 - t_1) - (t_3 - t_2)
$$

Offset:

$$
\theta = \frac{(t_2 - t_1) + (t_3 - t_4)}{2}
$$

Gradual frequency correction (no jumps).

---

# 29. DCF77

German longwave time signal:
- 77.5 kHz
- Located in Mainflingen
- Amplitude modulated

![[Pasted image 20260303185424.png]]

---

# 30. GPS

- Developed by US DoD
- PPS (military), SPS (civilian)
- Trilateration
- cm-level accuracy with DGPS

---

# 31. Application Example: High-Speed Printing

- Paper speed up to 100 km/h
- Multi-color stations synchronized
- Deviation < 1 mm
- Achieved via synchronized clocks

---
# Lecture 3: Embedded Hardware

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
# Lecture #4 Memory and Real-Time

---

# 1. CPU and Memory – Naïve View

CPU connected to off-chip memory (SRAM, DDR2/3/4).

Signals:

- Address
- Data
- Control signals (CS, R/W, RAS, CAS, CLK)

![[Pasted image 20260304152207.png]]

---

# 2. Memory Hardware Issues

- Single large address space
- Multiple ICs implementing memory
- Different memory types:
  - Internal SRAM
  - External DRAM/SDRAM
  - Special Function Registers
  - Memory-mapped peripherals
  - Off-chip devices (e.g., displays)

## Address Decoding

Goal: generate **Chip Select (CS)** from address lines.

![[Pasted image 20260304152223.png]]

---

# 3. Simple Address Decoding Example

Given:

- 10 address lines
- 8-bit data bus
- Total memory: 1 KiB
- Individual chips: 128 bytes

Since:

$$
8 \times 128\text{ B} = 1024\text{ B} = 1\text{ KiB}
$$

We need 8 chips.

- 7 LSBs → internal chip address
- 3 MSBs → decoder → 8 CS signals

![[Pasted image 20260304152250.png]]

Example address ranges:

- Memory 0: 0x000 – 0x07F
- Memory 1: 0x080 – 0x0FF
- Memory 2: 0x100 – 0x17F
- Memory 3: 0x180 – 0x1FF

Example CS logic:

$$
CS_0 = \neg(\neg A7 \land \neg A8 \land \neg A9)
$$

---

# 4. Cache – Motivation

Modern processors use deep memory hierarchies:

- L1 hit: ~5–7 cycles
- L1→L2→L3 miss: up to 1000 cycles

Hierarchy:

- L1 cache
- L2 cache
- L3 cache
- Off-chip memory (DDR)

Trade-offs:

- Speed ↑ closer to CPU
- Size ↑ further away
- Cost per byte ↓ further away

![[Pasted image 20260304153547.png]]

---

# Typical Cache Sizes

Example PC:

- L1: 32 KiB
- L2: 256 KiB
- L3: 10 MiB
- RAM: 16 GiB

---

# 5. Cache – Basic Operation

- Data transferred in **cache lines** (e.g., 16 bytes)
- Whole block copied on miss

![[Pasted image 20260304153628.png]]

---

# Locality

## Spatial locality

Accessing address A implies nearby addresses likely accessed.

## Temporal locality

Recently accessed data likely reused soon.

If access is random → cache effectiveness decreases.

---

# Address Structure Example

Assume:

- 32-bit address
- Cache line = 16 bytes

Offset bits:

$$
\text{offset} \in [0000, 1111]
$$

Address structure:

- Tag
- Offset

Reading one address copies full block into cache.

![[Pasted image 20260304153657.png]]

---

# Cache Line Structure

Each slot contains:

- Valid bit (1 bit)
- Dirty bit (1 bit)
- Tag
- Data block (e.g., 16 bytes)

Example (16-bit address, 16B line):

Total bits:

$$
1 + 1 + 12 + 16 \times 8 = 142 \text{ bits}
$$

To store 128 bits of data.

---

# Write Policies

## Write Through (WT)

- Write to cache AND lower memory
- More writes
- Simpler
- Higher energy

## Write Back (WB)

- Write only to cache
- Write to lower memory on eviction
- Requires dirty bit
- Fewer writes
- More complex

---

# 6. Direct Mapped Cache

Each memory block maps to exactly one cache line.

Analogy:

- 10 parking slots
- Student ID determines slot (last digit)

Simple but inefficient.

![[Pasted image 20260304153742.png]]

---

Example:

2 cache lines  
8 bytes per line  
Total size = 16 bytes

Address format:

- 1 bit → line
- 3 bits → offset
- Remaining bits → tag

Example:

Address 0x80 (1000 0000₂):

- Line = 0
- Offset = 0
- Tag = 1000₂

---

## Direct Mapping – Timing Example

Sequence:

- Read @0x80 → miss
- Read @0x98 → miss
- Read @0x78 → miss
- Write @0x80 → hit (dirty)
- Read @0x90 → miss (write-back)

Assume:

- Hit = 2 cycles
- Lower memory access = 8 cycles

Total:

$$
8 + 8 + 8 + 2 + (8 + 8) = 42 \text{ cycles}
$$

![[Pasted image 20260304153800.png]]

---

# Cache Replacement Policies

- LRU – Least Recently Used
- LFU – Least Frequently Used
- FIFO – First In First Out

---

# Fully Associative Cache

- Data can be placed in any cache line
- Requires parallel tag comparison
- Uses LRU/FIFO counters

Advantages:

- No conflict misses
- Better performance

Disadvantages:

- Complex
- Large hardware overhead

![[Pasted image 20260304153939.png]]

---

# Fully Associative (FIFO / Round Robin)

- Replacement pointer
- Only misses change pointer
- Hits do not affect pointer

Simpler than LRU.

![[Pasted image 20260304154006.png]]

---

# Set Associative Cache

Hybrid between direct and fully associative.

- Cache divided into sets
- Data maps to a set
- Can occupy any line inside set

Example:

- 4 lines
- 2 sets
- 2-way set associative

Only 2 lines compared per set.

![[Pasted image 20260304154027.png]]

8-way set associative ≈ behavior close to fully associative.

---

# Why Cache Analysis is Difficult

- Unknown memory addresses
- Unified instruction/data cache
- Timing anomalies:
  - Sometimes a cache hit increases execution time
- Cache state explosion

Reference: Reineke et al. – Timing Anomalies

---

# Cache Summary

- Direct mapped
- Fully associative
- Set associative
- Write-through vs write-back
- LRU vs FIFO

---

# 7. RAM and Timing

Storage delays vary significantly.

Non-determinism due to:

- Cache
- Memory technology
- Refresh
- Access direction changes

Relevant topic: WCET (Worst Case Execution Time)

---

# SRAM

- Static RAM
- No refresh
- Typically on-chip
- 6 transistors per bit
- Fast
- Large cell → less density
- No clock required

---

# SDRAM

Synchronous Dynamic RAM.

- Clocked
- Requires refresh
- Capacitor-based storage
- Large capacity
- Low cost
- Slower than SRAM
- Used after cache miss

DDR = Double Data Rate  
Transfers on rising + falling clock edge.

---

# SDRAM Architecture

- Data stored in banks
- Each bank has row buffer
- Row activation (ACT)
- Precharge (PCH)

If different row accessed:

1. Precharge current row
2. Activate new row

![[Pasted image 20260304154049.png]]

---

# SDRAM Timing Penalties

- ACT cost
- PCH cost
- Direction switch penalty (read ↔ write)

For WCET:

If row state unknown:

Assume worst-case penalty for every access.

---

# SDRAM Addressing Example (4MB)

22-bit address:

- 10 bits row (1024 rows)
- 1 bit bank (2 banks)
- 9 bits column (512 columns)
- 2 bits byte selection

![[Pasted image 20260304154142.png]]

---

# SDRAM Advantages / Drawbacks

Advantages:

- Large storage
- Low cost
- Enables advanced apps (camera, radar)

Drawbacks:

- Difficult WCET analysis
- Refresh interference
- Row buffer effects

---

# 8. Multi-Core Architectures

- AMP – Asymmetric multiprocessing
- SMP – Symmetric multiprocessing

---

# Cache Coherence Problem

Initial:

Core 1 loads value A = 42  
Core 2 loads value A = 42  

Core 1 increments A → 43  

Core 2 still sees 42 → stale data

![[Pasted image 20260304154232.png]]

---

# Cache Coherence – SWMR Invariant

Single-Writer Multiple-Reader (SWMR):

At any time:

- Either one core can write
- Or multiple cores can read

Token-based idea:

- If core has all tokens → write
- If core has ≥1 token → read

---

# Data Value Invariant

Value at start of epoch must equal value at end of last read-write epoch.

Correct value propagation required.

---

# Memory Consistency Problem

Example:

Core 1:
```
store data = new;
store flag = set;
```

Core 2:
```
load r1 = flag;
if (r1 != set) goto L1;
load r2 = data;
```

Question:

What value can `r2` observe?

Due to reordering, possible to observe stale values if no memory barriers are used.

---

# Summary

Memory hierarchy affects real-time behavior:

- Cache unpredictability
- SDRAM activation/precharge
- Refresh
- Direction switching
- Multi-core coherence and consistency

All significantly complicate WCET analysis.

---
#  Lecture 5: Real-Time Operating Systems

---

# 1. Introduction

## Motivation

Imagine a PC without an operating system (Windows, Linux, macOS):

- Programming such a system would be difficult.
- Even switching it on could already be problematic.

Bare-metal programming is therefore rarely done on general-purpose computers.

---

## Desktop Operating Systems

Typical features:

- Windows and graphical user interface
- File system
- Hardware abstraction
- Inter-process communication
- Scheduler

These components are normally hidden from application developers.

---

## Embedded Operating Systems

Embedded systems differ from desktop systems:

- Often **no user interface** (no screen or keyboard)
- **Limited resources** (memory, CPU)
- Must operate **continuously for long periods**
- Cross-compilation is common (PC → target device)
- Software updates may be difficult

---

# 2. Operating System – Basic Definition

Definition (Tanenbaum):

> The operating system controls all the computer’s resources and provides the base upon which the application programs can be written.

Two main roles:

## Extended Machine

- Provides an abstraction over hardware
- Hides technical details
- Simplifies programming

## Resource Manager

- Allocates CPU, memory, I/O resources
- Ensures orderly access
- Provides protection mechanisms

Key OS concepts:

- Processes
- Files
- System calls

---

# 3. User Space vs Kernel Space

Programs typically run in **user space**.

Characteristics:

- Limited access rights
- Cannot directly access hardware
- Must request OS services via **system calls**

The **kernel space**:

- Runs the OS kernel
- Has full access to hardware
- Manages system resources

Interaction between user space and kernel space occurs via **system calls**.

---

# 4. Embedded Real-Time System Without OS

Typical structure:

- Main loop executes application logic
- Interrupt Service Routines (ISRs) handle time-critical events

Characteristics:

- Simple architecture
- Limited scalability
- Time-critical work often placed in ISRs
- Requires careful distribution of workload

Issues:

- Hard to manage timing
- Difficult WCET analysis
- Increasing complexity as system grows

![[Pasted image 20260304154408.png]]

---

# 5. Embedded Real-Time System With RTOS

An RTOS introduces tasks and scheduling.

Features:

- Application divided into **tasks/threads**
- Tasks appear to run **in parallel**
- Kernel schedules tasks
- ISRs notify or trigger tasks

Advantages:

- Better modularity
- Easier work distribution
- Improved timing control

![[Pasted image 20260304154427.png]]

---

# 6. Threads vs Processes

## Threads (Typical in Small RTOS)

Characteristics:

- Share the same address space
- Fast context switching
- Only register state needs to be switched

Advantages:

- Efficient
- Lightweight

Disadvantages:

- Threads may accidentally overwrite shared memory.

![[Pasted image 20260304154440.png]]

---

## Processes (Desktop OS Model)

Each process has:

- Independent address space
- Memory protection

Requires:

- Memory Management Unit (MMU)

Advantages:

- Isolation between processes

Disadvantages:

- Context switch more complex.

![[Pasted image 20260304154459.png]]

---

## Compromise: Thread Protected Mode

Threads with memory protection.

Characteristics:

- Multiple threads
- Memory protected using MMU
- Only required memory regions visible to a thread

Also known as:

- Lightweight process model

![[Pasted image 20260304154525.png]]

---

# 7. Scheduling Strategies

Scheduling determines how CPU time is distributed among tasks.

---

## Run-To-Completion (RTC)

Characteristics:

- Tasks implemented as functions
- Task runs until it returns

Advantages:

- Very simple
- Minimal overhead

Disadvantages:

- A task can monopolize CPU
- Requires careful design

![[Pasted image 20260304154538.png]]

---

## Round-Robin Scheduler

Characteristics:

- Tasks voluntarily yield CPU
- Context must be saved and restored
- Implemented by RTOS kernel

Operations during switch:

- Save register state
- Save stack pointer
- Save program counter

![[Pasted image 20260304154551.png]]

---

## Time-Slice Scheduler

Features:

- CPU time divided into fixed slots
- Tasks executed during assigned slots
- Kernel may preempt tasks

Advantages:

- Predictable execution timing
- Fair CPU allocation

![[Pasted image 20260304154639.png]]

---

## Priority-Based Scheduler

Most common RTOS scheduling approach.

Features:

- Tasks assigned priorities
- Highest priority runnable task executes
- Preemption possible

Events that trigger scheduling:

- ISR events
- Task suspension
- Resource availability

Dynamic scheduling possible when priorities change.

![[Pasted image 20260304154656.png]]

---

# 8. Task States

A task may exist in several states:

- Created
- Ready
- Running
- Suspended
- Blocked
- Terminated

Suspension can occur due to:

- Sleep calls
- Blocking resource access
- Waiting for events

The **task context** must be saved and restored during switches.

![[Pasted image 20260304154715.png]]

---

# 9. Scheduler Concepts

Scheduling determines how processes and threads gain CPU access.

Important questions:

- What scheduling algorithms exist?
- How are periodic tasks handled?
- How is priority inversion addressed?
- When are tasks preemptible?

---

# 10. Types of Schedulers

## Cooperative (Non-Preemptive)

- Tasks voluntarily yield CPU
- Scheduler cannot interrupt a running task

Example historical systems:

- MacOS pre-9
- Windows 3.x

---

## Preemptive Scheduler

- Kernel can interrupt running tasks
- Higher-priority task can preempt lower-priority task

Examples:

- Linux
- Windows NT and later
- macOS

Real-time systems usually require **preemptive scheduling**.

---

# 11. Priority Inversion

Scenario:

1. Low-priority task holds a shared resource
2. High-priority task requires that resource
3. Medium-priority task executes instead

Result:

High-priority task blocked by low-priority task indirectly.

---

## Limited Priority Inversion

Priority inversion lasts until the resource is released.

![[Pasted image 20260304155037.png]]


---

## Unlimited Priority Inversion

Medium-priority tasks repeatedly preempt low-priority task.

![[Pasted image 20260304155037.png]]

High-priority task may wait indefinitely.

Solution:

**Priority inheritance protocol**
![[Pasted image 20260304155133.png]]

---

# 12. Requirements for Real-Time Operating Systems

Key characteristics:

- Continuous stable operation
- Predictable response times
- Parallel task execution
- Multi-core support
- Fast context switching
- Real-time interrupt handling
- Real-time scheduling
- Inter-process communication
- Precise time services
- Simple memory management

---

# 13. Additional RTOS Requirements

Hardware interaction:

- Extensive peripheral support
- Direct register access
- Fast driver development
- DMA support

System features:

- Simple file systems
- Network/field bus protocols
- Modular architecture
- Standard API support (e.g. POSIX)

---

# 14. Inter-Process Communication (IPC)

Tasks must exchange information.

Common mechanisms:

- Signals (task-owned flags)
- Event flags
- Mailboxes
- Queues
- Semaphores
- Mutexes
- Message passing

Shared variables:

- Fast but risky
- Safe only for atomic operations
- Locks required for complex access.

---

# 15. Evaluating Real-Time Operating Systems

Evaluation criteria include:

- Maximum number of tasks
- IPC mechanisms
- POSIX compatibility
- Portability
- API design

---

## POSIX

POSIX = Portable Operating System Interface

Benefits:

- Standard system call interface
- High portability of code

---

# 16. Memory Consumption

RTOS must operate on diverse hardware.

Important factors:

- Available memory may vary greatly
- Some OS modules unnecessary

RTOS should therefore be **scalable**.

Requirements:

- Optional modules
- Small memory footprint

---

# 17. Response Time Metrics

Important timing metrics in RTOS:

## Interrupt Latency

Time between interrupt occurrence and first instruction of ISR.

---

## Scheduling Latency

Time between end of ISR and start of scheduled task.

---

## Context Switch Latency

Time between stopping one task and starting the next.

---

Typical ranges vary depending on system requirements.

![[Pasted image 20260304155155.png]]

![[Pasted image 20260304155204.png]]

---

# 18. Summary

Key observations:

- Not all real-time systems require an OS.
- There is no universal RTOS suitable for all systems.
- RTOS memory requirements range from KB to MB.
- Systems are typically scalable.

Examples:

- freeRTOS
- VxWorks
- QNX

Real-time capabilities can also be added to standard OS:

- RTLinux
- RTAI
- PREEMPT_RT Linux patch

Scheduling and IPC mechanisms often follow POSIX standards.

---
# Lecture6: Scheduling

---

# Task Execution Model

Task states:

- READY
- RUN
- WAIT

Transitions:

- activation
- dispatching
- preemption
- signal wait

![[Pasted image 20260304170906.png]]

---

# 1. Scheduler and Dispatcher

## Scheduler

The **scheduler** performs resource allocation.

Responsibilities:

- Assign CPU time to tasks
- Decide which task should execute next

---

## Dispatcher

The **dispatcher** executes the scheduler's decision.

Responsibilities:

- Perform **context switching**
- Switch to **user mode**
- Jump to the correct program location to resume execution

![[Pasted image 20260304170845.png]]

---

# 2. Scheduling Problems

Define:

- $T = \{T_1, T_2, ..., T_n\}$ → set of processes/tasks
- $P = \{P_1, P_2, ..., P_n\}$ → set of processors
- $R = \{R_1, R_2, ..., R_n\}$ → set of resources

Goal:

Assign processors from P and resources from R to processes from T in order to complete all processes under the specified constraints

---

# 3. Task Constraints

Typical constraints:

- **Timing constraints** (deadlines)
- **Precedence constraints**
- **Resource constraints**

---

# 4. Temporal Characterization of Tasks

For task $T_i$:

- $a_i$ – arrival time (release time)
- $s_i$ – start time
- $f_i$ – finishing time
- $d_i$ – absolute deadline
- $C_i$ – computation time

---

## Derived Timing Metrics

### Relative Deadline

$$
D_i = d_i - a_i
$$

---

### Response Time

$$
R_i = f_i - a_i
$$

---

### Lateness

$$
L_i = f_i - d_i
$$

---

### Tardiness

$$
E_i = \max(0, L_i)
$$

---

### Slack Time (Laxity)

$$
X_i = d_i - a_i - C_i
$$

Other task attributes:

- Criticality (hard / firm / soft)
- Task value (importance)

---

# 5. Precedence Constraints

Tasks may depend on other tasks.

Represented using an **acyclic precedence graph**.

Example dependency chain:

- $T_1 \rightarrow T_2$
- $T_2 \rightarrow T_3$

![[Pasted image 20260304171124.png]]

---

# 6. Task Types

## Periodic Tasks

Released at regular intervals.

Example:

$$
T_i = (C_i, P_i)
$$

where $P_i$ is the period.

---

## Aperiodic Tasks

- Irregular arrival times
- No fixed period

---

## Sporadic Tasks

- Random arrival times
- Minimum inter-arrival time guaranteed

---

# 7. Scheduling Categories

Scheduling algorithms may be:

- **Preemptive** or **non-preemptive**
- **Static** or **dynamic**
- **Offline** or **online**
- **Optimal** or **heuristic**

---

# 8. Guarantee-Based Algorithms

## Hard Real-Time Systems

Characteristics:

- Often computed **offline**
- Use complex optimal algorithms
- No runtime scheduling overhead

Limitations:

- Inflexible
- Depend on accurate environment modeling

---

## Dynamic Real-Time Systems

Scheduling decisions occur at runtime.

Process:

1. Task arrives
2. **Acceptance test** performed
3. If schedulable → task accepted
4. Otherwise → task rejected

![[Pasted image 20260304171147.png]]

---

# Domino Effect

Adding a task may cause cascading deadline failures.

Result:

- System rejects the new task.

![[Pasted image 20260304171207.png]]

---

# 9. Scheduling Anomalies

Unexpected effects may occur when:

- Adding processors
- Reducing execution time
- Relaxing precedence constraints

These may **increase total completion time**.

![[Pasted image 20260304171300.png]]

---

# Key Insight

Seemingly beneficial improvements such as:

- Faster processors
- Additional CPUs
- Reduced execution times

may **increase overall completion time**.

This phenomenon is called **scheduling anomaly**.

---

# 10. Best-Effort Algorithms

Used for **soft real-time systems**.

Characteristics:

- Missed deadlines degrade performance
- Tasks are not rejected
- System tries to meet deadlines whenever possible

---

# 11. Aperiodic Task Scheduling

Aperiodic tasks:

- Have irregular arrival times
- May have soft or hard deadlines

---

# 12. Scheduling Problem Classification

Scheduling problems are often represented as:

```
a | b | c
```

Where:

- **a** → machine environment (number of processors)
- **b** → task/resource characteristics
- **c** → optimality criterion

Example:

```
3 | no_preem | Σ f_i
```

 Metrics for performance evaluation / cost functions:
 * average response time: $\bar{t}_r = \frac{1}{n}\sum_{i=1}^n(f_i - a_i)$
 * total completion time: $\max\limits_{i} (f_i) - \min\limits_{i} (a_i)$
 * weighted sum of completion times: $t_w = \sum_{i=1}^n w_i f_i$
 * maximum lateness: $L_max = \max\limits_i (f_i - d_i)$
 * maximum number of late tasks:  $N_{late} = \sum_{i=1}^n miss (f_i)$

---

# 13. Performance Metrics

## Average Response Time

$$
\bar{t_r} = \frac{1}{n}\sum_{i=1}^{n}(f_i - a_i)
$$

---

## Total Completion Time

$$
\max_i(f_i) - \min_i(a_i)
$$

---

## Weighted Completion Time

$$
t_w = \sum_{i=1}^{n} w_i f_i
$$

---

## Maximum Lateness

$$
L_{max} = \max_i(f_i - d_i)
$$

---

## Number of Late Tasks

$$
N_{late} = \sum_{i=1}^{n} miss(f_i)
$$

![[Pasted image 20260304175855.png]]

---

# 14. Utility Functions

Different real-time systems evaluate task completion differently.

Examples:

- Non-real-time
- Soft real-time
- On-time systems
- Firm real-time systems

![[Pasted image 20260304175908.png]]

---

# 15. Jackson's Algorithm (EDD)

Problem:

```
1 | sync | Lmax
```

Tasks arrive simultaneously.

Goal:

Minimize **maximum lateness**.

---

## Earliest Due Date Rule

Schedule tasks in **ascending order of deadlines**.

This strategy is **optimal** for minimizing lateness.

---

## Optimality Condition

A feasible schedule exists if:

$$
f_i \le d_i
$$

Worst-case finishing time:

$$
f_i = \sum_{k=1}^{i} C_k
$$

---

## Feasibility Condition

For hard real-time tasks:

$$
\sum_{k=1}^{i} C_k \le d_i
$$

Jacksons Algorithm:
![[Pasted image 20260304175953.png]]
![[Pasted image 20260304180001.png]]

---

# 16. Horn's Algorithm (EDF)

Problem:

```
1 | preem | Lmax
```

Tasks may arrive asynchronously.

Solution:

**Earliest Deadline First (EDF)**.

---

## EDF Rule

At every scheduling decision:

Execute the task with the **earliest absolute deadline**.

---

## Optimality

EDF minimizes **maximum lateness** for independent tasks.

Task definition:

$$
T_i = (a_i, C_i, d_i)
$$

![[Pasted image 20260304180142.png]]

---

# EDF Schedulability Test

Remaining execution time:

$$
f_i = \sum_{k=1}^{i} c_k(t)
$$

Feasible if:

$$
\sum_{k=1}^{i} c_k(t) \le d_i
$$

![[Pasted image 20260304180214.png]]

---

# 17. Non-Preemptive Scheduling Challenges

In non-preemptive systems:

- Tasks cannot be interrupted
- Idle time insertion may be required

However:

Arrival times must be known beforehand.

![[Pasted image 20260304180232.png]]

---

# Complexity of Scheduling

Brute-force search:

- Tree depth = $n$
- Possible schedules = $n!$

Complexity:

$$
O(n \cdot n!)
$$

This becomes impractical for large task sets.

---

# 18. Bratley's Algorithm

Problem:

```
1 | no_preem | feasible
```

Approach:

- Branch-and-bound search
- Prune branches when deadline violations occur

Branch is abandoned if:

- Deadline already missed
- A feasible schedule is found

![[Pasted image 20260304180300.png]]

---

# 19. Heuristic Scheduling Functions

Used to guide scheduling search.

Examples:

- **FCFS** – First Come First Served
- **SJF** – Shortest Job First
- **EDF** – Earliest Deadline First
- **ESTF** – Earliest Start Time First

Limitations:

- Not guaranteed optimal
- May miss feasible schedules

---

# 20. Static Scheduling with Precedence Constraints

Problem:

```
1 | PREC, SYNC | Lmax
```

Solution:

**Latest Deadline First (LDF)**.

Procedure:

- Build scheduling queue **from tail to head**
- Choose task with **largest deadline**

📌 Copy example on slide 52.

---

# EDF vs LDF

Example comparison:

- **EDF**: schedule by earliest deadline
- **LDF**: schedule backward by latest deadline

![[Pasted image 20260304180319.png]]

---

# 21. Dynamic Scheduling with Precedence Constraints

Problem:

```
1 | PREC, PREEM | Lmax
```

Steps:

1. Convert dependent tasks into independent tasks
2. Modify timing parameters
3. Apply **EDF scheduling**

---

## Parameter Transformation

Arrival time adjustment:

$$
a_2^* = a_1 + C_1
$$

Deadline adjustment:

$$
d_1^* = d_2 - C_2
$$

After transformation:

Apply **EDF (Horn's algorithm)**.

![[Pasted image 20260304180350.png]]

---

# 22. Comparison of Scheduling Algorithms

| Scenario | Algorithm | Optimal |
|--------|--------|--------|
| synchronous activation | EDD (Jackson) | Yes |
| asynchronous preemptive | EDF (Horn) | Yes |
| asynchronous non-preemptive | tree search | Yes |
| precedence constraints | LDF | Yes |
| dynamic precedence constraints | EDF* | Yes |
| heuristic search | heuristic tree search | No |
![[Pasted image 20260304180418.png]]

---

# Lecture 7: Concurrency, Threads, Processes and Resource Access Protocols

---

# 1. Concurrency

## Definition

Common meaning:

Concurrent events are **not causally dependent** on each other.  
Events (or sequences of events) are concurrent if none causes another.

Meaning in computer science:

Concurrency describes the property of code to be **runnable in parallel instead of sequentially**.

Instructions can run in parallel (pseudo-parallel) if they are **not dependent on each other's results**.

Types:

- **Multiprocessing**: Parallel execution of several independent processes on one or multiple processors.
- **Multithreading**: Parallel execution of sub-sequences within a process.

---

# Contents

- Introduction
- Processes
- Threads
- Resource access protocols

---

# 2. Motivation for Multiprocessor Computers

Limits of processor improvements:

**Moore’s Law**

> Number of transistors on a chip doubles roughly every two years, increasing performance.

However, two major limitations appear:

### Memory Wall

Memory speed does not scale with processor speed.

### Power Wall

Higher clock frequencies generate excessive heat that cannot be dissipated.

---

# Causes of Performance Degradation

Important delays arise from:

- Memory access
- Thread switching
- Thread synchronization

---

# 3. Processes

## Definition

A **process** is an abstraction of a program being executed.

A process includes:

- Code
- Stack
- CPU registers
- Memory mapping (MMU registers)
- File information
- Access rights
- Kernel stack

Processes can create new processes:

- **Parent process**
- **Child process**

![[Pasted image 20260304180601.png]]

---

# Process Execution

Process execution requires resources:

- CPU time
- Memory
- Other hardware resources

Execution time depends on:

- CPU performance
- Resource availability
- Input parameters
- Delay due to other processes

---

# Process States

Typical process states:

- Non-existing
- Created
- Ready
- Running
- Suspended
- Blocked
- Terminated

![[Pasted image 20260304180614.png]]

---

# Process Types

### Preemptable Process

Execution can be suspended.

Types:

- Fully preemptable
- Preemption only at predefined points

---

### Periodic Process

Released at a fixed frequency:

$$
p
$$

---

### Aperiodic Process

Irregular activation times.

- Soft deadline or none
- No minimum inter-arrival time

---

### Sporadic Process

Event-driven processes with hard deadlines.

Properties:

- Triggered by external signals
- Have a minimum inter-arrival time.

---

# Implementation Questions

When implementing concurrent systems:

- Which resources are required?
- What are the execution durations?
- How do processes communicate?
- When should processes be scheduled?
- How should processes synchronize?

---

# 4. Threads

Processes require large memory structures.

Process context includes:

- CPU state
- File descriptors
- Device state

Context switching between processes is expensive.

Therefore **threads** are used.

Threads:

- Share the same address space
- Require less management overhead
- Enable parallel execution paths within a program

---

# Reasons for Concurrency in Real-Time Systems

Real-time systems often:

- Run on distributed hardware
- Execute real-time and non-real-time tasks simultaneously
- Have strict response-time requirements
- Model parallel physical processes

---

# Multithreaded Processors

Processors may support **multiple threads simultaneously**.

Characteristics:

- Multiple thread contexts stored in registers
- Instructions from different threads feed the pipeline
- Latencies do not stall the processor

This differs from normal **context switching**, which requires storing state in memory.

---

# 5. Multithreading Techniques

## Fine-Grained Multithreading (Cycle-by-Cycle Interleaving)

- Instructions from different threads are interleaved every cycle
- Next instruction of same thread executed only after pipeline exit

---

## Coarse-Grained Multithreading (Block Interleaving)

- A thread runs until a blocking event occurs

Example blocking events:

- Cache miss
- Data dependency

---

# Processor Pipeline

Machine instructions are executed in several stages.

Typical pipeline stages:

1. Instruction Fetch
2. Instruction Decode
3. Execute (ALU)
4. Memory Access
5. Write Back

![[Pasted image 20260304180641.png]]

---

# Improving Pipeline Efficiency

Problem:

With only one thread, a new instruction can only be loaded every:

$$
n
$$

cycles, where:

$$
n = \text{pipeline length}
$$

Solution:

**Explicit-dependence lookahead**

The compiler marks independent instructions so the pipeline can execute them without waiting.

---

# Cycle-by-Cycle Interleaving

Advantages:

- No pipeline dependencies
- No pipeline flush after branch misprediction
- Less hardware required
- Faster context switching

Disadvantages:

- Less efficient than block interleaving.

---

# Block Interleaving

Types of switching:

### Static Switching

- Explicit context-switch instruction
- Based on instruction groups

Example triggers:

- Load
- Store
- Branch instructions

---

### Dynamic Switching

Switch occurs when:

- Cache miss occurs
- Signal/interrupt arrives
- Value dependency detected
- Conditional switch conditions met

---

# Concurrency Use Case: Interrupts

Interrupts are commonly used for:

- Interaction with external hardware

Example:

A thermometer triggers an interrupt when a **critical temperature level** is reached.

![[Pasted image 20260304180709.png]]

---

# Processes vs Threads

Processes:

- Separate memory spaces
- Higher management overhead
- Strong isolation

Threads:

- Shared memory
- Faster switching
- Lower overhead

Advantages of threads:

- Efficient communication via shared memory

Disadvantage:

- Shared data may cause **conflicts**.

---

# 6. Critical Sections

Shared resources cannot be accessed simultaneously by competing processes.

A **critical section** is code that must be executed with **mutual exclusion**.

---

# Protecting Critical Sections

Examples from everyday life:

- Railroad signals
- Traffic lights
- Room locks
- Ticket distribution

In software:

**Semaphores** are commonly used.

---

# Mutual Exclusion

Critical section protection ensures:

- Only one process enters a region at a time.

Example problem:

**Reader–Writer Problem**

- Multiple readers allowed
- Writer requires exclusive access

![[Pasted image 20260304180725.png]]

---

# Critical Section Example

Two processes accessing a shared buffer:

- Sensor data producer
- Data plotting consumer

![[Pasted image 20260304180741.png]]

---

# Requirements for Mutual Exclusion

A correct solution must satisfy:

1. Only one process enters the critical section
2. No assumptions about processor speed or number
3. Processes outside critical sections must not block others
4. Waiting time must be finite

---

# 7. Resource Access Protocols

Protocols for managing shared resources:

- Non-Preemptive Protocol (NPP)
- Highest Locker Priority (HLP)
- Priority Inheritance Protocol (PIP)
- Priority Ceiling Protocol (PCP)

---

# Resource Definition

A **resource** is any structure used by processes:

Examples:

- Data structures
- Variables
- Memory regions
- Files
- Device registers

Types:

- Private resource
- Shared resource
- Exclusive resource (protected)

---

# Semaphores

Semaphores are kernel data structures.

Operations:

- `wait(S_k)`
- `signal(S_k)`

Rules:

- Each exclusive resource has a semaphore
- Critical section starts with `wait()` and ends with `signal()`
- Each semaphore maintains a process queue.

![[Pasted image 20260304182855.png]]

---

# Synchronization Example

Processes synchronize access to a shared buffer using semaphores.

![[Pasted image 20260304182908.png]]

---

# 8. Concurrency Problems

## Race Conditions

Occurs when multiple threads read/write shared data.

Result depends on execution order.

Solution:

- Critical sections
- Mutual exclusion

---

## Starvation

A process is indefinitely denied required resources.

Solution:

- Fair waiting queues.

---

## Priority Inversion

A high-priority task waits for a low-priority task holding a resource.

---

# 9. Non-Preemptive Protocol (NPP)

Properties:

- No preemption allowed during critical sections
- Process entering critical section receives highest priority

Priority assignment:

$$
p_i(R_k) = \max_h \{P_h\}
$$

Priority resets after leaving the critical section.

![[Pasted image 20260304182921.png]]

---

# Blocking Time (NPP)

Assume:

$$
P_i > P_j
$$

Blocking time:

$$
B_i = \max \{ \delta_{j,k} \}
$$

Meaning:

A task can be blocked by the **longest critical section of a lower priority task**.

![[Pasted image 20260304183013.png]]

---

# 10. Highest Locker Priority Protocol (HLP)

When a process locks resource $R_k$:

It receives the **highest priority among processes using that resource**.

Dynamic priority:

$$
p_i(R_k) = \max_h \{P_h \mid T_h \text{ uses } R_k \}
$$

Simplified version:

Assign a **priority ceiling**:

$$
C(R_k) = \max_h \{P_h \mid T_h \text{ uses } R_k \}
$$

Process receives priority $C(R_k)$ during critical section.

![[Pasted image 20260304183038.png]]

---

# 11. Priority Inheritance Protocol (PIP)

Idea:

If a high-priority process is blocked by a lower-priority process:

The blocking process **inherits the higher priority**.

Priority rule:

$$
p_j(R_k) =
\max \left\{ P_j,\; \max_h \{P_h \mid T_h \text{ blocked on } R_k \} \right\}
$$

After leaving the critical section:

Priority returns to normal.

Priority inheritance is **transitive**.

![[Pasted image 20260304183100.png]]

---

## Blocking Types

### Direct Blocking

High-priority task waits for a lower-priority task holding a resource.

---

### Push-Through Blocking

Medium-priority task blocked because a lower-priority task inherited a higher priority.

---

# Transitive Priority Inheritance

If:

- $T_3$ blocks $T_2$
- $T_2$ blocks $T_1$

Then:

$$
T_3
$$

inherits the priority of

$$
T_1
$$

📌 Copy diagram on slide 58.

---

# 12. Deadlocks

Deadlocks occur when tasks wait for each other's resources.

Example:

```
T1: wait(Sa) → wait(Sb)
T2: wait(Sb) → wait(Sa)
```

Neither process can proceed.

![[Pasted image 20260304183110.png]]

---

# 13. Priority Ceiling Protocol (PCP)

Goal:

Prevent:

- Priority inversion
- Deadlocks
- Chained blocking

Rules:

1. Each resource has a **priority ceiling**.
2. A process may enter a critical section only if its priority is higher than the ceilings of all locked semaphores.

Example:

If

$$
C(a) = P_1,\quad C(b) = P_1,\quad C(c) = P_2
$$

then tasks must respect these ceilings.

![[Pasted image 20260304183129.png]]

---

# Comparison of Protocols

| Protocol | #Blocking | Pessimism | Blocking Instant | Transparency | Deadlock Prevention | Implementation |
|--------|--------|--------|--------|--------|--------|--------|
| NPP | 1 | High | On arrival | Yes | Yes | Easy |
| HLP | 1 | Medium | On arrival | No | Yes | Easy |
| PIP | >1 | Low | On access | Yes | No | Hard |
| PCP | 1 | Medium | On access | No | Yes | Medium |

Transparent protocols:

- NPP
- PIP

These work with standard semaphore primitives.

Protocols using ceilings:

- HLP
- PCP

Require additional system calls.

---

# Lecture 8: Real-Time Communication

---

# Motivation

Real-time communication is important for **distributed embedded systems**.

Typical applications:

- Systems containing many controllers  
  - e.g., cars and airplanes
- Distributed industrial systems  
  - e.g., factories

Field buses and peripheral connections allow controllers to communicate efficiently.

![[Pasted image 20260304183234.png]]

---

# Content

1. Requirements  
2. Aspects of Communication Protocols  
3. Applied Protocols  
   - IO Protocols  
   - Traditional Field Buses  
   - Industrial Ethernet Protocols

---

# 1. Requirements of Real-Time Communication Systems

Key requirements:

### Predictability

Communication must have **deterministic latency**.

### Synchronism

Low **jitter** is required.

### Fast Systems (e.g., Motion Control)

Requirements:

- Small latencies
- Guaranteed bandwidth

### Reliability

- Few faults
- Fault handling that maintains timing guarantees

![[Pasted image 20260304183250.png]]

---

# 2. OSI Model

The **Open Systems Interconnection (OSI) model** is an abstraction model for communication protocols.

Standardized by the **International Organization for Standardization (ISO)**.

OSI Layers:

1. Physical Layer  
2. Data Link Layer  
3. Network Layer  
4. Transport Layer  
5. Session Layer  
6. Presentation Layer  
7. Application Layer

---

# Important OSI Layers for Real-Time Communication

For real-time protocols, typically only three layers are relevant:

- Layer 1: Physical Layer
- Layer 2: Data Link Layer
- Layer 7: Application Layer

---

# 3. Physical Layer

Responsibilities:

- Physical connections
- Line codes
- Network topologies

---

# Physical Connections

Elements:

### Cables

Characteristics:

- Transport medium (electrical, optical, wireless)
- Parallel or serial communication
- Twisted pair or coaxial cables
- Proper termination
- Electromagnetic shielding

### Plugs and Sockets

Provide standardized connections between devices.

---

# Propagation Time of Signals

Signal propagation speed:

- Light in vacuum:

$$
v \approx 0.3 \cdot 10^9 \, m/s
$$

- Light in glass:

$$
v \approx 0.2 \cdot 10^9 \, m/s
$$

- Electromagnetic wave in copper:

$$
v \approx 0.2 \cdot 10^9 \, m/s
$$

Example:

Propagation delay for **100 m cable**:

$$
t = \frac{x}{v}
$$

$$
t = \frac{100\,m}{0.2 \cdot 10^9\,m/s} = 0.5\ \mu s
$$

---

# Bit Length of a Channel

If the transmission rate is:

$$
100\,Mbit/s
$$

then one bit takes:

$$
10\,ns
$$

Number of bits traveling in the channel during propagation:

$$
\frac{500\,ns}{10\,ns/bit} = 50 \text{ bits}
$$

---

# Line Coding

Line coding defines how bits are represented physically.

Possible representations:

- Voltage between wires
- Differential voltage
- Optical pulses

---

## Non-Return-to-Zero Level (NRZ-L)

Encoding:

- **1** → high voltage
- **0** → zero voltage

![[Pasted image 20260304183407.png]]

---

## Return-to-Zero (RZ)

Encoding:

- **1** → high for first half of bit period
- **0** → low level

---

## Bipolar RZ

Encoding:

- **1** → positive voltage
- **0** → negative voltage

![[Pasted image 20260304183425.png]]

---

## Manchester Coding

Encoding:

- **1** → negative transition mid-bit
- **0** → positive transition mid-bit

Properties:

- Embedded clock signal
- No DC component
- Requires twice the bandwidth of data rate

![[Pasted image 20260304183501.png]]

---

# Bit Stuffing

Problem:

Long sequences of identical bits cause **synchronization issues**.

Solution:

Insert **stuff bits** after a specified number of identical bits.

![[Pasted image 20260304183522.png]]

---

# Network Topologies

Common topologies:

- **Bus**
- **Ring**
- **Star**

Bus topology advantages:

- Minimal wiring
- Easy node addition/removal

Ring topology advantages:

- Redundancy

![[Pasted image 20260304183535.png]]

---

# Hubs and Switches

## Hub

- Forwards messages to **all nodes**
- One collision domain

## Switch

- Forwards frames only to the **target node**
- Uses MAC address table

![[Pasted image 20260304183556.png]]

---

# Ethernet Frame Structure

Components:

- Preamble
- Start Frame Delimiter (SFD)
- Destination MAC
- Source MAC
- EtherType
- Payload
- Frame Check Sequence (FCS)

![[Pasted image 20260304183614.png]]

---

# 4. Data Link Layer

Responsibilities:

- Media Access Control (MAC)
- Transmission error detection

---

# Media Access Control (MAC)

The communication medium can typically only be used by **one node at a time**.

MAC methods allocate the medium.

Categories:

- Random access
- Deterministic access

![[Pasted image 20260304183632.png]]

---

# CSMA/CD (Collision Detection)

Carrier Sense Multiple Access with Collision Detection.

Rules:

1. Node transmits only if bus is free
2. If collision occurs:
   - Detect collision
   - Abort transmission
   - Wait random time
   - Retry transmission

Used in **standard Ethernet**.

---

# CSMA/CA (Collision Avoidance)

Collision avoidance with **priority arbitration**.

If multiple nodes transmit:

- Message with highest priority wins.

Used in systems such as **CAN**.

![[Pasted image 20260304183705.png]]

![[Pasted image 20260304183717.png]]

---

# Centralized Control

Master-slave system.

Procedure:

1. Master searches for slaves
2. Master assigns transmission slots
3. Slave transmits

---

# Distributed Control

Two approaches:

### Time-Slot Assignment

Each node has a predefined time slot.

### Token Passing

Only the node holding the **token** may transmit.

Example:

FlexRay.

---

# Real-Time Compatibility of MAC Methods

Only **deterministic MAC methods** guarantee real-time behavior.

Correct answer:

**Only deterministic methods are real-time compatible.**

---

# Error Detection

Common methods:

### Checksums / CRC

Cyclic Redundancy Check.

### Parity Bits

Simple error detection mechanism.

Real-time systems often prioritize **fast retransmission** rather than complex error correction.

![[Pasted image 20260304183738.png]]

---

# 5. Application Layer

Responsibilities:

- Data input/output
- Simplify lower-layer usage
- Provide APIs for embedded systems

---

# Communication Models

## Client-Server Model

Characteristics:

- One-to-one communication
- Optional confirmation messages

---

## Producer-Consumer Model

Characteristics:

- One producer
- Many receivers
- Usually no confirmation

![[Pasted image 20260304183808.png]]

---

# Message Classification

Messages may be:

### Time-triggered

Periodic communication.

Example:

Controller polling sensor data.

### Event-triggered

Triggered by events such as faults.

---

## Real-Time Timing Requirements

Typical latency requirements:

| Application | Latency | Jitter |
|---|---|---|
| Controller to controller | 10–100 ms | |
| Controller to peripherals | 1–10 ms | ≈ 1 ms |
| Motion control | ≤ 1 ms | ≤ $10^{-3}$ ms |

---

# 6. Communication Protocol Categories

Three major categories:

1. IO protocols
2. Field buses
3. Industrial Ethernet protocols

---

# IO Protocols

Examples:

- RS232
- RS422
- SPI
- I2C

---

# RS232 / RS422

Characteristics:

- Point-to-point communication
- Asynchronous protocol
- Uses voltage difference between wires

Example:

ASCII character transmission with:

- Start bit
- Data bits
- Stop bit

📌 Copy bitstream diagram on slide 48.

---

# UART (RS232)

UART = Universal Asynchronous Receiver Transmitter.

3-wire interface example:

- TX
- RX
- GND

Optional hardware handshaking possible.

---

# SPI (Serial Peripheral Interface)

Characteristics:

- Synchronous protocol
- Master-slave architecture
- Clock generated by master
- Full duplex communication

Signals:

- MOSI (Master Out Slave In)
- MISO (Master In Slave Out)
- CLK (Clock)
- SS (Slave Select)

---

# SPI Multi-Slave Architecture

Slave selection performed via **SS lines**.

Data exchanged via shift registers.

Communication is simultaneous in both directions.

![[Pasted image 20260304183841.png]]

---

# 7. Traditional Field Buses

Examples:

- CAN
- Profibus
- FlexRay
- LIN

---

# CAN (Controller Area Network)

Developed by **Bosch** in the 1980s.

Characteristics:

- Multi-master network
- Bus topology
- Event-triggered communication
- Uses **CSMA/CA arbitration**

Physical layer:

- 2-wire twisted pair
- Up to **1 Mbit/s**

---

# CAN Message Format

Structure:

- Start-of-frame
- Message ID (11 bits)
- Data length code
- Data (0–8 bytes)
- CRC checksum

Nodes do not have addresses — messages have IDs.

![[Pasted image 20260304183956.png]]

---

# CAN Arbitration

Mechanism:

- Dominant bit = 0
- Recessive bit = 1

Lower message ID → higher priority.

When collision occurs:

Node transmitting recessive bit stops transmission.

![[Pasted image 20260304183932.png]]

---

# CAN Summary

Key characteristics:

- Widely used in automotive systems
- Multi-master bus
- 2-wire physical layer
- Up to 1 Mbit/s
- Maximum payload: 8 bytes

Approximately:

$$
7 \text{ full messages per ms}
$$

---

# Profibus

Developed by Siemens.

Two versions:

- **DP (Decentralized Peripherals)**
- **PA (Process Automation)**

Characteristics:

- Master-slave system
- Multiple masters possible
- Data rates:

$$
9.6\,kbit/s \text{ to } 12\,Mbit/s
$$

---

# 8. Industrial Ethernet Protocols

Examples:

- EtherNet/IP
- Profinet
- EtherCAT
- Ethernet Powerlink

---

# EtherNet/IP

Industrial Protocol using Ethernet.

Characteristics:

- Uses UDP for I/O data
- TCP for configuration
- Requires switched Ethernet network
- Supports unicast, multicast, broadcast

Common in North America.

---

# Profinet

Developed by Siemens.

Features:

- Built on standard Ethernet hardware
- Integrates TCP/IP
- Uses **provider-consumer communication model**

Not simply "Profibus over Ethernet".

---

# EtherCAT

Developed by Beckhoff.

Architecture:

- Master-slave network
- Nodes process frames **on-the-fly**

Performance example:

- 1000 I/O updates in

$$
30\ \mu s
$$

- 100 servo axes updated in

$$
100\ \mu s
$$

---

# Selecting a Communication Protocol

Important criteria:

- Required bandwidth
- Number of nodes
- Cable length
- Cost
- Availability of hardware

---

# Summary

Key observations:

- Real-time protocols typically implement fewer OSI layers.
- Time-triggered communication provides deterministic behavior.
- Many different protocols exist with different design philosophies.
- Trend toward **Ethernet-based protocols**.
- Robotics frameworks like ROS often use standard Ethernet despite real-time limitations.

---

# Lecture 9: Dependability

---

# Introduction

Recent cyberattacks demonstrate the importance of dependable systems:

- Cyberattack causing **physical damage to a German steel mill** (2015)
- Malware attack disrupting **Hoya factory operations** (2019)
- Cyberattack affecting **Palfinger crane manufacturer** (2021)

Dependability concerns the reliability and robustness of systems under faults.

---

# Fault – Error – Failure Chain

System behavior can be described by the following chain:

```
FAULT  →  ERROR  →  FAILURE
```

- **Fault**: defect in system component
- **Error**: incorrect internal system state
- **Failure**: system deviates from correct service

![[Pasted image 20260304184328.png]]

---

# Aspects of Dependability

Dependability consists of several attributes:

- **Availability**  
  Readiness for correct service.

- **Reliability**  
  Continuity of correct service delivery.

- **Safety**  
  Absence of catastrophic consequences.

- **Confidentiality**  
  Protection against unauthorized information disclosure.

- **Integrity**  
  Protection against improper data modification.

- **Maintainability**  
  Ability to repair or modify the system.

![[Pasted image 20260304184343.png]]

---

# Dependability Terminology

Dependability can be described using:

### Attributes

- Availability
- Reliability
- Safety
- Integrity
- Confidentiality
- Maintainability

### Means

- Fault prevention
- Fault tolerance
- Fault removal
- Fault forecasting

### Impairments

- Faults
- Errors
- Failures

![[Pasted image 20260304184352.png]]

---

# Faults

Faults are defects in hardware, software, or environment.

Types of faults include:

- **Internal faults**
- **External faults**

Further classifications:

### Space domain

- Physical faults
- Design faults
- Input-data faults

### Time domain

- Transient faults
- Permanent faults

![[Pasted image 20260304184402.png]]

---

# Transient, Permanent, and Intermittent Faults

### Transient Fault

- Appears temporarily and disappears.
- Example: cosmic radiation affecting hardware.

### Permanent Fault

- Remains until repaired.
- Example: broken wire or design error.

### Intermittent Fault

- Occurs occasionally.
- Example: temperature-sensitive hardware component.

![[Pasted image 20260304184421.png]]

---

# Errors

An **error** is an incorrect system state.

Examples:

- incorrect memory value
- incorrect register content

Errors become visible only when the faulty state is accessed.

---

## Software Error Types

### Bohrbugs

- Deterministic
- Easily reproducible
- Caused by specific input sequences.

### Heisenbugs

- Hard to reproduce
- Occur due to timing or interaction effects.

---

# Failures

A **failure** occurs when the system behavior deviates from the expected service.

![[Pasted image 20260304184440.png]]

---

# Failure Modes

Failures can occur in different domains:

### Value Domain Failures

Incorrect output values.

### Timing Domain Failures

- Early output
- Late output
- Omission

### Arbitrary Failures

Unpredictable behavior.

Other categories:

- Fail-silent
- Fail-stop
- Fail-controlled

![[Pasted image 20260304184456.png]]

---

# Failure Severity

Failures may be:

### Benign

- Loss of system functionality
- No severe consequences

### Malign

- Can cause accidents
- Potentially catastrophic outcomes

Systems where malign failures are possible are called **safety-critical systems**.

---

# Approaches to Achieve Reliable Systems

Two major approaches exist:

### Fault Prevention

Prevent faults from entering the system.

### Fault Tolerance

Allow system to continue operating despite faults.

Both aim to ensure **well-defined failure behavior**.

---

# Fault Prevention

Fault prevention consists of:

- **Fault avoidance**
- **Fault removal**

Fault avoidance techniques include:

- reliable hardware components
- improved hardware assembly
- interference protection
- rigorous specification of requirements
- proven design methodologies
- modular software design
- advanced programming languages

---

# Fault Removal

Fault removal involves detecting and eliminating faults.

Typical techniques:

- design reviews
- program verification
- code inspections
- system testing

Important limitation:

Testing can show the **presence of faults**, but never guarantee their absence.

Challenges include:

- incomplete testing conditions
- simulation inaccuracies
- requirement errors discovered only after deployment.

---

# Limits of Fault Prevention

Hardware components will eventually fail.

Fault prevention becomes insufficient when:

- repair frequency is unacceptable
- systems cannot be easily repaired

Example:

**Voyager 1 spacecraft**

- launched in 1977
- now about **25 billion km from Earth**

In such cases **fault tolerance** is essential.

---

# Bathtub Curve

Hardware failure rates follow the **bathtub curve**:

1. Early failures (infant mortality)
2. Constant failure rate
3. Wear-out failures

![[Pasted image 20260304184507.png]]

---

# Levels of Fault Tolerance

### Full Fault Tolerance

System continues functioning without significant performance loss.

### Graceful Degradation (Fail Soft)

System operates with reduced functionality.

### Fail Safe

System halts safely while maintaining integrity.

Most safety-critical systems aim for **full fault tolerance**, but many systems implement **graceful degradation**.

---

# Fault Detection

Fault tolerance requires:

- detection of faults
- predefined recovery behavior

Examples:

- communication systems detecting timing failures
- receivers detecting incorrect message values.

---

# Fault Hypothesis

Systems define a **fault hypothesis**:

- set of faults the system is designed to tolerate.

Rare faults outside this hypothesis may occur.

Example strategy:

### Never-Give-Up (NGU)

Example:

- watchdog timer resets system after severe fault.

![[Pasted image 20260304184526.png]]

---

# Exceptions

Exceptions represent abnormal system conditions.

Types of exceptions:

1. Environment-detected synchronous exceptions  
   Example: division by zero

2. Application-detected synchronous exceptions  
   Example: program-defined checks

3. Environment-detected asynchronous exceptions  
   Example: hardware failure monitoring

4. Application-detected asynchronous exceptions  
   Example: process detecting deadline violation.

---

# Exception Handling

Programs may define **exception handlers**.

Handlers respond to exceptional situations during execution.

The domain of an exception handler defines the code region where it applies.

---

# Exception Handling Example (C++)

```cpp
try
{
 int a=0;
 int b=42;
 int c = b/a;
}
catch (...)
{
 cout << "Exception detected..." << endl;
}
```

Another example:

```cpp
void doSomething(int Problem)
{
 if (Problem>0)
 {
 throw 5;
 }
}

int main()
{
 try
 {
 doSomething(1);
 }
 catch(int a)
 {
 cout << "Exception: " << a << endl;
 }
}
```

---

# Ariane 5 Failure Example

On **June 4, 1996**, the Ariane 5 rocket exploded shortly after launch.

Cause:

- software exception during floating-point conversion
- conversion from **64-bit float → 16-bit integer**
- value exceeded allowed range
- no exception handler implemented.

Loss:

Approximately **500 million dollars**.

see also: https://archive.eiffel.com/doc/manuals/technology/contract/ariane/

---

# Programming Language Support

Programming languages influence system dependability.

Important requirements:

- responsiveness
- reliability
- modifiability
- efficiency
- portability
- cost effectiveness

---

# Real-Time Language Requirements

Languages for real-time systems should provide:

- security
- readability
- flexibility
- simplicity
- portability
- efficiency

---

# Exception Handling Models

### Resumption Model

Handler fixes problem and execution continues.

### Termination Model

Handler stops operation.

### Hybrid Model

Handler decides whether execution resumes or terminates.

---

# Decomposition and Abstraction

Two key software engineering principles:

### Decomposition

Breaking a complex system into smaller components.

### Abstraction

Focusing on essential functionality while hiding implementation details.

---

# Modules

Modules encapsulate related data and operations.

Advantages:

- information hiding
- modular design
- independent compilation
- abstract data types

---

# Information Hiding

Module structure allows internal implementation details to remain hidden.

Examples:

- Ada: package specification and body
- C: header files (.h) and implementation files (.c)

---

# Abstract Data Types

Modules may define:

- a type
- operations on that type

Implementation details remain hidden.

In C:

- structures often hidden using pointers.

---

# Ada Programming Language

Developed for the **U.S. Department of Defense**.

Key features:

- modular programming
- strong typing
- built-in concurrency support
- standardized real-time capabilities

Current major version:

**Ada 2012**

---

# Ada Program Structure

Program units include:

- procedures
- functions
- packages
- tasks
- protected units

Library units:

- packages
- subprograms

Subunits:

- packages
- tasks
- protected units

---

# Example: "Hello World" in Ada

In a block structured language, like Ada, the domain is normally the block.

```
declare
subtype Temperature is Integer range 0 .. 100;
begin
-- read temperature sensor and calculate its value
exception
-- handler for Constraint_Error
end;
```

---

# Blocks in Ada

Block structure example:

```
declare
 subtype Temperature is Integer range 0 .. 100;
begin
 -- statements
exception
 -- error handler
end;
```

---

# C Programming

C language characteristics:

- low-level programming language
- sequential execution
- structured through functions
- flexible but less type-safe.

---

# Example C Function

```c
int largest(vector X, int len)
{
 int max = 0;
 int i;

 for (i = 0; i < len; i++)
 {
  if(X[i] > max) max = X[i];
 }

 return max;
}
```

Note:

C does **not provide native exception handling**.

---

# C++ Programming

C++ extends C with:

- object-oriented programming
- classes
- improved abstraction mechanisms

However:

C and C++ do not provide built-in mechanisms for **predictable real-time concurrency**.

Real-time applications typically rely on:

- RTOS
- specialized concurrency frameworks.

---

# Programming Language Comparison

Ada provides:

- built-in concurrency
- stronger type safety
- exception handling.

C/C++ provide:

- greater flexibility
- lower-level control
- but fewer built-in safety mechanisms.

---

# Summary

Key observations:

- Real-time systems require **precise specification**.
- Errors must be anticipated and failure behavior defined.
- Exception handling improves system robustness.
- Programming language choice strongly influences system dependability.

---

# Emerging Language: Rust

Rust emphasizes:

- performance
- memory safety
- safe concurrency

Website:

https://www.rust-lang.org/

---
# Controller Area Network (CAN) — Complete Introduction

This document explains the **Controller Area Network (CAN)** from first principles to practical system design.  
It is based on lecture material and Texas Instruments application reports.

Goal:  
Take someone with **0% knowledge of CAN → full conceptual understanding**.

---

# 1. Why CAN Exists

## Centralized Control

Traditional embedded systems often used **one microcontroller controlling everything**.

Problems with large systems:

- Large **wiring harness**
- Signal integrity issues
- High electromagnetic interference
- **Single point of failure**

---

## Distributed Control

Modern systems use **many microcontrollers communicating together**.

Advantages:

- Short sensor/actuator wiring
- Local preprocessing
- Better robustness
- Easier maintenance
- Modular architecture

Example domains:

- Automotive systems
- Robotics
- Industrial automation

Copy picture from **slide 3**.

---

# 2. What is CAN?

**Controller Area Network (CAN)** is a **serial communication bus** designed for distributed embedded systems.

Key facts:

- Developed by **Bosch in the 1990s**
- Widely used in **automotive electronics**
- Used in **robotics and automation**
- Supports **multi-master communication**

Modern cars may contain:

- up to **70 microcontrollers**
- multiple CAN networks

Copy picture from **slide 5**.

---

# 3. CAN Network Topology

CAN uses a **two-wire differential bus**.

Characteristics:

- Multi-master network
- Broadcast communication
- Up to **1 Mbit/s**
- All nodes connected to the same bus

Topology:

```
Node1 ----\
Node2 -----\ 
Node3 ------ CAN BUS ----- Node4
Node5 -----/
Node6 ----/
```

The bus is terminated at both ends.

Copy picture from **slide 9**.

---

# 4. What is a CAN Node?

Each device on the network is called a **node**.

A node consists of three components:

```
Application (software)

Microcontroller
     ↓
CAN Controller
     ↓
CAN Transceiver
     ↓
CAN Bus (CANH / CANL)
```

Functions:

| Component | Role |
|---|---|
| Microcontroller | runs application |
| CAN controller | protocol handling |
| CAN transceiver | electrical interface |

Copy picture from **slide 10**.

---

# 5. CAN Bus Electrical Signals

CAN uses **differential signaling**.

Two wires:

- **CANH**
- **CANL**

## Recessive State (logic 1)

```
CANH ≈ 2.5V
CANL ≈ 2.5V
Differential voltage ≈ 0V
```

## Dominant State (logic 0)

```
CANH ≈ 3.5V
CANL ≈ 1.5V
Differential voltage ≈ 2V
```

Advantages:

- High noise immunity
- Robust communication
- Reduced EMI

Copy picture from **page 8 of TI report**.

---

# 6. CAN Communication Model

CAN is a **broadcast communication system**.

Key idea:

Nodes do **not communicate directly with each other**.

Instead:

```
Node A broadcasts message → all nodes receive
```

Each node decides whether the message is relevant.

Nodes filter messages using the **message ID**.

Copy picture from **page 3 of the physical layer report**.

---

# 7. Message-Based Communication

Unlike Ethernet:

- Nodes do **not have addresses**

Instead:

- Messages have **identifiers**

The identifier defines:

- message meaning
- message priority

Example:

| ID | Meaning |
|----|--------|
| 0x050 | Wheel speed |
| 0x070 | Brake pressure |
| 0x091 | Battery voltage |

Nodes subscribe to messages they need.

---

# 8. CAN Frame Structure

Standard CAN frame:

```
SOF | Identifier | RTR | IDE | r0 | DLC | DATA | CRC | ACK | EOF
```

Detailed explanation:

| Field | Description |
|---|---|
| SOF | Start of frame |
| Identifier | Message ID (priority) |
| RTR | Remote transmission request |
| IDE | Identifier extension |
| DLC | Data length (0–8 bytes) |
| DATA | Message payload |
| CRC | Error check |
| ACK | Receiver acknowledgment |
| EOF | End of frame |

Maximum payload:

```
8 bytes
```

Copy picture from **slide 12**.

---

# 9. Standard vs Extended CAN

Two identifier formats exist.

## Standard CAN

Identifier size:

```
11 bits
```

Possible identifiers:

```
2^11 = 2048
```

---

## Extended CAN

Identifier size:

```
29 bits
```

Possible identifiers:

```
2^29 ≈ 537 million
```

Extended CAN adds:

- SRR bit
- IDE bit
- 18 additional identifier bits

---

# 10. Bit Stuffing

CAN uses **bit stuffing** for synchronization.

Rule:

After **5 consecutive identical bits**, insert **opposite bit**.

Example:

```
11111 → 111110
```

Purpose:

- maintain synchronization
- detect errors

Copy picture from **slide 16**.

---

# 11. Arbitration (Collision Handling)

Multiple nodes may transmit simultaneously.

CAN uses **non-destructive arbitration**.

Important rule:

```
Dominant (0) overrides recessive (1)
```

This is called **wired-AND behavior**.

Example:

Node A ID:

```
001101
```

Node B ID:

```
001111
```

Comparison bit-by-bit:

```
00110 → Node A wins
```

Result:

- Node B stops transmitting
- Node A continues

This ensures **no message corruption**.

Copy picture from **slide 19**.

---

# 12. Message Types

CAN defines four frame types.

## 1 Data Frame

Normal message containing data.

Fields:

- identifier
- payload
- CRC
- ACK

---

## 2 Remote Frame

Request for data.

Example:

Sensor node sends value on request.

---

## 3 Error Frame

Sent when error detected.

Causes retransmission.

---

## 4 Overload Frame

Used to delay communication when node is busy.

---

# 13. Error Detection Mechanisms

CAN is extremely robust.

Five error detection mechanisms exist.

### 1 CRC check

Message checksum verification.

### 2 ACK check

Receiver must acknowledge message.

### 3 Form check

Certain bits must be recessive.

### 4 Bit monitoring

Transmitter checks bus while sending.

### 5 Bit stuffing check

Detects stuffing violations.

If error occurs:

```
Error frame sent
Message retransmitted
```

Faulty nodes are eventually **disconnected automatically**.

---

# 14. Physical Layer Design

CAN networks require specific wiring rules.

## Cable

Recommended:

```
120 Ω twisted pair cable
```

---

## Termination

Bus must be terminated at both ends.

```
120 Ω resistor
```

Example:

```
120Ω --- CAN BUS --- 120Ω
```

Prevents signal reflections.

Copy picture from **page 7 termination diagram**.

---

# 15. Bus Length vs Data Rate

Trade-off between cable length and speed.

Typical values:

| Length | Speed |
|---|---|
| 40 m | 1 Mbps |
| 100 m | 500 kbps |
| 200 m | 250 kbps |
| 500 m | 100 kbps |
| 1000 m | 50 kbps |

Rule of thumb:

```
bitrate(Mbps) × cable_length(m) ≤ 50
```

---

# 16. Stub Length

Nodes connect via **short branches**.

Rule:

```
stub_length ≤ 1/3 of critical length
```

Example:

If driver transition time:

```
50 ns
```

Propagation delay:

```
5 ns/m
```

Critical length:

```
5 m
```

Maximum stub:

```
1.67 m
```

---

# 17. Bus Load

Bus load = percentage of time bus is transmitting.

Example:

Message size:

```
≈135 bits (worst case)
```

At **1 Mbps**:

```
135 µs per message
```

Maximum messages per millisecond:

```
≈7 messages
```

---

Example bus load calculation:

50 messages every 20 ms.

Broadcast time:

```
50 × 135 µs = 6.75 ms
```

Bus load:

```
6.75 / 20 = 34%
```

Acceptable.

---

# 18. Real Applications

CAN is used in many systems.

## Automotive

Different CAN networks:

- Body CAN
- Chassis CAN
- Powertrain CAN

Example bandwidths:

| Network | Speed |
|---|---|
| Body | 100 kbit/s |
| Chassis | 500 kbit/s |
| Powertrain | 500 kbit/s |

Copy picture from **slide 7**.

---

## Robotics

Example:

iCub humanoid robot.

Uses:

```
4 CAN buses
```

Copy picture from **slide 6**.

---

## Industrial Automation

Used for:

- motor drives
- PLC communication
- sensors
- actuators

Copy picture from **slide 8**.

---

# 19. Higher-Level CAN Protocols

CAN only defines **data link + physical layers**.

Higher-level protocols define:

- message formats
- device profiles

Examples:

| Protocol | Application |
|---|---|
| CANopen | industrial automation |
| DeviceNet | industrial networks |
| CAN Kingdom | embedded control |

---

# 20. Summary

Key properties of CAN:

- distributed control communication
- multi-master bus
- broadcast messaging# Controller Area Network (CAN) — Complete Introduction

This document explains the **Controller Area Network (CAN)** from first principles to practical system design.  
It is based on lecture material and Texas Instruments application reports.

Goal:  
Take someone with **0% knowledge of CAN → full conceptual understanding**.

---

# 1. Why CAN Exists

## Centralized Control

Traditional embedded systems often used **one microcontroller controlling everything**.

Problems with large systems:

- Large **wiring harness**
- Signal integrity issues
- High electromagnetic interference
- **Single point of failure**

---

## Distributed Control

Modern systems use **many microcontrollers communicating together**.

Advantages:

- Short sensor/actuator wiring
- Local preprocessing
- Better robustness
- Easier maintenance
- Modular architecture

Example domains:

- Automotive systems
- Robotics
- Industrial automation

Copy picture from **slide 3**.

---

# 2. What is CAN?

**Controller Area Network (CAN)** is a **serial communication bus** designed for distributed embedded systems.

Key facts:

- Developed by **Bosch in the 1990s**
- Widely used in **automotive electronics**
- Used in **robotics and automation**
- Supports **multi-master communication**

Modern cars may contain:

- up to **70 microcontrollers**
- multiple CAN networks

Copy picture from **slide 5**.

---

# 3. CAN Network Topology

CAN uses a **two-wire differential bus**.

Characteristics:

- Multi-master network
- Broadcast communication
- Up to **1 Mbit/s**
- All nodes connected to the same bus

Topology:

```
Node1 ----\
Node2 -----\ 
Node3 ------ CAN BUS ----- Node4
Node5 -----/
Node6 ----/
```

The bus is terminated at both ends.

Copy picture from **slide 9**.

---

# 4. What is a CAN Node?

Each device on the network is called a **node**.

A node consists of three components:

```
Application (software)

Microcontroller
     ↓
CAN Controller
     ↓
CAN Transceiver
     ↓
CAN Bus (CANH / CANL)
```

Functions:

| Component | Role |
|---|---|
| Microcontroller | runs application |
| CAN controller | protocol handling |
| CAN transceiver | electrical interface |

Copy picture from **slide 10**.

---

# 5. CAN Bus Electrical Signals

CAN uses **differential signaling**.

Two wires:

- **CANH**
- **CANL**

## Recessive State (logic 1)

```
CANH ≈ 2.5V
CANL ≈ 2.5V
Differential voltage ≈ 0V
```

## Dominant State (logic 0)

```
CANH ≈ 3.5V
CANL ≈ 1.5V
Differential voltage ≈ 2V
```

Advantages:

- High noise immunity
- Robust communication
- Reduced EMI

Copy picture from **page 8 of TI report**.

---

# 6. CAN Communication Model

CAN is a **broadcast communication system**.

Key idea:

Nodes do **not communicate directly with each other**.

Instead:

```
Node A broadcasts message → all nodes receive
```

Each node decides whether the message is relevant.

Nodes filter messages using the **message ID**.

Copy picture from **page 3 of the physical layer report**.

---

# 7. Message-Based Communication

Unlike Ethernet:

- Nodes do **not have addresses**

Instead:

- Messages have **identifiers**

The identifier defines:

- message meaning
- message priority

Example:

| ID | Meaning |
|----|--------|
| 0x050 | Wheel speed |
| 0x070 | Brake pressure |
| 0x091 | Battery voltage |

Nodes subscribe to messages they need.

---

# 8. CAN Frame Structure

Standard CAN frame:

```
SOF | Identifier | RTR | IDE | r0 | DLC | DATA | CRC | ACK | EOF
```

Detailed explanation:

| Field | Description |
|---|---|
| SOF | Start of frame |
| Identifier | Message ID (priority) |
| RTR | Remote transmission request |
| IDE | Identifier extension |
| DLC | Data length (0–8 bytes) |
| DATA | Message payload |
| CRC | Error check |
| ACK | Receiver acknowledgment |
| EOF | End of frame |

Maximum payload:

```
8 bytes
```

Copy picture from **slide 12**.

---

# 9. Standard vs Extended CAN

Two identifier formats exist.

## Standard CAN

Identifier size:

```
11 bits
```

Possible identifiers:

```
2^11 = 2048
```

---

## Extended CAN

Identifier size:

```
29 bits
```

Possible identifiers:

```
2^29 ≈ 537 million
```

Extended CAN adds:

- SRR bit
- IDE bit
- 18 additional identifier bits

---

# 10. Bit Stuffing

CAN uses **bit stuffing** for synchronization.

Rule:

After **5 consecutive identical bits**, insert **opposite bit**.

Example:

```
11111 → 111110
```

Purpose:

- maintain synchronization
- detect errors

Copy picture from **slide 16**.

---

# 11. Arbitration (Collision Handling)

Multiple nodes may transmit simultaneously.

CAN uses **non-destructive arbitration**.

Important rule:

```
Dominant (0) overrides recessive (1)
```

This is called **wired-AND behavior**.

Example:

Node A ID:

```
001101
```

Node B ID:

```
001111
```

Comparison bit-by-bit:

```
00110 → Node A wins
```

Result:

- Node B stops transmitting
- Node A continues

This ensures **no message corruption**.

Copy picture from **slide 19**.

---

# 12. Message Types

CAN defines four frame types.

## 1 Data Frame

Normal message containing data.

Fields:

- identifier
- payload
- CRC
- ACK

---

## 2 Remote Frame

Request for data.

Example:

Sensor node sends value on request.

---

## 3 Error Frame

Sent when error detected.

Causes retransmission.

---

## 4 Overload Frame

Used to delay communication when node is busy.

---

# 13. Error Detection Mechanisms

CAN is extremely robust.

Five error detection mechanisms exist.

### 1 CRC check

Message checksum verification.

### 2 ACK check

Receiver must acknowledge message.

### 3 Form check

Certain bits must be recessive.

### 4 Bit monitoring

Transmitter checks bus while sending.

### 5 Bit stuffing check

Detects stuffing violations.

If error occurs:

```
Error frame sent
Message retransmitted
```

Faulty nodes are eventually **disconnected automatically**.

---

# 14. Physical Layer Design

CAN networks require specific wiring rules.

## Cable

Recommended:

```
120 Ω twisted pair cable
```

---

## Termination

Bus must be terminated at both ends.

```
120 Ω resistor
```

Example:

```
120Ω --- CAN BUS --- 120Ω
```

Prevents signal reflections.

Copy picture from **page 7 termination diagram**.

---

# 15. Bus Length vs Data Rate

Trade-off between cable length and speed.

Typical values:

| Length | Speed |
|---|---|
| 40 m | 1 Mbps |
| 100 m | 500 kbps |
| 200 m | 250 kbps |
| 500 m | 100 kbps |
| 1000 m | 50 kbps |

Rule of thumb:

```
bitrate(Mbps) × cable_length(m) ≤ 50
```

---

# 16. Stub Length

Nodes connect via **short branches**.

Rule:

```
stub_length ≤ 1/3 of critical length
```

Example:

If driver transition time:

```
50 ns
```

Propagation delay:

```
5 ns/m
```

Critical length:

```
5 m
```

Maximum stub:

```
1.67 m
```

---

# 17. Bus Load

Bus load = percentage of time bus is transmitting.

Example:

Message size:

```
≈135 bits (worst case)
```

At **1 Mbps**:

```
135 µs per message
```

Maximum messages per millisecond:

```
≈7 messages
```

---

Example bus load calculation:

50 messages every 20 ms.

Broadcast time:

```
50 × 135 µs = 6.75 ms
```

Bus load:

```
6.75 / 20 = 34%
```

Acceptable.

---

# 18. Real Applications

CAN is used in many systems.

## Automotive

Different CAN networks:

- Body CAN
- Chassis CAN
- Powertrain CAN

Example bandwidths:

| Network | Speed |
|---|---|
| Body | 100 kbit/s |
| Chassis | 500 kbit/s |
| Powertrain | 500 kbit/s |

Copy picture from **slide 7**.

---

## Robotics

Example:

iCub humanoid robot.

Uses:

```
4 CAN buses
```

Copy picture from **slide 6**.

---

## Industrial Automation

Used for:

- motor drives
- PLC communication
- sensors
- actuators

Copy picture from **slide 8**.

---

# 19. Higher-Level CAN Protocols

CAN only defines **data link + physical layers**.

Higher-level protocols define:

- message formats
- device profiles

Examples:

| Protocol | Application |
|---|---|
| CANopen | industrial automation |
| DeviceNet | industrial networks |
| CAN Kingdom | embedded control |

---

# 20. Summary

Key properties of CAN:

- distributed control communication
- multi-master bus
- broadcast messaging
- priority-based arbitration
- strong error detection
- robust differential signaling

Important numbers:

```
Max speed: 1 Mbps
Max data: 8 bytes per frame
Typical nodes: ≤ 30
Cable: 120Ω twisted pair
```

---

# Final Intuition

Think of CAN as:

```
A shared conversation channel
where messages compete based on priority
and everyone hears everything.
```

Nodes only react to the messages they care about.

This makes CAN **simple, reliable, and scalable** for embedded systems.
- priority-based arbitration
- strong error detection
- robust differential signaling

Important numbers:

```
Max speed: 1 Mbps
Max data: 8 bytes per frame
Typical nodes: ≤ 30
Cable: 120Ω twisted pair
```

---

# Final Intuition

Think of CAN as:

```
A shared conversation channel
where messages compete based on priority
and everyone hears everything.
```

Nodes only react to the messages they care about.

This makes CAN **simple, reliable, and scalable** for embedded systems.

---

# Exam Preparation – Winter Term 2025/2026

TUM School of CIT – Chair of Robotics, Artificial Intelligence and Real-Time Systems (I6)

Course: **Real-Time Systems / Embedded Networked Systems**

---

# Exam Information

Course: **IN2060 – Real-Time Systems**

- **Date:** Thursday, 12 February 2026  
- **Time:** 14:00 – 15:30  
- **Locations:** multiple lecture halls (check TUMonline)

Important notes:

- The exam may take place in **4–5 different rooms**
- Seating plans will be posted at the entrance
- Students must check their **assigned seat and room in TUMonline**
- Information is updated **no later than Monday, February 9**

Example locations:

- Hörsaal 1A ("Zelt") – Room 5539.EG.001A  
- Hörsaal 1B ("Zelt")  
- Friedrich L. Bauer Hörsaal – Room 5602.EG.001  
- Galileo Hörsaal – Room 8120.EG.001  
- Hans-Fischer-Hörsaal – Room 5401.01.101K

---

# Embedded Networked Systems Exam

Course: **IN8014 – Eingebettete Vernetzte Systeme**

- **Date:** Thursday, 12 February 2026  
- **Time:** 14:00 – 15:30  
- **Location:** one lecture hall

Room:

- Hörsaal – Room 5508.02.801

All participants of IN8014 take the exam at this location.

---

# Exam Format

- **Closed-book exam**
- Language: **English**

Allowed materials:

- **One non-programmable calculator**
- **One analog dictionary** (English ↔ native language)

No other resources are allowed.

---

# Exam Structure

The exam consists of several problems covering different topics from the course.

---

# Problem 1 – Real-Time Basics

Topics include:

- Characteristics of real-time systems
- Interrupt timing and response time
- Clock synchronization concepts
- Event timing with distributed clocks
- Reliability concepts:
  - Fault
  - Error
  - Failure
- Resource-sharing protocols:
  - HLP (Highest Locker Priority)
  - NPP (Non-Preemptive Protocol)
  - PIP (Priority Inheritance Protocol)

---

# Problem 2 – Memory & Cache

Topics include:

- Cache locality effects
- Associative cache placement
- Cache eviction policies
- Direct-mapped cache
- Memory transfer mechanisms
- Cache metadata:
  - Tags
  - Valid bits
  - Dirty bits

---

# Problem 3 – Scheduling

Topics include:

- Scheduling algorithms
- Periodic task scheduling
- Aperiodic task scheduling
- Real-time scheduling constraints

---

# Problem 4 – Communication & Timing

Topics include:

- Network topology
- Hubs vs switches
- I/O communication protocols
- Fieldbus systems
- Ethernet-based industrial communication
- Line coding
- Bit stuffing
- Synchronization techniques
- Time synchronization protocols:
  - PTP (Precision Time Protocol)
  - NTP (Network Time Protocol)

---

# Problem 5 – C Programming

Students should understand:

- Basic C syntax
- Program analysis
- Control flow
- Memory and pointer concepts
- Real-time programming considerations

---

# Problem 6 – CAN Bus (Only for IN2060)

Topics include:

- CAN message frame
- Acknowledgment (ACK)
- Bus arbitration
- Bus length considerations
- Bit length and timing

---

# Important Note

**All exercise sessions are relevant for the exam.**

Students should review:

- lecture material
- exercises
- problem sheets
- examples discussed in tutorials.

---

# Final Message

Good luck with the exam!

---
