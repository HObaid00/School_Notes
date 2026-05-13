## Scheduling vs Reactive Operating Systems

A traditional operating system often uses **scheduling**: it decides which process or thread runs at a given time.

A reactive IoT OS often avoids full preemptive scheduling and instead processes events from an event queue.

| Model | How work starts | Advantage | Disadvantage |
|---|---|---|---|
| Reactive | Event occurs | Energy efficient, simple | Long handlers reduce responsiveness |
| Scheduled | Scheduler chooses task | Better multitasking | More memory and synchronization overhead |

Preemptive scheduling can interrupt one task to run another. This improves responsiveness but makes programs harder to reason about because shared data may change unexpectedly.

---

## Links

[[Edge Computing & IoT]]
