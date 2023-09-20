---
layout: post
title:  "Research Directions and Ideas 3"
date:   2023-05-01 15:30:00 -0600
last_modified_at: 2023-05-04 14:00:00 -0600
categories: Ideas
published:  true
---

+ Hybrid automata as system models and refinement to ROS programs an the simulation engine

  - The reaction module is the abstraction of ROS programs.
    Consider Khan Process Network~(KPN) as the intermediate model for 
    abstracting ROS nodes and publish/subscribe communication paradigm
    because KPN can be analyzed independently from communication delay
    and interleaving of ROS nodes.
  - Need a model of the environment that can be refined to match real
    or simulated environments. An interesting topic is to allow
    failure reproduction. If the hybrid automaton exhibits a failing execution, how do we instantiate a witness execution in the ROS program with the simulator.

+ Synthesize perception contracts in different *templates*
  - Receding horizon with temporal evolution

+ Synthesize invariant and perception contract with Property-Directed Reachability
  - Kohei Suenaga and Takuya Ishizawa, "Generalized Property-Directed Reachability for Hybrid Systems", VMCAI 2020, doi: [10.1007/978-3-030-39322-9_14](https://doi.org/10.1007/978-3-030-39322-9_14)


+ Set-induced Lyapunov function that is piecewise linear. For discrete dynamical systems first, then use Euler approximation for continuous systems.
  - Franco Blanchini, "Ultimate boundedness control for uncertain discrete-time systems via set-induced Lyapunov functions", IEEE Transactions on Automatic Control, 1994, doi: [10.1109/9.272351](https://doi.org/10.1109/9.272351).
  - Franco Blanchini, "Nonquadratic Lyapunov functions for robust control", Automatica, 1995, doi: [10.1016/0005-1098(94)00133-4](https://doi.org/10.1016/0005-1098(94)00133-4).
  - Hai Lin and Panos J. Antsaklis, "Uniformly Ultimate Boundedness Control for Uncertain Switched Linear Systems", ISIS Technical Report, ISIS-2003-004, University of Notre Dame (2003).


+ Synthesize the model of the environment using automata learning, e.g., L* algorithms.
  - Amit Gurung, Masaki Waga, Kohei Suenaga, "Learning nonlinear hybrid automata from input-output time-series data", arXiv, 2023, doi: [10.48550/arXiv.2301.03915](
https://doi.org/10.48550/arXiv.2301.03915)
  - Iman Saberi, Fathiyeh Faghih, and Farzad Sobhi Bavil, "A Passive Online Technique for Learning Hybrid Automata from Input/Output Traces",  ACM Trans. Embed. Comput. Syst. 22, 1, Article 9, January 2023, doi: [10.1145/3556543](https://doi.org/10.1145/3556543)
