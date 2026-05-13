# Session 5: Rule-Based Models of Legal Reasoning

---

## Legal Expert Systems

- Represent legal knowledge  
- Provide:
  - Advice  
  - Decisions  
  - Automation  

---

## Transition Model (Contracts)

States:

- Offer  
- Acceptance  
- Contract  

➡️ Insert figure: transition network (page 6) :contentReference[oaicite:15]{index=15}  

---

## Propositional Logic

Basic rule:

$$\Large A \land B \Rightarrow C$$

Example:

$$\Large \text{offer} \land \text{acceptance} \Rightarrow \text{contract}$$

---

## Logic Operators

- $\Large \neg$ (NOT)  
- $\Large \land$ (AND)  
- $\Large \lor$ (OR)  
- $\Large \Rightarrow$ (IMPLIES)  

---

## Horn Clauses

$$\Large (R_1 \land R_2) \Rightarrow C$$

Used in:

- Prolog  
- Rule-based systems  

---

## Example Rule

$$\Large \text{vehicle}(X) \land \text{at}(X, park) \Rightarrow \text{violation}(X)$$

---

## British Nationality Act Model

- Encoded as logic program  
- ~150 rules  

➡️ Insert figure: BNA logic tree (page 13) :contentReference[oaicite:16]{index=16}  

---

## Challenges

### Non-monotonic Logic

- New facts can invalidate conclusions  

### Negation as Failure

- Assume false if not provable  

---

## Open Texture Problem

Example:

- “No vehicles in park”

Questions:

- Is a bike a vehicle?  
- Is a tank a vehicle?  

➡️ Insert figure: open-texture example (page 28) :contentReference[oaicite:17]{index=17}  

---

## Summary

- Legal reasoning can be formalized  
- Logic systems powerful but limited  
- Real-world law requires:
  - Exceptions  
  - Interpretation  
  - Context  