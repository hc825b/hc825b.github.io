---
layout: post
title:  "Research Directions & Ideas"
date:   2026-05-27 19:00:00 +0900
last_modified_at: 2026-05-27 19:30:00 +0900
categories: Ideas
published:  false
---

# Theoretical Descriptions

Temporally Permissive Perception Contract (TPPC)

Let $x$ denote the state

* TPPC is a temporal logic formula $\varphi(z, \hat{z})$ over the evolution of the ground-truth $z$ and its estimate $\hat{z}$

### Modeling of Trajectory for Perception Contracts

TODO: We want to relate the trajectories of the ideal and actual systems in the formula of TPPC.

* Let $\xi$ be the combined trajectory of the ideal system and the actual system as the variable evolutions (from variable name and time point to value). The evolution of $z$ can be obtained by $\xi(t)\downarrow_{z}$. Similarly, the evolution of $\hat{z}$ can be obtained by $\xi(t)\downarrow_{\hat{z}}$.
* Sampling trajectories of distinct variables in different frequencies may be addressed by the sampling function for sensing.
  + E.g., a recorded sequences of values of discrete time points is from a sensing function sampling $z$ periodically.
  + What about modeling computation and communication delays?

### Reuse Existing Proof Certificates

TODO: We want to reuse the proof certificates for the nominal system to guide the synthesis of TPPC for relating to the actual system

* Existing invariant $\mathcal{I(x(t))}$ for all time $t$
  + Does it suggest a TPPC for an "inductive time step" to preserve the invariant or do we need to reason with forward invariant set and therefore need white-box dynamic model (ODE)
* Existing monotonically decreasing potential functions $\mathcal{V}(x(t))$
  + What about the ISS functions? Ans. It seems to preserve the same value ever after, so it still preserves monotonicity.
* Other proof certificates?


# Case Study

## System-Level Specification

### Scenarios as Assumption on Environment

### 



## System under Analysis

Autonomous Driving software stack: Autoware

# Observed Problems

* Background: Scenario-based Analysis of ADS
  + Scenarios in Automated Driving Safety Evaluation Framework (ver. 4.0)  
    https://www.jama.or.jp/english/reports/framework.html
    - Responsibility Sensitive Safety analysis: Does SV follow the RSS rules under the scenarios?
  + Software implementation for ADS is mostly black-box or gray-box.
    - Hard-to-formalize perception tasks
    - Hard-to-analyze components (neural networks, optimization)
    - Proprietary software modules from different suppliers

Question: Are the problems below engineering issues or research problems?

* Scenarios in the JAMA framework are over variables on a highly abstract model
  + Classifying trajectories according to such scenarios loses the opportunity to 
  + Refinement to a model at least matching interface variable between modules
  + Decomposition
* Scenario based testing starts from triggering a particular response of the black-box implementation
  + *In retrospective*, we can classify that a particular trajectory belongs to a scenario of interest.
  + How to design NPC behaviors to trigger overtake behaviors instead of deceleration behaviors of the SV?
    - May be considered as a problem that the specification of the scenario is infeasible.
    - Need a concrete example of the following.
> A coverage criteria is defined for some parameter ranges (preventable boundary) for a scenario, but some combinations of parameter values never triggers the scenario of interest (low probability). Similar to an unreachable code or branch in black-box software testing.
* Composition or conjunction of scenario-based RSS rules
  + Composition of rule for lateral distances composed and rule for longitudinal distances
* Refinement from STL formulas defining scenarios to temporal logic formulas on interface variables in actual implementation
  + Quantify away/constant assignments on variables for NPC behaviors? How does this relate to AW Scripts or dynamic scenarios in Scenic?
  + Actual perception stream over bounding boxes


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


# Notes

* Four-variable model, Parnas and Madey 1991, https://doi.org/10.1016/0167-6423(95)96871-J
* Foundational Research Gaps and Future Directions for Digital Twins. Washington, DC: The National Academies Press, 2024. https://doi.org/10.17226/26894.

LLM Agent-Assisted Analysis has become "the thing".


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
