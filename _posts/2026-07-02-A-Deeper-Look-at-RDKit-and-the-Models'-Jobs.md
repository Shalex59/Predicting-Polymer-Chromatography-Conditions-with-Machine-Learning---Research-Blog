---
layout: post
title: "A Deeper Look at RDKit and the Models' Jobs"
date: 2026-07-2
---
July 2 2026 Entry

**How RDKit works**

RDKit is an open-source chemistry toolkit/library that lets a computer read a molecule's structure and turn it into numbers a machine learning model can use. It takes a molecule written as a SMILES string, a compact text description of the molecule's structure, and from that it can generate a chemical representation. For example, methanol is written as "CO" and water as "O". RDKit needs nothing more than these text strings to produce its chemical output, so no external chemical database is required.

The specific representation this project uses is called a Morgan fingerprint (also known as ECFP, for Extended Connectivity Fingerprint). This fingerprint representation is the industry standard for representing the characteristics of molecules and therefore makes our project more generalizable. Now, specifically, what is a fingerprint? Here, it is a long string of numbers, in this case 2048 of them, where each position stands for a specific structural aspect of the molecule, like "an oxygen bonded to a hydrogen" or "a carbon inside a ring" (these are just examples, not necessarily relevant to the data). If a pattern is present in the molecule, its position is marked; if not, it is left blank.

**What the first model (Layer 1) does**
The first model works by similarity mapping. It keeps a fixed set of reference solvents, the eleven individual solvents that appear across the dataset, and stores their ECFP. Every recipe is then measured against all eleven individual solvents. 

Here is how that measurement works for a single recipe. Take a recipe that is 56% water and 44% acetonitrile. To measure how similar this recipe is to one reference solvent, say methanol, the model first compares water to methanol and computes how much structure they share, then compares acetonitrile to methanol and does the same.

Then it blends those two similarities weighted by how much of each is in the recipe: 0.56 × (water-to-methanol similarity) + 0.44 × (acetonitrile-to-methanol similarity). That single blended number is the recipe's "similarity to methanol" score. Similarity here is defined by a standard cheminformatics tool called Tanimoto similarity, which compares two molecules' fingerprints and counts how many structural building blocks they share, producing a score from 0 (nothing in common) to 1 (identical). For example, water and methanol are not very "similar" so the Tanimoto similarity is low. 2 alchohols, on the other hand, score rather highly.

Repeat this process 11 times for each different solvent pair. Essentially, we will have 11 scores for each of the 86 rows of data, as although there are only 7 distinct sets of solvent pairs, each has a different weight ratio and therefore a different similarity score. 

The comparison is always between individual molecules, each ingredient in the recipe against each individual reference solvent, never between whole pairs. THis improves the model's ability to handle unfamiliar groups of solvents/polymers. A unfamiliar system can be described in terms like "x% similar to solvent 1 and y% similar to solvent 2. 

**Layer 2**
The second layer receives the 11 similarity scores per row of data from the first layer plus the other factors that the first layer didn't process (temperature, base material, ratios, etc). Fundamentally, it is of the same structure as the first test's model: a classifier. During training, it sees many recipes along with whether each one worked, and it gradually learns patterns from the data. Instead of seeing the names of the solvents and materials involved and deciding based on those vague factors, it now has a means of relating those means to each other. 

An example would work well here. Imagine someone who only recognizes his online friends Abe, Bob, and Carson, because those are the only ones he has met in person. Under the old approach, when shown a photo of a fourth friend, Dillan, whom he has never met, he draws a complete blank and can say nothing about him. The similarity bridge works here by describing Dillan's features (eg dark hair, skinny build, looks like Bob, has a hooked nose, etc). Now the person can reason: "Dillan is described a lot like Bob, and I know what Bob is like, so I can make a reasonable judgment about Dillan." He has never seen Dillan, but by describing him in terms of features shared with people he does know, Dillan is no longer a total stranger.

These similarity scores are like descriptions for solvents that the trained model has never seen before. Through the relative resemblance to other known solvents, it can determine (at least vaguely) what the other solvent is like in familiar terms.

Other than these factors, nearly everything is the same as the first test. We will still use classifiers (eg Random Forest and XGBoost), just that there is one added factor.

**Limitations**

The most fundamental one is that structural similarity is a good stand-in for chromatographic behavior. The similarity scores measure how much two molecules share the same structural building blocks, not how they actually behave in a chromatography column. We are essentially betting that molecules which look alike structurally will act alike in practice. But two solvents can be structurally similar and still behave quite differently for reasons a fingerprint doesn't see. In other words, we don't consider the effects of a chemical reaction in this case.

Furthermore, the data itself is still limited to a single polymer at this testing stage. As more polymers are introduced, and potentially new factors along with them, this test will need to be adjusted to account for them.

