## Core Definition
* Intelligent Agent
	* An entity that perceives its environment through *sensors* and *acts* upon the environment through *actuators*
* Interaction Loop:
	* Environment -> Sensors -> Agent -> Actuators -> Environment
* Agent can be software or hardware

## Agents VS Control Systems
* Control Theory distinguishes *plant and environment*
* AI perspective often merges both into single environment
* Key distinction: AI agent reasons and decides, doesn't only regulate

## Precepts, Precept Sequences, and Agent Functions
* Precept: Agents immediate sensory input
* Precept Sequence: Complete history of precepts.
* Agent Function: Mapping function f: Precept Sequence -> Action
* Longer precept histories allow more informed decisions

## Agent Program VS Agent Functions
* Tabular agent functions
	* Theoretically expressive
	* Practically infeasible (astronomical size)
* Agent Programs
	* Compact, executable implementations of agent functions
	* The only practical solution - [[Rational Agent]], [[Omniscience]], [[Learning]], and [[Classification with Piecewise Linear Functions]]

## Rational Agents
* "Rationality": Doing the "right thing" according to a performance measure
* A rational agent:
	* Maximize expected performance 
	* Is not Omniscient
* Rational action depends on:
	* Performance measure
	* Prior Knowledge
	* Available action
	* Precept sequence so far

## Omniscience, Learning, and Autonomy
* Omniscience Agent: Knows actual outcomes of actions (impossible in reality)
* Learning Agent: improves knowledge from experience.
* Autonomy: 
	* Less reliance on build-in knowledge
	* Greater reliance on learned behavior
* More Learning  -> more autonomy

## Task Environment and PEAS
To design a rational agent, specify its task environment using PEAS:
* Performance measure
* Environment
* Actuators
* Sensors

Examples:
* Automated taxi
* Integrated shopping agent

## Properties of Task Environment (**Must Memorize**)
1. Fully observable Vs. Partially observable
2. Single Agent Vs. Multi Agent
3. Deterministic Vs. Stochastic
4. Episodic Vs. Sequential
5. Discrete Vs. Continuous (state and time)
6. Static Vs. Dynamic
7. Known  Vs. Unknown
These properties determine **agent design complexity**

## Types of Agents (Increasingly Generality)
1. [[Simple Reflex Agent]]
	* Act only on current perception
	* Use Condition-Action rules
	* Require fully observable environments
2. [[Model Based Reflex Agents]]
	* Maintain internal state
	* Handle partial observability
3. [[Goal-Based Agents]]
	* Choose action based on future goal achievement
	* Use searching and planning
4. [[Utility Based Agents]]
	* Maximize expected utility (trade-off between goals)
5. [[Learning Agents]]
	* Improve performance over time
	* Can extend any of the above types

## Learning Agent Architecture
Components:
* Performance element-selection actions
* Learning element - improves behavior
* Problem generator - encourages exploration
Key Idea: Learning modifies the agent decision-making over time

