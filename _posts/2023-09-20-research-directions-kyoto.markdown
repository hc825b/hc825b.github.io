---
layout: post
title:  "Research Directions and Ideas: Kyoto Draft"
date:   2023-09-20 19:00:00 +0900
last_modified_at: 2023-09-20 19:30:00 +0900
categories: Ideas
published:  true
---

+ Synthesize invariant and perception contract with Property-Directed Reachability
  - Kohei Suenaga and Takuya Ishizawa, "Generalized Property-Directed Reachability for Hybrid Systems", VMCAI 2020, doi: [10.1007/978-3-030-39322-9_14](https://doi.org/10.1007/978-3-030-39322-9_14)


+ Synthesize the model of the environment using automata learning, e.g., L* algorithms.
  - Amit Gurung, Masaki Waga, Kohei Suenaga, "Learning nonlinear hybrid automata from input-output time-series data", arXiv, 2023, doi: [10.48550/arXiv.2301.03915](
https://doi.org/10.48550/arXiv.2301.03915)
  - Need a model of the environment that can be refined to match real
    or simulated environments. An interesting topic is to allow
    failure reproduction. If the hybrid automaton exhibits a failing execution, how do we instantiate a witness execution in the ROS program with the simulator.

+ Synthesize perception contracts in different *templates*
  - Receding horizon with temporal evolution
  - Quantization as discrete abstractions for quantized control
  - Symbolic abstractions for nonlinear control systems
    * K. Hashimoto, A. Saoud, M. Kishida, T. Ushio, D. V. Dimarogonas, “Learning-based symbolic abstractions for nonlinear control systems,” Automatica pp.110646, 2022
