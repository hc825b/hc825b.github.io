---
layout: page
title: Research Projects
permalink: /projects/
---

My broad research direction is the formal *assurance* of the cyber-physical system (CPS) containing complex components that are incompletely specified or currently intractable for existing formal verification techniques.

In my study, I have been investigating several systems containing incomplete vehicle dynamics, vision-based perception pipelines, communication protocols, or combinations of all.
The main intuition behind all case studies is to achieve the *separation of concerns* via abstractions of components.
We repeatedly apply the abstraction then refinement principle to decompose the verification problem of CPS into component level verification subproblems.

With this principle in mind,
the crucial step is to select a proper abstraction for each component that is suitable for domain specific formal analyses.


## Programming Abstractions for Distributed Robotics

Project Website: <https://cyphyhouse.github.io>  

I have been in the CyPhyHouse team since Summer 2018. CyPhyHouse aims to provide programming, debugging, and deployment for distributed robotic applications (DRAs). Users can develope distributed applications using the high-level, hardware-agnostic, event driven Koord programming language included with CyPhyHouse, without requiring deep expertise in controller design or distributed network protocols.

One key abstraction provided by the Koord language is *synchronous logically*.
That is, Koord program language aims to provide a synchronous round-based semantics though physically running on a distributed asynchronous multi-robot system.
Under this language semantic, the *Koord users*, such as control theorist, can design the high level coordination logic with much simpler synchronous executions in mind.
The *Koord compiler developers* focus on design and implement the middleware that achieves the synchronous semantics with a well-defined set of asynchronous communication primitives such as *Physically-Asynchronous Logically-Synchronous (PALS)* System.
The *hardware platform developers* then concentrates on supporting the robot control commands delivered through the communication primitives for each kind of vehicles.

On the other thread, we study CPS with an asynchronous communication model, Input/Output Automata.
In order to achieve the separation between communication and robot control, we restrict the communication to share only *intent information* .
Under this context, each robot shares its plan of movement, for instance, Operational Volumes for UAS traffic management.
The communication protocol is used to ensure the plans from different robots are not conflicting.
This reduces the problem of distributed communication to well studied consistency and mutual exclusion protocols.
Then, each robot should abide by its shared intent for the planned time horizon.
The abstraction can happen in planning to over-approximate the true physical behavior with a more conservative plan.
In short, we show this approach to be effective on UAS traffic management and smart manufacturing systems.

Such separation of concerns not only lowers the barrier of programming DRAs but also decomposes the verification and debugging tasks for the communication components (platform independent) and robot control components (platform dependent).
Different tasks can then be addressed by the developers with specific expertise.


### Presentation Videos

<iframe width="32%" src="https://www.youtube.com/embed/bxPmpVuFcQM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="32%" src="https://www.youtube.com/embed/Hf8OUsXBIhc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="32%" src="https://www.youtube.com/embed/VMLmOHSlmj4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br/>

### References ordered by relevance
+ Ghosh et al., *Koord: a language for programming and verifying distributed robotics application*, OOPSLA 2020
+ Ghosh et al., *CyPhyHouse: A programming, simulation, and deployment toolchain for heterogeneous distributed coordination*, ICRA 2020
+ Hsieh et al., *SkyTrakx: A Toolkit for Simulation and Verification of Unmanned Air-Traffic Management Systems*, ITSC 2021
+ Hsieh et al., *Programming Abstractions for Simulation and Testing on Smart Manufacturing Systems*, CASE 2022
+ Chiao Hsieh and Sayan Mitra, *Dione: A Protocol Verification System Built with Dafny for I/O Automata*, iFM 2019


## Assurance for Vision-Based Control Systems

Under construction.


### References ordered by relevance:
+ Hsieh et al., *Verifying Controllers with Vision-based Perception using Safe Approximate Abstractions*, EMSOFT 2022
+ Hsieh et al., *Assuring safety of vision-based swarm formation control*, Under submission to ICRA 2023


## Epilogue: Safety assurance in addition to testing and simulation

Current best practices for the safety assurance of cyber-physical systems relies on extensive testing and simulating the systems to exhibits safety violations and falsify the design and implementation.
These approaches however suffers from the fact that unsafe events are inherently rare events.
Hence, the required amount of simulation and testing to find safety violations can be prohibitively high. (**TODO** Link to driving millions of miles to achieve human performance.)

In comparison, our approaches for the safety assurance stem from the formal safety proof of the approximated abstract system.
We can guarantee the worst case behavior of the approximated system will not violate the system requirement.
