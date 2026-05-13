# Hardware Timers

A **hardware timer** is a counter driven by a clock. Timers allow embedded systems to wake up, schedule jobs, measure time, and trigger interrupts.

A timer with frequency $f$ has tick duration:

$$\Large
T_{tick} = \frac{1}{f}
$$

If the system clock is $8\,\text{MHz}$ and the prescaler is $8$, then the timer frequency is:

$$\Large
f_{timer} = \frac{8\,\text{MHz}}{8} = 1\,\text{MHz}
$$

so one tick is approximately:

$$\Large
T_{tick} = 1\,\mu s
$$

A comparator can trigger an interrupt when the timer reaches a selected value.

---

## Links

[[Edge Computing & IoT]]
