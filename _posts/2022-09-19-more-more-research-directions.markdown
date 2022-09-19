---
layout: post
title:  "More and More Research Directions and Ideas"
date:   2022-09-19 16:30:00 -0500
categories: Ideas
published:  true
---

## Synthesize Contracts and Certificates for System with Vision-based Perception

Consider Approximate Abstract Perception as a Likely Contract for Perception

+ Learned contract will include all observed positive input/output pairs from the perception component while remain safe w.r.t safety certificate
  - input is the image labeled with the ground truth.
  - output is perceived value

+ SyGus based approach to infer a contract within a *grammar* L
  - Maximal safe region (symbolically) can be difficult to express due to nonlinearity of vehicle dynamics and piecewise linear control
  - Define maximal region expressible in grammar L
    + Maximal expressible region in grammar L can still be difficult/too complex
    + Regions in grammar L may not be comparable
  - Simple expressions in L that covers all observed i/o pairs


Consider finding certificates for proving safety spec along with contract for perception. We only consider some class of Lyapunov functions for certificates.

+ Our EMSOFT paper uses certificates from the proof of the nominal system assuming no perception errors. Such certificates may not tolerate perception error, and therefore the inferred AAP is too stringent.
+ Consider L1, L2, and L∞ norms and other norm induced norms as the candidate grammar for searching Lyapunov functions.


### References

+ "Precis" by Angello and Madhu
+ ICE learning framework by Madhu


## Runtime Monitoring with Approximate Abstraction

+ Can we use the set-valued approximate abstract perception (AAP) as a monitor to detect and predict failure?
  - First step is to check how likely AAP is violated in a simulation trace with ground truth perception.

+ How to apply on traces without ground truth?

+ Is AAP too conservative? If so, how many consecutive violations of the AAP should happen before the system really enters an unsafe state?


### Related approaches or reusable code base/dataset

+ Momtaz et al., "Predicate Monitoring in Distributed Cyber-Physical Systems", RV 2021
  - Use retiming function to address time skew in distributed CPS
  - The definition of traces and SMT encoding is interesting and reasonable.
  - I have been exchanging emails with Anik, the first author, about improving SMT solving with extra *hints* encoded in SMT from dynamics of each agent.
  - I think the reachability analysis for dynamics and the AAP for vision can make his approach work on very interesting case studies.
+ ROS bags from GRAIC by our group: <https://popgri.github.io/Race/>
  - Talk to Yan


## Drone Formation with Vision-based Relative Pose Estimation

+ Consider the piecewise constant AAP for the perception error as a quantized model for perception values
  - Use existing theory on quantized systems for convergence rate to the ultimate bound.
+ Can we consider removing top X% percentile of the worst observed perception error to find a piecewise constant AAP for X% that is less conservative?
+ Implement a distributed version in AirSim simulation with partial synchrony.

