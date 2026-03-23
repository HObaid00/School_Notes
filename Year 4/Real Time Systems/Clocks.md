# Real-Time Systems  
## Part 2: Time and Clocks

TUM School of CIT – Chair of Robotics, Artificial Intelligence and Real-Time Systems (I6)

Partly based on:  
H. Kopetz, *Real-Time Systems*, 2nd Edition, Chapter 3, 2011, Springer

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

# Literature

- Kopetz, *Real-Time Systems*
- Tanenbaum, *Distributed Systems*
- IEEE 1588
- GPS official site
- PTB

---

# Questions

- Difference between instant and event?
- How does synchronization help in alarm analysis?
- Fundamental limits of time measurement?