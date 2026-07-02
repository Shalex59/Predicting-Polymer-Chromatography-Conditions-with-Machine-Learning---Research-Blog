---
layout: post
title: "Mentor Feedback, Observations, and What Comes Next"
date: 2026-06-27
---
June 27 2026 Entry

As confirmed by the two model tests conducted on the data beforehand, ML models could not reliably recognize recipes from a solvent group they had never seen during training. Even with RDKit incorporated to provide chemical information about each solvent, the gap couldn't be bridged. That finding opened up a conversation with my mentor, Professor Wang, and led us to a new phase of this research.

**Professor Wang's RDKit suggestion**

Professor Wang suggested going deeper with RDKit than what the current test attempted. Rather than using four broad summary descriptors, the idea is to use full chemical fingerprints for each solvent and polymer. The fingerprint, represented as a long string of numbers describing various properties of the polymer/solvent, can provide a much more whole picture of the molecule's role in a critical condition. Essentially, incorporating RDKit's molecular information would be key to this next step. 

**The layered algorithm idea**

One idea I've been developing, which Professor Wang also encouraged, is to layer two separate models rather than asking one model to do everything at once. The first layer would analyze the RDKit fingerprints, learning what chemical signatures are associated with critical conditions. The second layer would take the output of the first model and combine it with factors like temperature, stationary phase, base material, and solvent ratio to make the final prediction. While this idea seems complex in theory and hard to implement in reality, it carries several benefits compared to the initial test. While the single-model approach is being asked to answer two questions simultaneously, the second test only requires one question to be answered per model: Question 1: what is a detailed description of the molecules involved in the data (Model 1), Question 2: Taking into account the description of the molecules involved and other factors, will a given system reach critical point? The first model will also feed more detailed information from RDKit compared to the that of the first test. 

Of course, the latter question has been simplified for this stage. Our original aim was to have the model give us suggestions as to what factors could be changed to bring a system not at its critical point to critical point, but this is a far more ambitious goal and much further down the road.

What is most important, however, is finding a way to incorporate RDKit effectively like what is described above. That will be the subject of my research for the next few days.


**Rethinking the data split**

A second possible change involves changing how the test data is divided. Our first model test held out an entire solvent group at a time, which meant the model never saw any examples from that group during training. A more informative next test would include some entries from every solvent group in the training data and hold out a random subset across all groups instead. That gives the model at least some exposure to every system, which is a much fairer test of whether it can learn the underlying pattern. In the next test, I plan to incorporate both of these ideas to test whether the gap from the first test could be bridged.
