---
layout: page
title: Research Projects
permalink: /projects/
---

My broad research direction is the *formal assurance* of the cyber-physical system (CPS) containing complex components that are incompletely specified or currently intractable for existing formal verification techniques.

I have been investigating several systems containing incomplete vehicle dynamics, vision-based perception pipelines, communication protocols, or combinations of all.
The main intuition behind all case studies is to achieve the *separation of concerns* via abstractions of components.
We repeatedly apply the abstraction then refinement principle to decompose the verification problem of CPS into component-level verification sub-problems.

With this principle in mind,
the crucial step is to select a proper abstraction for each component that is suitable for domain specific formal analyses.


## System Safety Assurance via Perception Contracts of Deep Learning Components 

In this line of research, we aim to certify autonomous systems that use machine learning (ML) components for perception.
Especially, we want to address vision-based perception that uses deep neural networks (DNN) to process camera images and extract information for decision and control.

The research started in late 2020, amid the first year of COVID-19 pandemic,
when we faced the uncertainty in perception components (and in life).
We first studied the [CropFollow] perception component for the [TerraSentia] robot.
TerraSentia is a small ground vehicle for agricultural applications developed by Prof. Girish Chowdhary's team in UIUC,
and CropFollow is the component for visual navigation in the crop field.
I was involved in [the agricultural robot project][agbot] funded by USDA/NIFA and started to discuss with students from Prof. Chowdhary and Prof. Campbell's groups.
I clearly remember that I sent a message *around Christmas* in 2020 and got responses *before New Year* from [Arun], Prof. Chowdhary's PhD student at that time.
Then, I got the simulator for CropFollow and TerraSentia and started some preliminary experiments to celebrate the coming of 2021.

[TerraSentia]: https://www.earthsense.co/home
[agbot]: https://archive.cps-vo.org/node/76005
[Arun]: https://scholar.google.com/citations?user=peIOOn8AAAAJ
[CropFollow]: https://arxiv.org/abs/2107.02792


### Challenges in Certifying Systems with DNN Components

In my opinion, two major challenges in the formal analysis on DNN and systems using DNN for perception are as below:

+ **High dimensional input space**: For example, the input image size for VGG16, a well-known DNN architecture, is 224x224 pixels with RGB colors.
  That is 224x224x3=150528 Bytes, which includes about 10<sup>45313</sup> different images.
+ **Hard-to-formalize perceptual tasks**: Consider lane detection for autonomous driving, which detects lane markers for the lane keeping assist system.
It is unclear how to formally define images that "contain a lane" in terms of pixel values.

These are two of the five main challenges listed in the article ["Toward Verified Artificial Intelligence"](https://doi.org/10.1145/3503914).
As pointed out in the article, the insight to address the above challenges is to actually consider the whole system and the system-level specification instead of the individual DNN.
We again consider the lane keeping assist system with a lane detection component as an example.
For lane keeping, we not only need the information whether there are image pixels showing lane markers,
but more importantly we need the estimated position of the ego vehicle and the detected lane for steering the vehicle.
That is, the complete perception task is a *state-estimation* task,
and the detection or classification tasks are only intermediate stages.
This allows us to formally define perception tasks with respect to ground-truth states of the vehicle.

**TODO**: add images to illustrate the insight that classification is usually an intermediate stage in the entire state estimation task.

In addition to lane keeping, we found that this insight applies to many other perception tasks for self-driving cars such as pedestrian avoidance, automatic parking, etc., as well as for unmanned aerial vehicles including automatic landing and taxiing, visual odometry, and drone racing.


### Approximated Abstractions of Perceptions

**TODO** Our first attempt is to 

### Why Perception Contracts

With the great help from Angello and Madhu, we formalized the notion of *perception contracts* as the component-level specification for perception components.
Perception contracts capture errors in perception that preserve system-level properties when systems act upon them.
We develop a theory of perception contracts and design learning algorithms for synthesizing them.

With perception contracts, we can decompose the certification of the systems into two problems:

1. Certify that the deep learning components for perception conforms to its perception contract, and
1. Assuming that its perception contract is conformed, certify the system.


The second task can be performed using traditional techniques in formal verification of cyber-physical systems.

**TODO** Finish illustrating the following insights

1. Use ground truth information to construct approximations of perception components.
1. The approximation of the component preserves (a relaxation of) the existing invariance for the approximated system, given that the invariance is proven w.r.t the ideal system.
1. The approximation can be validated w.r.t the actual component via testing/simulation and obtain statistical guarantees.


### Presentation Videos

<iframe width="48%" src="https://www.youtube.com/embed/ABTUA2OdV0E?start=1778&end=2436" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<iframe width="48%" src="https://www.youtube.com/embed/VT7nMsBT4f4?start=23341&end=24390" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### Links
<https://publish.illinois.edu/aproximated-abstract-perception/>

### References Ordered by Relevance
+ Astorga et al., *Perception Contracts for Safety of ML-Enabled Systems*, OOPSLA 2023, doi:[10.1145/3622875](https://doi.org/10.1145/3622875)
+ Hsieh et al., *Verifying Controllers with Vision-based Perception using Safe Approximate Abstractions*, EMSOFT 2022, doi:[10.1109/TCAD.2022.3197508](https://doi.org/10.1109/TCAD.2022.3197508)
+ Abraham et al., *Industry-track: Challenges in Rebooting Autonomy with Deep Learned Perception*, EMSOFT 2022, doi:[10.1109/EMSOFT55006.2022.00016](https://doi.org/10.1109/EMSOFT55006.2022.00016)
+ Hsieh et al., *Assuring Safety of Vision-based Swarm Formation Control*, arXiv 2022, doi:[10.48550/arXiv.2210.00982](https://doi.org/10.48550/arXiv.2210.00982)
+ Arun et al., *Learned Visual Navigation for Under-Canopy Agricultural Robots*, RSS 2021, doi:[10.15607/RSS.2021.XVII.019](https://doi.org/10.15607/RSS.2021.XVII.019)


## Programming Abstractions for Distributed Robotics

Project Website: <https://cyphyhouse.github.io>  

I have been in the CyPhyHouse team since Summer 2018. CyPhyHouse aims to provide programming, debugging, and deployment for *distributed robotic applications (DRAs)*. Users can develope distributed applications using the high-level, hardware-agnostic, event driven Koord programming language included with CyPhyHouse, without requiring deep expertise in controller design or distributed network protocols.

One key abstraction provided by the Koord language is *synchronous logically*.
That is, Koord program language aims to provide a synchronous round-based semantics though physically running on a distributed asynchronous multi-robot system.
Under this language semantic, *Koord users*, such as control theorists, can design the high level coordination logic with much simpler synchronous executions in mind.
*Koord compiler developers* focus on design and implement the middleware that achieves the synchronous semantics with asynchronous communication, for example, [*Physically-Asynchronous Logically-Synchronous (PALS)* System][PALS].
*Hardware platform developers* then concentrate on supporting the robot control commands delivered through the communication primitives for each kind of vehicles.

[PALS]: http://hdl.handle.net/2142/11897


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

### References Ordered by Relevance
+ Ghosh et al., *Koord: A Language for Programming and Verifying Distributed Robotics Application*, OOPSLA 2020, doi:[10.1145/3428300](https://doi.org/10.1145/3428300)
+ Ghosh et al., *CyPhyHouse: A Programming, Simulation, and Deployment Toolchain for Heterogeneous Distributed Coordination*, ICRA 2020, doi:[10.1109/ICRA40945.2020.9196513](https://doi.org/10.1109/ICRA40945.2020.9196513)
+ Hsieh et al., *SkyTrakx: A Toolkit for Simulation and Verification of Unmanned Air-Traffic Management Systems*, ITSC 2021, doi:[10.1109/ITSC48978.2021.9564492](https://doi.org/10.1109/ITSC48978.2021.9564492)
+ Hsieh et al., *Programming Abstractions for Simulation and Testing on Smart Manufacturing Systems*, CASE 2022, doi:[10.1109/CASE49997.2022.9926564](https://doi.org/10.1109/CASE49997.2022.9926564)
+ Chiao Hsieh and Sayan Mitra, *Dione: A Protocol Verification System Built with Dafny for I/O Automata*, iFM 2019, doi:[10.1109/ITSC48978.2021.9564492](https://doi.org/10.1109/ITSC48978.2021.9564492)



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
+ Formalize Operational Design Domain (ODD) (in autonomous driving literatures) or
  Foreseeable Operating Conditions (in overarching properties defined by FAA)

(**TODO** explain the connection from the assumption to the open problems.)

In my opinion, it is more practical to view formal proofs as an approach to reduce the amount of simulation and testing of *simple* scenarios.
This leads to three

**Guided Search in Testing.**
If we avoid the scenarios where formal proofs already can provide safety guarantees,
we can guide the search of rare scenarios to expose unsafe behaviors faster.
This in turn should speed up the whole verification and testing process.

**Runtime Monitoring.**
(**TODO** Describe how we may construct executable monitors over only observed variables.)
We can integrate this monitor into the system to ensure safety.
For instance, it can serve as the logic to switch between high performance controllers and high-assurance controllers in the [simplex architecture](https://doi.org/10.1109/MS.2001.936213) coined by Prof. Lui Sha.
