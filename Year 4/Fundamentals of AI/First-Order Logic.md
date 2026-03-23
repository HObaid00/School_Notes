## Why First-Order Logic
* Propositional Logic:
	* Declarative, compositional, context-independent
	* Very Limited expressive power
* FOL adds:
	* **Object, Relations (Predicates), Functions
* Much closer to natural language
FOL allows general rules without enumerating all cases.

## Key Advantages of FOL
* Represented objects, relations, and functions
* Closer to natural languages
* Can express general rules with quantifiers
## Ontology of FOL
* Propositional Logic: Facts only
* First Order Logic: Facts + Objects + relations
* Truth values remain: true/false/unknown
#### Objects
* Individual entities in the domain
* Examples: people, numbers, squares, colors
#### Relations (Predicates)
* Properties or relationships between objects
* Unary $\Large Red(x), King(x)$
* N-ary: $\Large Brother(x,y), Owns(x, y)$
#### Functions
* Map inputs -> exactly one output
* Example: $\Large Father(x), LeftLeg(x)$
#### Critical Distinction
* Functions return objects
* Predicates return true/false

## Syntax Elements
* Constants: "John", "2", "TUM"
* Variables: "x", "y", "z"
* Predicates: "Brother", "King", ">"
* Functions: "Mother", "Sqrt"
* Connectives: $\Large \neg, \land, \lor, \implies, \iff$
* Equality: $\Large =$
* Quantifiers: $\Large \forall, \exists$
Convention:
* Constants uppercase, Variables lowercase
## Terms
`Term ::= Function(Term,...) | Constant | Variable`
* A term **refers to an object**
* Think: complicated name, not a computation
Example:
`LeftLeg(John)`

## Atomic Sentences
Forms:
```
Predicate
Predicate(Term, ...)
Term = Term
```

Examples:
```
Brother(Richard, John)
Father(John) = Henry
Married(Father(Richard), Mother(John))
```
Predicates return true/false.

Equality Usage:
* Assert Usage
* Assert non-Identity
## Complex Sentences
Built using connectives and quantifiers:
* Logical Connectives
* Quantifiers 

Examples:
```
¬P
P ∧ Q
P ∨ Q
P ⇒ Q
P ⇔ Q
∀x P
∃x P
```
$Brother(Richard, John) ∧ Brother(John, Richard)$ 
$\neg King(Richard) \implies King(John)$
## Universal Quantifier ($\forall$)
* Meaning: Sentences must be true for every object
* Typical Pattern: $\forall x \quad P(x) \implies Q(x)$
* Key Rule: $\implies$ is usually the main connective with $\forall$ 
## Existential Quantifiers ($\exists$)
* Meaning: Sentence true for at least one (there exists at least one)
* Typical Patter: $\exists x \quad P(x) \land Q(x)$
* Key rule: $\land$ is the main connective with $\exists$

## Common Quantifier Mistakes
For $\forall$:
*  $\forall x \quad At(x, TUM) \land Smart(x)$ is Wrong
* Means: Everyone is at TUM AND everyone is smart
* $\forall x \quad At(x, TUM) \implies Smart(x)$ is Correct
* Means if you are at TUM IMPLIES you are smart

For $\exists$:
* $\exists x \quad At(x, TUM) \implies Smart(x)$ is Wrong
* Means: True if anyone is not at TUM
* $\exists x \quad At(x, TUM) \land Smart(x)$ is Correct
* Means: There exists at least one who is at TUM AND is smart

## Scope Quantifiers
Definition:
* The past of the formula where the quantifier applies
Rules:
* Parentheses make scope exploit
* Otherwise, quantifier applies as far right as possible
Example
* $\forall x \quad \exists y \quad \exists z \quad P(x, y, z) \equiv \forall x \quad(\exists y \quad(\exists z \quad P(x,y,z)))$

## Variables and Binding 
* Rule: A variable is bound by the innermost quantifier
* Best Practice: Avoid reusing variable names in nested quantifiers

## Nested Quantifiers
* Same-type Quantifiers: Order does not matter
	* $\forall x \quad \forall y \equiv \forall y \quad \forall x$
	* $\exists x \quad \exists y \equiv \exists y \quad \exists x$
* Different-type Quantifiers: Order matters
	* $\forall y \quad \exists x \quad Loves(x,y)$: Everyone is loved by someone
	* $\exists y \quad \forall x \quad Loves(x,y)$: Someone Loves Everyone
## Relationship Between $\forall$ and $\exists$
* Quantifier duality;
	* $\forall x \quad P \equiv \neg\exists x \quad \neg P$
	* $\exists x \quad P \equiv \neg\forall x \quad \neg P$
User for transformation and reasoning

## Knowledge Engineering in FOL (Process)
1. Identify the task
2. Gather domain knowledge
3. Choose Vocabulary (ontology)
4. Encode general axioms
5. Encode specific facts/instances
6. Pose Queries
7. Debug the knowledge base
Good ontology makes everything easier

## Assertions vs Queries
Assertions (Tell)
* Add facts/rules to KB
* Examples: 
	* $Tell(KB, \quad King(John))$
	* $Tell(KB, \forall x \quad King(x)) \implies Person(x)$
Queries (Ask/AskVars):
* Ask -> yes/no
* AskVars -> Variable Binding
* Example:
	* $AskVars(KB, \quad \exists x \quad Person(x)) \rightarrow (x/John), (x/Richard)$


## Typical Exam Tasks
* Translated English -> FOL
* Identify correct formula among choices
* Spot quantifiers/connective mistakes
* Determine meaning of nested quantifiers
* Distinguish object vs predicate vs function
* Decide if sentence is well-formed
## Summary
* FOL extends propositional logic with Objects, relations, functions
* Syntax build on propositional logic
* Quantifiers enable compact general rules
* $\forall$ usually pairs with $\implies$ , $\exists$ with $\land$
* Quantifiers order matters
* Knowledge bases assertions and queries
* Knowledge engineering in a structured process
---
# Inference First-Order Logic
Problem:
* Propositional inference is decidable and complete
* FOL is more expressive but harder to reason with
Objective:
* Perform sound and (as far as possible) complete inference in FOL
* Avoid full propositionalization where possible

## Reducing FO Inference to Propositional Inference
Key Idea:
* Removing quantifiers to obtain ground (variable-free) sentences
* Apply propositional inference techniques
## Universal Instantiation (UI)
* Rule: Infer any  sentence from substituting a **ground term** (a term without variables) for the variable.
* We denote the result of applying the substitution $\Large \theta$ to the sentence $\Large \alpha$ so that:

$$
\Large \frac{\forall v \quad \alpha}{Subst(\{v/g\}), \alpha}
$$
	Where $\Large \{v/g\}$ means $\Large v$ gets replaced by $\Large g$. 
* Examples: 
$$
\Large \forall x \quad King(x) \land Greedy(x) \implies Evil(x) 
$$$$ 
\Large \implies King(John) \land Greedy(x) \implies Evil(John)
$$
* Properties
	* Can be applied multiple times
	* Preserve logical equivalence of the KB.
## Existential Instantiation (EI)
* When Existential quantifiers appear, replace a variable by a single *new constant symbol*.
* More formally: For any sentence $\Large \alpha$, variable $\Large v$ and constant symbol $\Large k$ that does not appear elsewhere in the knowledge base:
$$
\Large \frac{\exists v \quad \alpha}{Subst(\{v/k\}, \quad \alpha)}
$$
	Examples: 
	$$\Large \exists x \quad
	Crown(x) \land OnHead(x, John)
	$$
	yields
$$\Large  
Crown(C_1) \land OnHead(C_1, John)
$$
	provided $\Large C_1$ is a new constant symbol, called a  **Skolem constant***. 

Properties:
* Applied once
* Resulting KB is not equivalent, but equisatisfiable.
## Propositionalization: Benefits & Problem
Benefits:
* Allow reuse  of propositional resolution
Problem:
* Explosion of irrelevant ground sentence
* With $\Large p$ predicts, $\Large n$ constants, arity k -> $p \times n^k$ instantiations
* With function symbols -> infinitely many ground terms
Key Results:
* Entailment in FOL is semidecidable
	* if entailed -> algorithm eventually says "Yes"
	* if not entailed -> may never terminate

## Generalized Modus Pones (GMP)
Motivation:
* Avoid full propositionalization
* Perform inference directly in FOL
Core Inference Rules From:
* $\Large p_1', ... , p_n'$
* $(\Large p_1 \land ... \land p_n \implies q)$
	If there exists a substitution $\Large \theta$ such that $\Large Subst(\theta,p_i') \equiv subst(\theta, p_i)$  $\Large \forall i$ 
	Then infer  $\Large Subst(\theta,q)$
Example:
* $\Large \forall x \quad King(x) \land Greedy(x) \implies Evil(x)$
* $\Large King(John), \quad Greedy(John)$
* $\Large \theta = \{x/John\} \implies Evil(John)$
Key Insight
* GMP is a lifted version of Modus Pones
## Unification
* Purpose: Find substitution that make expressions Identical
* Definition: $\Large Unify(p, q) = \theta$ such that $\Large Subst(\theta, p)=Subst(\theta, q)$
* Example 

| $\Large p$              | $\Large q$                    | $\Large Results$                       |
| ----------------------- | ----------------------------- | -------------------------------------- |
| $\Large Knows(John, x)$ | $\Large Knows(John, Jane)$    | $\Large \{x/Jane\}$                    |
| $\Large Knows(John, x)$ | $\Large Knows(y, Elisabeth)$  | $\Large \{x/Elisabeth, \quad y/John\}$ |
| $\Large Knows(John, x)$ | $\Large Knows(x, Elisabeth )$ | $\Large Fail$                          |
## Important Techniques
* Standing apart: Rename variables to avoid clashes
* Always prefer the most general unifier (MGU).

## First Order Horn Clauses
Definition:
* Atomic Sentences
* $\Large (p_1 \land ... \land p_n \implies q)$
* Variables are implicit universally quantified
Importance:
* Enables forward chaining 
* Efficient and widely used

## Forward Chaining in FOL
Main Idea:
* Goal Driven
* Starts with the query, reduce to sub-goal
Algorithm Characteristics:
* Depth-first, recursive
* Uses unification to match goals with conclusion
Properties
* Linear space complexity
* Can loop infinitely 
* Common Programming logic

## Forward Chaining Vs. Backwards Chaining
| Aspect      | FC                  | BC                     |
| ----------- | ------------------- | ---------------------- |
| Direction   | Data -> Goal        | Goals -> Data          |
| Control     | Bottom-up           | Top-down               |
| Efficiancy  | Good for many facts | Good for few questions |
| Termination | Not guaranteed      | Not guaranteed         |
## Resolution in FOL
Goal:
* Achieve complete proof procedure for FOL
* Resolution: is refutation-complete
Conjunction Normal Form (CNF)
* Literals may contain variables
* All variables are implicitly universally quantified
CNF Conversion Step
1. Eliminate $\Large \iff$
2. Eliminate $\Large \implies$
3. Move $\Large \neg$ inward (quantifier rules apply)
4. Standardize variables
5. Skolemization (remove $\Large \exists$)
6. Drop $\Large \forall$
7. Distribute $\Large \lor$ or $\Large \land$

## Skolemization
Replace existential variables with:
* Constants, or
* Functions or surrounding universally quantified variables
Key rules:
* Arguments of Skolem function = universally quantified variables in scope

## Resolution Rule in FOL
Rule from:
* $\Large l_1 \lor ... \lor l_k$
* $\Large m_1 \lor ... \lor m_n$
if $\Large Unify(l_i, \neg m_j) = 0$ infer
* $\Large Subst(\theta, \quad remain \quad literals)$
Example of Resolve:
* $\Large Loves(G(x), x)$
* $\Large \neg Loves(u,v)$

## Proof by Resolution
Procedure: To show $\Large KB \models \alpha$
1. Add $\Large \neg \alpha$ to $KB$
2. Convert all sentences to CNF
3. Apply resolution repeatedly
4. Empty clauses $\implies$ contradiction $\implies$ entailment proven

## Completeness of Resolution
* Resolution in FOL is refutation-complete
* If a sentence is unsatisfiable, resolution will find a contradiction
* If satisfiable, resolution may not terminate
## Summary 
* Quantifier elimination via UI and EI
* Propositionalization preserves entailment but is inefficient
* Generalized Modus Pones enable lifted inference
* Unification + MGU are central tools
* Forward & Backward Chaining apply to Horn Clauses
* CNF conversion requires Skolemization
* Resolution is refutation-complete for FOL*