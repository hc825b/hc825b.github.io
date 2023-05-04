---
layout: post
title:  "Available Tools and Case Studies"
date:   2023-05-04 12:30:00 -0600
last_modified_at: 2023-05-04 12:30:00 -0600
categories: Ideas
published:  true
---


# Program Analysis Tools

The goal is to compute symbolic post-image for (a snippet of) a controller program in ROS, so the idea is to reuse existing program analysis tools for C++ or Python.


## C/C++

+ Software Analysis Workbench by Galois Inc. https://saw.galois.com/
+ SPARTA by Facebook https://github.com/facebook/SPARTA
+ IKOS by NASA https://github.com/NASA-SW-VnV/ikos
+ CBMC https://github.com/diffblue/cbmc
+ ESBMC https://github.com/esbmc/esbmc


## Python

+ CrossHair https://github.com/pschanely/CrossHair


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

