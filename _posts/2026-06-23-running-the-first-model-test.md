---
layout: post
title: "Running the First Model Test"
date: 2026-06-23
---
June 23 Post:

After two days of breaking down the reverse-phase PEG data, today I actually ran the first machine learning test on it. Here is how it went:
**DISCLAIMER: For the coding side, I used AI assistance, including Claude, to help write and run the scripts for the machine learning tests; the design of the test and the interpretation of the results are my own and my mentor's.**

The reverse-phase PEG data splits into solvent groups, with three that have enough entries to work with: methanol/water (32 entries), acetonitrile/water (23), and acetone/water (23). The question I wanted to answer was: if one such solvent group of sufficient size was excluded from the training data and set aside as the testing data, would a machine learning model, having learned only from the remaining 6 distinct solvent groups, still be able to correctly predict whether those held-out recipes of the seventh solvent group reach the critical point? This test can serve as a measure of whether the model has truly learned the role the 6 factors play in pushing the system towards the critical point.

The hypothesis is that a model that understands the role each factor plays should be able to handle a system it has never seen and determine whether that system is at its critical point. The excluded group that serves as the testing data comes into play here. Since we know all the cases in that group did in fact reach critical point, we can compare the model's results with the known "correct" answers to determine how well the model "learned".

First, before running the test, I had to deal with a fundamental limitation present in the data: there were no "failure" cases, or in other words, cases where the combinations of the 6 factors did not lead to the critical point. Every entry in the dataset is a confirmed, working recipe, which is a problem, because a model can't learn to tell a working recipe from a non-working one if it has only ever seen recipes that work. To solve this, I generated artificial "failure" cases by taking real recipes and deliberately altering one of the 6 factors at a time (for example, shifting the solvent ratio, changing the temperature, or swapping in a different solvent). But that raises a question: what is the best ratio of these artificially generated failures to successes in a data set to optimize the performance of the machine learning algorithm? 

This turns out to be a studied problem. A 2014 cheminformatics study by Kurczab and colleagues (link: https://link.springer.com/article/10.1186/1758-2946-6-32), which examined five machine learning algorithms (including Random Forest) for drug screening, found that the ratio matters. The percentage of negative training examples can negatively affect a machine learning model's accuracy but is also highly dependent on the task and dataset, with a larger share of failures generally favoring precision over recall (the model's ability to correctly recognize true positives). However, the study's goal (sifting a few drug candidates out of a massive dataset) differs from mine and they explicitly warn their ratio may not transfer. 

With this factor in mind, I tested four different failure-to-success ratios:

- 1:1 (balanced) 
- 3:1 
- 6:1 
- 9:1

**The two models I tested**

I ran this with two different machine learning models, to check whether the choice of model made a difference.

The first, a Random Forest, works like asking hundreds of simple yes/no questionnaires about a recipe and then taking a majority vote on the final answer. Produces a reliable result.

The second, XGBoost, builds its models one after another, where each new one focuses on correcting the mistakes the previous one made, increasing the overall accuracy.

Both of these models were run from Claude AI, with RDKit used to give context about the polymers and solvents.

Results:

**Random Forest**

| Held-out group | Ratio | Overall accuracy | Real recipes recognized | Failures caught |
|---|---|---|---|---|
| Methanol/Water | 1:1 | 53.1% | 12.5% | 93.8% |
|  | 3:1 | 75.0% | 0.0% | 100% |
|  | 6:1 | 85.7% | 0.0% | 100% |
|  | 9:1 | 90.0% | 0.0% | 100% |
| Acetonitrile/Water | 1:1 | 52.2% | 4.3% | 100% |
|  | 3:1 | 76.1% | 4.3% | 100% |
|  | 6:1 | 85.7% | 0.0% | 100% |
|  | 9:1 | 88.3% | 4.3% | 97.6% |
| Acetone/Water | 1:1 | 60.9% | 56.5% | 65.2% |
|  | 3:1 | 72.8% | 4.3% | 95.7% |
|  | 6:1 | 86.3% | 17.4% | 97.8% |
|  | 9:1 | 87.4% | 4.3% | 96.6% |

**XGBoost**

| Held-out group | Ratio | Overall accuracy | Real recipes recognized | Failures caught |
|---|---|---|---|---|
| Methanol/Water | 1:1 | 48.4% | 0.0% | 96.9% |
|  | 3:1 | 71.9% | 0.0% | 95.8% |
|  | 6:1 | 85.3% | 0.0% | 99.5% |
|  | 9:1 | 89.7% | 0.0% | 99.7% |
| Acetonitrile/Water | 1:1 | 50.0% | 4.3% | 95.7% |
|  | 3:1 | 76.1% | 8.7% | 98.6% |
|  | 6:1 | 84.5% | 4.3% | 97.8% |
|  | 9:1 | 90.0% | 0.0% | 100% |
| Acetone/Water | 1:1 | 58.7% | 39.1% | 78.3% |
|  | 3:1 | 78.3% | 26.1% | 95.7% |
|  | 6:1 | 87.0% | 8.7% | 100% |
|  | 9:1 | 90.0% | 0.0% | 100% |

Discussion:
The clearest pattern in both tables is that overall accuracy and real-recipe recognition move in opposite directions. As the failure-to-success ratio climbs from 1:1 to 9:1, overall accuracy steadily rises, approaching 90% in both models, while the percentage of real recipes the model correctly recognized, collapses toward zero. 
What actually matters here though is real reciped recognized. Overall accuracy, while it may seem like the best measure of how well the model performs, lumps both identification of false cases and true cases together. When failures vastly outnumber real recipes, as they do at the higher ratios, that single number becomes dominated by the failures. So as I added more failure cases, the model's overall accuracy climbed, not because it got better at recognizing real recipes, but because it got better at rejecting failures, and there were simply so many failures that getting those right was enough to push the overall score up. Meanwhile, its ability to recognize the real recipes, the actual goal, dropped.
Furthermore, looking at the actual percentages of real recipes identified, which is the key measure for this test, almost none were substantial. Across every solvent group, every ratio, and both models, the recognition rate was poor, frequently 0% and rarely climbing out of the single digits. The one apparent exception was the acetone/water group at the balanced 1:1 ratio, which reached roughly 40-57% depending on the model. But even that result sits right around the 50% mark, which for a two-outcome problem is no better than a coin flip. With only 23 acetone/water recipes in the test set, a result hovering near chance is most plausibly explained by random variation. In short, no result was strong enough or stable enough to conclude that the model actually learned the underlying rule for reaching the critical point.

Now: did the test work? 

Even though the results say otherwise, I beg to differ. 

The experiment itself worked exactly as intended. Both models basically "agreed" in their interpretation, and the results were to say the least, abysmal. But that failure isn't the end of it. From this, I realized these models were leaning almost entirely on recognizing the specific solvent systems they had already been trained on, rather than understanding the chemistry involved to reason about a new one. Even though RDKit gave the models chemical information about each solvent, this suggests information still wasn't enough to bridge the gap for the model to extend the reasoning gained from the training data to the excluded solvent system. 



