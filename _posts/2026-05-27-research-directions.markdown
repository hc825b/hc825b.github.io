---
layout: post
title:  "Research Directions & Ideas"
date:   2026-05-27 19:00:00 +0900
last_modified_at: 2026-07-16 10:30:00 +0900
categories: Ideas
published:  True
---

# Module Contract Synthesis Problem for Automated Driving Systems

How to derive module-level contracts for perception, decision, or control modules in ADS from system-level specifications?
* Formalization of assumptions and guarantees conceptually are all **sets of trajectories**
  + E.g., assumptions for scenario-based analysis is also a filter to look for trajectories of interest in a dataset, and guarantees as a predicate is applied to decide if the trajectory satisfies or violates the specification.
* Two intuitive choices of representing a set of trajectories are (signal) temporal logics and (hybrid) automata
  + The filter and the predicate can be implemented either as evaluating the truth value of a logic formula or accepting/rejecting by an automata

| Techniques          | Temporal Logic | Automata                       |
| ------------------- | -------------- | ------------------------------ |
| Contract Algebra    | AND, OR, NOT   | Compose, Nondet., Complement   |
| Data-driven Synth.  | SyGus          | Automata Learning              |
| Spec-Guided Approx. | Interpolants   | Property Directed Reachability |

* Decomposition of system-level specification remains unclear


## Sketch for the Theoretical Framework

Given the evolution of the ground-truth $z$ and its estimate $\hat{z}$, Temporally Permissive Perception Contract (TPPC) can be formalized as:

* a temporal logic formula $\varphi(z, \hat{z})$ relating the ground-truth and its estimate
* a set membership query $\hat{z} \in \Phi(z)$ where $\Phi(z)$ captures all trajectories that are *close enough* to the given ground truth $z$


### Modeling of Trajectory for Perception Contracts

**Idea:** We want to relate the trajectories of the nominal system and the actual system in the formula of TPPC.

* May be modelled with an observation function to apply on trajectories of $z$ and $\hat{z}$ to only talk about input/output of perception module
* Sampling trajectories of distinct variables in different frequencies may be addressed by the sampling function for sensing.
  + E.g., a recorded sequences of values of discrete time points is from a sensing function sampling $z$ periodically.
  + What about modeling computation and communication delays?


### Reuse Existing Proof Certificates

**Idea:** We want to reuse the proof certificates for the nominal system to guide the synthesis of TPPC for relating to the actual system

* Existing invariant $\mathcal{I(z(t))}$ for all time $t$
  + Does it suggest a TPPC for an "inductive time step" to preserve the invariant? Or do we need to reason with forward invariant set and therefore need white-box dynamic model (ODEs)?
* Existing monotonically decreasing potential functions $\mathcal{V}(z(t))$
  + What about the ISS functions? Ans. It seems to preserve the same sublevel set ever after, so it still preserves monotonicity.
* Other proof certificates?


# Case Study

Our case study focused on the scenario-based safety evaluation following the recently drafted international standard, ISO 34502, which is based on the framework proposed by JAMA.

+ Scenarios in Automated Driving Safety Evaluation Framework (ver. 4.0)  
    https://www.jama.or.jp/english/reports/framework.html
    - Responsibility Sensitive Safety analysis: Does SV follow the RSS rules under the scenarios?
+ Software implementation for ADS is mostly black-box or gray-box.
  - Hard-to-formalize perception tasks
  - Hard-to-analyze components (neural networks, optimization)
  - Proprietary software modules from different suppliers

## Example System under Analysis

* Autonomous Driving software stack: Autoware
* Simulation Environment: AWSim

## Specifications

**Idea:** We would like to apply assume-guarantee style reasoning.

Assumptions from scenarios:
+ Desired SV behaviors for the select scenario
  - Focus on the responder role
+ **Preventable POV Behaviors**
  - SV cannot prevent collision to all possible POV behaviors.
  - JAMA defines preventable boundary by a driver model. It is unclear and maybe difficult to directly define the preventable behaviors.
+ Interaction between SV and POV

System-Level Guarantees:
+ Collision Avoidance

Module-level Assumptions and Guarantees
+ Perception error model of perception output
  - Infer tolerable error shapes instead of starting an assumed error bound with a symmetric shape
+ Safe separation between predicted POV path and planned SV path
+ Error model of tracking error by the control over the vehicle dynamic
  - Tracking error here is to describe the difference between the planned path and actual SV trajectory
  - Tracking error in this context likely requires a more complex definition because the planned SV path also evolves wrt time.


## Observed Problems

Question: Are the problems solvable with existing approaches or novel research problems?

* Scenarios in the JAMA framework are over variables on a highly abstract model
  + Classifying trajectories according to only JAMA scenarios does not utilize the internal information available in ADS. 
  + Need a refined model at least matching interface variable between modules
    - Refinement relation with the JAMA scenarios
    - Decomposition with respect to the system architecture
    - This should enable a refinement-based proof strategy and decomposed proof obligations for modules.
* Scenario based testing starts from triggering a particular response of the black-box implementation
  + In *post-analysis*, we can classify that a particular trajectory belongs to a scenario of interest. However, it can be difficult to trigger the desired response because of the black-box implementation.
  + How to design NPC behaviors to trigger, e.g., overtake behaviors instead of deceleration behaviors of the SV?
    - May be considered as a problem that the specification of the scenario is infeasible.
    - Need a concrete example of the following.
> A coverage criteria is defined for some parameter ranges (preventable boundary) for a scenario, but some combinations of parameter values never triggers the scenario of interest (low probability). Similar to an unreachable code or branch in black-box software testing.
* Composition or conjunction of scenario-based RSS rules
  + Composition of rule for lateral distances composed and rule for longitudinal distances
* Refinement from STL formulas defining scenarios to temporal logic formulas on interface variables in actual implementation
  + Quantify away/constant assignments on variables for NPC behaviors? How does this relate to AW Scripts or dynamic scenarios in Scenic?
  + Actual perception stream over bounding boxes

* Sampled parameter values by Scenic may be difficult to realize in Autoware and AWSim.
* Simulation with Autoware takes long execution time. According to Duong-san, each iteration in guided falsification will be time consuming.


# Checkpoints

* Existing offline runtime monitoring engines to specify queries of temporal properties for retrieving trajectories of interest
  + Spatio Temporal Regular Expression
    - Pattern Matching for Perception Streams, RV 2023
    - STREM https://cps-atlas.github.io/strem/
  + STL formalization of scenarios
    - "Temporal Logic Formalisation of ISO 34502 Critical Scenarios: Modular Construction with the RSS Safety Distance", SAC 2024, https://doi.org/10.1145/3605098.3636014
* Installation of AWSim and Autoware for data collection
  + Technical issues in reproducibility?
    - Time delay due to computation time, congestion, or message buffer
    - Precision of floating point or other number formats
  + Understand issues in ROS2 communication
  + Re-implementation with Scenic instead of AW Script?

* Deliverable: A Dockerfile to create a Docker image for consistent development environments
  + Autoware
  + AWSim in the official repository (AWSim Lab is discontinued.)
  + AWSim script or an equivalent (Scenic?)


# Autoware+AWSIM in Docker

## Host Machine Configurations

The following section discusses necessary configurations on the host machine for running Autoware with AWSIM inside a docker container.

### Increase the maximum receive buffer size for network packets on the host machine
Error message:
```
... failed to increase socket receive buffer size to at least xxx bytes, current is yyy bytes
...
... rmw_create_node: failed to create domain, error
```

Reference: [Tune system-wide network settings](https://autowarefoundation.github.io/autoware-documentation/main/installation/additional-settings-for-developers/network-configuration/dds-settings/#tune-system-wide-network-settings)
```shell
sudo sysctl -w net.core.rmem_max=2147483647  # 2 GiB, default is 208 KiB
```
To make it permanent,
```shell
sudo nano /etc/sysctl.d/10-cyclone-max.conf
```

Paste the following into the file:

```ini
# Increase the maximum receive buffer size for network packets
net.core.rmem_max=2147483647  # 2 GiB, default is 208 KiB
```

### Support Vulkan in docker container using NVIDIA GPU for hardware acceleration

Reference: https://qiita.com/lzpel/items/20e9df87b744177b665b


## Configure the Container

Configurations can already be specified inside the docker image.
