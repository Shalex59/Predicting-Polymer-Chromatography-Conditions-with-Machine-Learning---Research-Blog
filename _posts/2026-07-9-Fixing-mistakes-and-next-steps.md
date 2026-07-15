---
layout: post
title: "Fixing Mistakes and Next Steps"
date: 2026-07-9
---
July 9 2026 Entry
 
The last post was all about pulling negative results out of the literature. This one is about two things: extending that to the positive side, and fixing a subtlety in what I was actually extracting that I didn't realize appreciate at first. First, the not so subtle subtlety (dont laugh at my joke).
 
 
**The subtlety I had to pin down**
 
Here's the part that took some sorting out. Early on, I was treating a critical condition as if it were a property of an individual sample or run. It isn't, in reality, that is an experimental condition. A sample of polymer can be subject to many experimental condition. A critical condition is a property of a *(polymer backbone, recipe)* pair — the repeat-unit chemistry together with a specific solvent system, ratio, temperature, and column. I am not necessarily saying that any polymer can only have one critical point, even as you change one variable (eg temp, solvent ratio, etc). Simply a shift of ratio can yield a new critical point, but we don't know by how much or if that is even applicable to that polymer. This also is the final goal of the ML algorithm, as stated multiple times in the previous posts.
 
Now for why that matters and putting this in context of teh papers I am looking over. A single paper will often establish one critical composition using a reference polymer, then hold that exact mobile phase fixed while testing a dozen variants of the same backbone — different architectures, end groups, and arm counts (paper is Radke 2005). Those aren't a dozen critical conditions. They're one condition, and early extraction runs didn't make that distinction and split one real critical point into many rows. 
 
Once I understood that, the fix was to treat identity as the backbone plus the recipe.
 
**Learning the tools to go with it**
 
Alongside the data work, I've been learning how to use Visual Studio Code. So far I've been using AI to do the actual mining, and coding, but I want to understand the code that's involved and ideally get to the point where I can run it myself, read what it's doing, and fix any mistakes or misconceptions that arise.

The bigger reason is that I don't want to rely on the AI completely. Handing a paper to a model and trusting whatever comes back is fine for a first pass, but if I can run the extraction myself in an environment I understand, I can check the output against the code rather than taking it
 
**Where this leaves things**
 As of now, after patching the misconception, I intend to mine the papers for critical conditions as a point of comparison. My mentor and her students have both a manually curated set of records and a parallel extraction effort running on a different model, so once I have my own critical conditions pulled, all three can be lined up against each other. The goal of my data mining is to obtain results that can agree with that of the other two data sets. Furthermore, as a machine learning model cannot run on only "true" results, I will also use this algorithm to pull any non-critical results mentioned in the papers, if at all present. 
 
As always, I'm still very much learning here, and I'd welcome any correction on the framing or the conventions
