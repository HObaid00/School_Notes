# Real-Time Systems  
## Part 5: Real-Time Operating Systems

TUM School of CIT – Chair of Robotics, Artificial Intelligence and Real-Time Systems (I6)

---

# Content

- Introduction
- Operating system (OS) – basic definition
- Typical embedded system software with and without OS
- Special requirements for real-time operating systems
- Evaluation criteria for real-time operating systems

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

# Literature

- Tanenbaum – Modern Operating Systems
- Embedded.com RTOS resources
- Ubuntu Real-Time Linux documentation