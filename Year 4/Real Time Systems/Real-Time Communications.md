# Real-Time Systems  
## Part 8: Real-Time Communication

TUM School of CIT – Chair of Robotics, Artificial Intelligence and Real-Time Systems (I6)

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

# Literature

- Wolfgang Hanlang, Juliane Benra – *Software-Entwicklung für Echtzeitsysteme*
- Hermann Kopetz – *Real-Time Systems: Design Principles for Distributed Embedded Systems*
- Documentation of protocol organizations (Profibus, EtherCAT, CAN)