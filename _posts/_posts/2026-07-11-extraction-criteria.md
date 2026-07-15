---
layout: post
title: "Extraction Criteria and Approach"
date: 2026-07-11
---

July 11, 2026 Entry

Been data mining this entire since the last post. This post is an update on the process of mining, what data counts, and a little explanation of the extractor I have been using. After all, this data is much more than just data put into a spreadsheet. A seperate post with actual results will be uploaded into the blog once I am finished.

**What counts as a condition, again, and an example of a complication**
 
The core definition hasn't changed. However, sometimes, caveats emerge, and this one is important enough that I want to specifically bring it up. To reiterate, a critical or non-critical condition is a property of a (polymer backbone, recipe) pair, not of a sample or an architecture. During the previous data mining session, this condition was not specified in the prompts file to guide the LLM, thus drawing erronous results. 

However, it is not always easy to teach LLMs to tell that difference. Most of the time, architecture variants (star vs. linear, different end groups, different arm counts) of the same polymer count as one row. But every so often a paper does something structurally different. The polyisoprene paper I worked through this week (Hiller et al., 2011) separates 1,4-polyisoprene from 3,4-polyisoprene, one a critical condition while the other not. How could that be? Upon initial analysis, it may seem that the fundamental backbone (polyisoprene)  is the same across both polymers, which leads to the conclusion that the results are contradictory. However, in actuality, that is not the case. Both of the these molecules are polyisoprenes, but their backbones are fundamentally different. 

Now, for the goal of the paper. This would greatly clarify the point I am making here. Polyisoprene, a widely used polymer in the maufacturing of synthetic rubber, can polymerize in 3 different ways: 

1,4-PI: the double bond stays in the main chain
3,4-PI: the double bond ends up on a pendant isopropenyl side group
1,2-PI: similarly, a pendant vinyl-type side group

Now these three types are notoriously hard to tell apart. Even normally used chemical detectors can't tell them apart. By finding the critical conditions of one (in this case, 1-4 PI) and subjecting a blend of these three polymers to that critical condition. Since 1,4-PI sits at its critical point under those conditions, it becomes what chromatography calls "chromatographically invisible" as its retention stops depending on molecular weight entirely, so it elutes at the same rate regardless of how big or small any individual chain is. Whatever isn't at its own critical point, meanwhile, still separates normally by size. Run a blend of all three isoprene microstructures through this one recipe, and there are exactly two behaviors: 1,4-PI lies at one retention volume no matter its molecular weight, while 3,4-PI (and whatever 1,2-PI is riding along with it) spreads out across a range of retention volumes ordered by size. 

 An LLM extracting this paper without the distinction spelled out would see "polyisoprene" twice along with identical conditions for 3,4 PI and 1,4 PI and auotmatically think that these were both experimental conditions and collapse them into one polyisoprene row critical condition. Luckily, me and my mentor spotted this mistake as we performed the 3 step extraction (explained below) and corrected the extractor file before anything happened.

**The criteria for data extraction and what actually gets logged**
 
 
*Pass 1* is pure extraction — read the whole thing and pull out every (backbone, recipe) pair reported, from tables, captions, and body text, not just the headline sentence.
 
*Pass 2* is where the LLM is trained to try and think like a reviewer instead of a transcriber. The question for each candidate: does the paper's own evidence actually demonstrate the claim, or does it just *assert* it? A composition described as "the critical condition" with no multi-standard test behind it doesn't clear the bar. Neither does a condition that's purely cited from someone else's earlier paper with nothing checkable in the current one — unless the current paper shows its own fresh chromatogram at that recipe, in which case it's fine to include, just flagged as citation-reliant. I've also started explicitly checking for internal contradictions within a single paper as those pop up, albeit infrequently. In this case I would flag it for later review rather than getting rid of the candidate altogether. 
 
*Pass 3* is a straight fabrication check. LLMs are commonly known for "hallucinations" in which they make up data that doesn't exist. This last part actually matters, as we are working with data that contributes to actual research. Of course, such data, even if flawlessly extracted, must be reviewed once again (I will talk a bit more about this later). Factors like base material (silica vs. polymer), which solvent promotes adsorption vs. desorption and column mode are tempting to fill these in from general knowledge of a well-known column brand, but if the paper itself doesn't say it, it stays blank.

Of course, the code is still under review. I don't want to jump to conclusion right now and completely bar the LLM from any analysis of its own (that comes later). I welcome any comments on my blog, questions, or concerns.
