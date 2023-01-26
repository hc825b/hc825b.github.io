---
layout: page
title: Research Projects
permalink: /projects/
---

My broad research direction is the *formal assurance* of the cyber-physical system (CPS) containing complex components that are incompletely specified or currently intractable for existing formal verification techniques.

I have been investigating several systems containing incomplete vehicle dynamics, vision-based perception pipelines, communication protocols, or combinations of all.
The main intuition behind all case studies is to achieve the *separation of concerns* via abstractions of components.
We repeatedly apply the abstraction then refinement principle to decompose the verification problem of CPS into component level verification subproblems.

With this principle in mind,
the crucial step is to select a proper abstraction for each component that is suitable for domain specific formal analyses.


## Programming Abstractions for Distributed Robotics

Project Website: <https://cyphyhouse.github.io>  

I have been in the CyPhyHouse team since Summer 2018. CyPhyHouse aims to provide programming, debugging, and deployment for *distributed robotic applications (DRAs)*. Users can develope distributed applications using the high-level, hardware-agnostic, event driven Koord programming language included with CyPhyHouse, without requiring deep expertise in controller design or distributed network protocols.

One key abstraction provided by the Koord language is *synchronous logically*.
That is, Koord program language aims to provide a synchronous round-based semantics though physically running on a distributed asynchronous multi-robot system.
Under this language semantic, *Koord users*, such as control theorists, can design the high level coordination logic with much simpler synchronous executions in mind.
*Koord compiler developers* focus on design and implement the middleware that achieves the synchronous semantics with asynchronous communication primitives, i.e., [*Physically-Asynchronous Logically-Synchronous (PALS)* System][PALS].
*Hardware platform developers* then concentrate on supporting the robot control commands delivered through the communication primitives for each kind of vehicles.

[PALS]: http://publish.illinois.edu/cpsintegrationlab/rtsi-projects/architecture-design-and-analysis/complexity-reduction/physically-asynchronous-logically-synchronous-pals-system/


This division of roles and tasks also matches my personal experiences in the CyPhyHouse team.
ECE students with multi-agent control theory background serve as Koord users and design coordinations algorithms in the Koord language.
CS students including myself with distributed communication and compiler design knowledge act as Koord compiler developers and implement distributed shared memory over UDP broadcast.
MechEng students are hardware platform developers and focus on the positioning and trajectory tracking for drones and racecars using Robot Operating System (ROS).


On the other thread, we study CPS with an asynchronous communication model, Input/Output Automata.
In order to achieve the separation between communication and robot control, we restrict the communication to share only *intent information*.
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
+ Ghosh et al., *Koord: A Language for Programming and Verifying Distributed Robotics Application*, OOPSLA 2020, doi:[10.1145/3428300](https://doi.org/10.1145/3428300)
+ Ghosh et al., *CyPhyHouse: A Programming, Simulation, and Deployment Toolchain for Heterogeneous Distributed Coordination*, ICRA 2020, doi:[10.1109/ICRA40945.2020.9196513](https://doi.org/10.1109/ICRA40945.2020.9196513)
+ Hsieh et al., *SkyTrakx: A Toolkit for Simulation and Verification of Unmanned Air-Traffic Management Systems*, ITSC 2021, doi:[10.1109/ITSC48978.2021.9564492](https://doi.org/10.1109/ITSC48978.2021.9564492)
+ Hsieh et al., *Programming Abstractions for Simulation and Testing on Smart Manufacturing Systems*, CASE 2022, doi:[10.1109/CASE49997.2022.9926564](https://doi.org/10.1109/CASE49997.2022.9926564)
+ Chiao Hsieh and Sayan Mitra, *Dione: A Protocol Verification System Built with Dafny for I/O Automata*, iFM 2019, doi:[10.1109/ITSC48978.2021.9564492](https://doi.org/10.1109/ITSC48978.2021.9564492)


## System Safety Assurance via Approximate Abstractions of Deep Learning Components 

<https://publish.illinois.edu/aproximated-abstract-perception/>


In this project, we proposes a method of certifying autonomous systems that use deep learning for camera-based perception.
For example, we certify a vision-based lane tracking system as a case study of our method.

**TODO** Finish illustrating the following insights

1. Use ground truth information to construct approximations of perception components.
1. The approximation of the component preserves (a relaxation of) existing invariances for the approximated system, given that the invariances are proven w.r.t the ideal system.
1. The approximation can be validated w.r.t the actual component via testing/simulation and obtain statistical guarantees.


### Presentation Videos

<iframe width="50%" src="https://www.youtube.com/embed/ABTUA2OdV0E?start=1778&end=2436" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


### References ordered by relevance:
+ Hsieh et al., *Verifying Controllers with Vision-based Perception using Safe Approximate Abstractions*, EMSOFT 2022, doi:[10.1109/TCAD.2022.3197508](https://doi.org/10.1109/TCAD.2022.3197508)
+ Abraham et al., *Industry-track: Challenges in Rebooting Autonomy with Deep Learned Perception*, EMSOFT 2022, doi:[10.1109/EMSOFT55006.2022.00016](https://doi.org/10.1109/EMSOFT55006.2022.00016)
+ Hsieh et al., *Assuring Safety of Vision-based Swarm Formation Control*, Under submission to ICRA 2023


## Epilogue: Formal Safety Assurance **in addition to** Testing and Simulation

Current best practices for the safety assurance of cyber-physical systems rely on extensive testing and simulating the systems to exhibit safety violations and falsify the design and implementation.
These approaches however suffers from the fact that unsafe events happen in rare scenarios.
Hence, the required amount of simulation and testing to find safety violations can be prohibitively high. (**TODO** Link to driving millions of miles to achieve human performance.)

In comparison, our approaches for the safety assurance stem from the formal safety proof of the approximated abstract system.
We can guarantee the worst case behavior of the approximated system will not violate the system requirement.
However, our approaches or any other formal model-based approaches rely on the following assumption ---
the formal model is faithfully representing or over-approximating all behaviors of the actual cyber-physical system.
Validating this assumption can be as hard as solving the following open problems:
+ Resolve the Sim2Real gap
+ Formalize Operational Design Domain (ODD) in autonomous driving literatures or
  Foreseeable Operating Conditions in overarching properties defined by FAA
(**TODO** explain the connection from the assumption to the open problems.)

In my opinion, it is more practical to view formal proofs as an approach to avoid the simulation and testing of *simple* scenarios.
If we avoid the scenarios where formal proofs already can provide safety guarantees,
we can guide the search of rare scenarios to expose unsafe behaviors faster.
This in turn should speed up the whole verification and testing process.
