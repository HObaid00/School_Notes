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