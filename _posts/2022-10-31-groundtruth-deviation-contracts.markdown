---
layout: post
title:  "Ground-truth Deviation Contracts"
date:   2022-10-31 09:30:00 -0500
last_modified_at: 2022-10-31 11:30:00 -0500
categories: Notes
published:  true
---

Learning how Madhu presents the idea of GTDC

Talk about formal specification of perception tasks
+ Local robustness - input domain is image domain
+ Global robustness - input domain is image domain
+ Specification w.r.t an image generator representing a *reasonable* set of images labelled with ground-truth. (Scenic in VerifAI)
  - Developing realistic image generator is the *verification approach*, not part of the specification?

Ground-truth deviation contracts is about the end-to-end analysis.
> "I don't care what I see as long as my system is safe." - Madhu

> "Even if the system acts in response to gt estimates, it preserves the invariant." - Madhu

+ GTDC is an alternative specification for ensuring safety. If the perception satisfies GTDC, the system is safe.

+ Assuming that system with perfect perception and the model of environment is safe with given safety proof.
  - The model of environment can *simulate* the actual environment (simulation relation).
+ Introduce the system with actual environment and perception pipeline.
+ Mining GTDC that is likely to hold for ensuring safety.
  - We cannot ensure GTDC will always hold because of the model of the environment.

+ Visualize the wrong estimates that will lead to unsafe using the lane and lane boundary.
+ Explain the system evolves gt carefully evens through the control feedback is computed using gte.
+ GTDC links the two systems.

+ Mining GTDC can be modelled as a learning probelm with positive (gt, gte) pairs from labelled images and negative examples from the negation of invariants.
