---
layout: post
title:  "Available Tools and Case Studies"
date:   2023-05-04 12:30:00 -0600
last_modified_at: 2023-05-04 13:30:00 -0600
categories: Ideas
published:  true
---


# Program Analysis Tools

The goal is to compute symbolic post-image for controller programs in ROS for synthesizing assumptions on the interfacing variables/ROS messages.

The idea is to reuse existing program analysis tools for C++ or Python.
At the best case, we only need to analyze the callback functions for ROS subscribers and the loop for periodically publishing messages using ROS publishers.


## C/C++

+ Software Analysis Workbench by Galois Inc. https://saw.galois.com/
+ SPARTA by Facebook https://github.com/facebook/SPARTA
+ IKOS by NASA https://github.com/NASA-SW-VnV/ikos
+ CBMC https://github.com/diffblue/cbmc
+ ESBMC https://github.com/esbmc/esbmc


## Python

+ CrossHair https://github.com/pschanely/CrossHair


## Some Features to Look for

+ How to instrument or annotate to only analyze part of a ROS package.
  The fewer instrumentation needed the better.
+ How to add pre/post conditions or approximations for complicate/uninterpreted functions such as trigonometry functions or ellipsoids
+ Floating point numbers or real numbers
+ Support matrix and linear algebra?


# Simulated Autonomous Systems for Case Studies

## Gazebo

- Lane keeping (vision, dynamics)
https://github.com/hc825b/POLARIS_GEM_e2
- Crop row following (vision)
https://bitbucket.org/hc825b/terrasentia-gazebo
- Vision-based fixed-wing aircraft landing (vision, dynamics)
https://github.com/cyphyhouse/Aircraft_Landing_Verification
- UTM (dynamics, coordination)
https://github.com/cyphyhouse/CyPhyHouseExperiments/tree/master/experiments_utm
- ARIAC smart manufacturing (dynamics, coordination)
  https://github.com/cyphyhouse/ARIAC


## AirSim

See https://publish.illinois.edu/aproximated-abstract-perception/

- Drone racing (vision, dynamics)
- Vision-based drone formation (vision, dynamics, coordination)

