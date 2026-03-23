# Real-Time Systems  
## Part 9: Dependability

TUM School of CIT – Chair of Robotics, Artificial Intelligence and Real-Time Systems (I6)

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

# Literature

- H. Kopetz — *Real-Time Systems*
- P. A. Laplante — *Real-Time Systems Design and Analysis*
- A. Burns & A. Wellings — *Real-Time Systems and Programming Languages*
- Avizienis, Randell, Landwehr — *Basic Concepts and Taxonomy of Dependable and Secure Computing*