---
layout: post
title: "Mining the Papers for Failure"
date: 2026-07-06
---
July 6 2026 Entry
As stated by the previous post, if a model is ever to succeed, it needs negative results (in this case, defined as data points of experiments that did not reach critical point). A model that's only seen a handful of solvent groups can't tell you anything useful about a new one. So instead of running another model test, I spent this stretch going back into the literature and extracting data through the means of commercial LLMs. 

That turns out to be less simple than it sounds because "didn't reach it" isn't one thing. A polymer can miss the critical point by being excluded from the pores entirely (SEC mode), by adsorbing too strongly onto the column (LAC mode), or by just not dissolving in the mobile phase at all. Those are three different failure modes and tracking which is which matters.

**How I'm pulling the data**
The raw material is published papers, read closely. The useful stuff is almost never in the abstract but in the figure captions, method sections, and tables. For each condition a paper reports I'm logging the polymer, its class and end groups, the solvents and their ratio, temperature, column type and base material, phase type, and whether it reached the critical point. Other points of interest include which solvents contributed to adsorption and desorption ( I will define later), and pH (only applicable to a small number of data rows), paper name, and date. Date is relevant as the underlying variation in column surface chemistry can be more significant for older studies, potentially skewing the data.

Here are a few of the conventions I am following:  If a paper gives a range — say a critical point "between 80 and 90 wt% methanol" and doesn't specify a concrete percentage, then it doesn't get counted in the model, at least for now. Technically, while any value in that range could be considered a non-critical condition, the goal of this data mining process is to extract stated values, not making assumptions. That fact remains the same for adsorption and desorption data. If not stated clearly, it isn't included. 

These conditions were provided to the commercial LLM in context (in this case, Claude AI). The specifications are as follows: Opus 4.8 on high effort, provided with sufficient context. I had the model go through each paper twice to ensure no data points were missed. Every batch of extracted rows was shown to me for review before anything touched the file. The model would display the proposed rows, I'd check them against the conventions, and only confirmed rows got appended. Nothing went in automatically.

Furthermore, after all data from the papers went in, a round of data cleaning was performed. Not all the papers in the file were published after the year 2000, so data from those papers were filtered out. Next, the LLM was asked to evaluate the entire dataset in the context of all papers identify and remove any contradictions in the results or repeated results (corroborated across multiple papers). In this context, a contradiction would mean two sets of experimental conditions that were identical but disagree on the final state of the experiment: whether it reached critical point or not. 

In the context of my study, only one such contradiction came up, but was quickly cleared as both came from older papers and therefore filtered out. No repeats were found, and all results found to be consistent. 

**Results**
The final product was a single excel file of 154 relevant negative data points. I have the link pasted below in a Google Drive, for easy access. I believe this captures the essence of open source and also invites critique to improve the techniques used. These results are by no means perfect. 

https://drive.google.com/drive/folders/1Vf2_NblEiXuTLJL-7O1uD8xpYcy9hZn_?dmr=1&ec=wgc-drive-globalnav-goto

Up to this point the file has only tracked negative results — the non-critical conditions. The next step is to go back through the same papers and pull the critical conditions too (c=0), alongside the ones already logged (c>0 for adsorption, c<0 for exclusion). Capturing all three states in one file lets the extracted critical points be checked against two independent references: the manually curated records, and the parallel extraction effort running on a different model (Qwen). If all three agree on the same critical conditions, that's strong evidence the extraction process itself is trustworthy rather than model-specific.

I welcome any comments on any form of the strategy I used in this test. As I merely a curious high school students diving into a world I'm still very new to, feedback from people who know this field far better than I do is valuable. If you spot a condition I misread, a convention that should be tightened, or an assumption that doesn't hold up, I'd rather hear it now than progressing to the next step on a mistake.
