---
layout: post
title:  "More Research Directions and Ideas"
date:   2020-11-16 07:30:00 -0500
categories: Ideas
published:  true
---

# Directions

Light weight formal approaches applicable to problems in V&V of distributed CPS with (some of) the following traits:

+ Middle to large scale/numbers of agents
+ Complex/realistic examples

Evaluation and validation of our approaches using ROS Gazebo simulations

+ Large amount of simulations
+ Large number of agents


## Decomposition of Communication and Continuous Dynamics

Extension/revision of Koord

+ Message passing style, Actor model
  - Thespian, a Python package for programming in Actor model
+ Asynchrony, partial synchrony
+ Fault tolerant, failure recovery
  - Reliable vs out of order delivery
+ Safety and Liveness guarantees for distributed coordination under local assumptions
  - Precise safety and liveness for an agent can be very difficult to provide
  - Empirical/statistical/probabilistic provided by local monitoring or local models


## Runtime Verification/Testing of Distributed CPS with Timed Distributed Traces

See previous posts.


## Verification/Debugging of protocols built on publish/subscribe architecture (ROS)

Debug or verify ROS ActionLib

Predicate detection problem
+ Monitoring global predicates

Deterministic scheduling and replay in different abstraction levels and areas
+ Operating system level support
  - Liblog https://static.usenix.org/events/usenix06/tech/geels/geels.pdf
  - Flashback: A Lightweight Extension for Rollback and Deterministic Replay for Software Debugging
+ Distributed realtime systems
  - Towards Lightweight Logging and Replay of Embedded, Distributed Systems, https://hal.archives-ouvertes.fr/hal-00848180
  - Using deterministic replay for debugging of distributed real-time systems, Euromicro RTS 2000

Web
+ Interactive record/replay for web application debugging, UIST 2013

Software failure reproduction
+ A Search-Based Framework for Failure Reproduction, SSBSE 2012
+ ReCrash: Making Software Failures Reproducible by Preserving Object States, ECOOP 2008

ROS Gazebo discussion
+ https://answers.gazebosim.org//question/25010/repeatability-of-experiments-and-determinism-of-gazebo-simulation/
+ https://discourse.ros.org/t/deterministic-replay-and-debugging/1316
+ https://roscon.ros.org/2018/presentations/ROSCon2018_Mozilla_rr.pdf
  - Video: https://vimeo.com/293623186
  - Only for single ROS node with multiple threads


## Formalization of centralized approaches for UTM and analyses using Gazebo simulation

Based on our work "SkyTrakx: A Toolkit for Simulation and Verification of Unmanned Air-Traffic Management Systems", ITSC 2021

UTM sets up a good narrative and problem scope for centralized approaches
+ It must be centralized because UTM is likely coordinating aircraft from different delivery companies for example.
  - Distinguish us from Drona and many other decentralized approaches for distributed planning
  - More related to TCAS and ACAS family, but deals with finer space-time partitions and low-altitude terrain and obstacles.
+ Using abstraction of continuous dynamics, path planning, and controllers is natural and **necessary**
  - because UTM and its agent-side protocol have to support various kinds of unmanned aircraft.
  - Besides distributed coordination, difficulties also come from less control and information on aircraft states.

Ideas and extensions from the submission

New protocols
+ Timing based
+ Geo info based

Violation detection, safety under bounded violation of contract
+ Violation can be detected by agent side protocol
+ Bounded violation means violation is always resolved within some time period OR some distance traveled.
  - Violation not caused by failure but by overly strict contracts are mostly resolved shortly

Failure report, safety under failure with or without recovery
+ Failure should be decided and reported by aircraft. Failure recovery is also done by the aircraft and can be abstracted.
  - Failure can induce violation, but it is neither a necessary nor sufficient condition.
  - UTM observes only violations and needs a report to know the failure.
+ Notification to other aircraft and reassign contracts
+ However, (hardware) failure for CPS is typically very specific to the dynamics and the model
  - Decompose fail action (general comm.) from its message (specific datatype with semantics)

Centralized monitoring and prediction with limited state information
+ Using only observed positions and approved contracts instead of full dynamic model

Improvements on the submission
+ Measuring failure related behavior
  - It is done in the last minute, and we didn’t discuss them thoroughly.
+ Unclear “formal” models
  - We didn’t know whether the agent automaton is a hybrid I/O automaton or not.
  - We should be able to move the abstraction of trajectory control out of the agent automaton, and make it a simple IOA only for communication.
  - Locally monitoring the violation can be a separated HIOA with only clock and position as continuous variables
+ Lack of discussion in the following
  - Static obstacles
  - From a global clock to local clocks with skews
  - Communication delays in liveness proof

Improvements and extensions on implementation and running experiments
+ Reliable and correct implementation/refinement of the protocol
+ It seems a fixed delta period is assumed between each iteration of actions, but the implementation does not
+ Introduce communication delays and message drops
+ Evaluate scalability over more metrics
  - Flight paths
+ Ad-hoc logging which makes collecting extra data from experiment result not easy