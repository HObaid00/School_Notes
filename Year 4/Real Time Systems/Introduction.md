# Real-Time Systems / Embedded Networked Systems  
**Winter Term 2025/2026**  
TUM School of CIT – Chair of Robotics, Artificial Intelligence and Real-Time Systems (I6)  

Prof. Dr.-Ing. habil. Alois Knoll (on leave)  
Dr. Alexander Lenz  

---

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

## Lecturing Team

- Prof. Dr.-Ing. Alois Knoll  
- Dr. Alexander Lenz  

Exercises:
- Cary Jiang  
- Andre Schamschurko  
- Sven Kirchner  
- Nils Purschke  
- Chengdong Wu  

---

## Literature

- Lee, Seshia: *Introduction to Embedded Systems*  
  (available online via Berkeley Ptolemy website)

- Buttazzo, Giorgio: *Hard Real-Time Computing Systems*, 3rd edition, Springer  

- Kopetz, Hermann: *Real-Time Systems*, 2nd edition, Springer  

Additional references:
- Burns, Wellings: *Real-Time Systems and Programming Languages*
- Bennett: *Real-Time Computer Control*
- Gallmeister: *Programming for the Real World: POSIX.4*
- Liu: *Real-Time Systems*
- Li, Yao: *Real-Time Concepts for Embedded Systems*

---

## Additional Work (IN2060 – 6 credits)

- Additional self-study material (December)
- One exercise session dedicated to it
- One additional exam question

---

## Exam Bonus (Optional)

- Mini projects (pairs)
- Demonstration of embedded (real-time) system
- Report required
- Bonus: +0.3 marks  
  - Only if exam mark ∈ [1.3, 4.0]
  - Exam must be passed
  - Final grade cannot exceed 1.0

Details will follow on Moodle.

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

# Applications at the Chair

## Myorobotics (EU FP7)

- TMS570LS20216
  - 32-bit floating point
  - 140 MHz
  - FlexRay, CAN, SPI
- dsPIC33FJ128MC802
  - BLDC driver
  - Current sensors
  - Incremental encoder

📌 Copy pictures on slides 58–61.

---

## Practical Lab Course

Micromouse – Building a Robot from Scratch

📌 Copy pictures on slides 62–63.

---

## Real-Time at Our Chair

- Robotino
- Real-time Digital Twin (A9 Motorway)
- Stäubli robot
- Robotic Mouse (HBP)
- Roboy

📌 Copy picture on slide 64.

---

## Applications in Robotics

- Remote surgery
- JAST (ETH Zurich)
- HBP projects
- Autonomous robotic systems

📌 Copy pictures on slides 65–66.

---

# Project AURORA

Autonomous Robotic Surgery Assistance  
“Robotic Circulation Nurse”

📌 Copy picture on slide 66.

---

# End of Lecture

Thank you very much!  
Questions?  
See you next week!