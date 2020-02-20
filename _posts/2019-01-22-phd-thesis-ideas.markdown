---
layout: post
title:  "PhD Thesis Ideas"
date:   2020-01-22 07:30:00 -0500
categories: Ideas
published:  false
---

## Thesis topics in one sentence

1. How to answer *formally defined runtime behavior*
   using *available data* from a distribute cyber-physical system?

    - Data can come from hardware sensor/actuators, operating systems, or
      program states in user programs.
    - Formal interpretation however has to be in programming language level
      for developers to understand

2. Given a formal interpretation, what/how much data are sufficient/necessary to
   be *collected/stored*?


## Research Problems

All three problems below will require a formal definition of *traces*, i.e.,
reasonable abstractions of observable system executions.

#### Monitoring
Given a *formal specification* P, answer *online* if the *data* violates P.

Data -> Estimate of *current state* -> current state violates P

+ Lightweight
+ Fast

#### Replay
Reconstructing the runtime behavior up to some *precision*

+ initialization
+ recreate environments and environment changes

#### Prediction (Runtime Verification)

Using history/log
-> Estimate current state
-> Guarantee reaching good/bad states after T time/k-step ahead


### Formal Definitions and Specification Languages

Should consider error bound or error distributions.

#### Traces

Based on the definition in "Static and Dynamic Analysis of Timed Distributed Traces"
we can simplify/revise the definition to account for periodic sampling
and explore if this can help in monitoring/replaying/predicting.

#### Invariants

T: Non-negative continuous time?
I: index domain for parameterized system

    Forall i in I*, Forall t in T, inv<i>(t)

inv is limited to linear predicates.


## From data/logs to error-aware traces

**Question:** Can we prove that we must consider approximated or probabilistic
specification over values?
E.g., for counter-examples found in analyses using exact values,
the probability is ignorable.

### Availability and structure of different data with uncertainty

#### External (Observable from operating system or network)

+ Sensor/Actuator data from hardware devices

  - Time series (timestamped values).
    E.g., ROS topic messages with (precise) time stamps
  - Periodic/Aperiodic
  - **Error**: Value error bounds due to sampling rate, quantization, jitter, etc.

+ Distributed communication

  - Shared memory/message passing (timestamped messages or value updates)
  - Synchronous/Asynchronous
  - **Error**: Global clock, local clock, clock skew


#### Internal (Requires code instrumentation or user annotations)

+ Program States and Debugging traces
+ Storing/Logging

  - online/offline
  - log window size?

### Assumptions for error-aware definition of traces

+ Program logic does not rely on precise continuous time/clock for decisions
+ Perception errors are much larger than clock skew/jitter/sync errors

  - E.g., use Precise Time Protocol between robots

+ Timestamps on collected sensor/actuator values and communication messages are precise and ideal.

  - Or we can transform clock related errors to be over-approximated by perception errors

+ Centralized logs with partial order


## Related Topics

+ "Static and Dynamic Analysis of Timed Distributed Traces", Duggirala et al, RTSS 2012
+ "Verification of Annotated Models from Executions", Duggirala et al, EMSOFT 2013

  - Definition of traces and numerical simulation

+ Signal Temporal Logic for Runtime Verification,
  look for Ezio Bartocci et al
+ Monitoring Markov Chain, Markov Decision Procedure, Probabilistic CTL,
  look for Sistla Prasad's works
+ Work by Hussein and Daniel Liberzon on state estimation with finite bandwidth

  - "Optimal Data Rate for State Estimation of Switched Nonlinear Systems", HSCC 2017
  - "Entropy and Minimal Data Rates for State Estimation and Model Detection", HSCC 2016
