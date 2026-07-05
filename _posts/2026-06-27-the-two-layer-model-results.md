---
layout: post
title: "The Two-Layer Model Results"
date: 2026-07-04
---
June 4 2026 Entry

The two-layer model is built and tested. This is the design from the last few posts: Layer 1 converts each recipe into eleven similarity scores describing how much its chemistry resembles eleven reference solvents, and Layer 2 takes those scores plus the experimental conditions and predicts whether the recipe reaches the critical point.

I ran the two-layer model under two different data splits so I could compare them directly. The first was a random split, where the model sees some examples of every solvent group during training. The second was the hold-out-by-group split from the very first test, where an entire solvent group is removed and the model has to recognize it having never seen its chemistry. The ratio of negative data points to positive ones is 3:1. The key metric, as always, is how many of the real critical-point recipes the model correctly recognizes.

**The results**

On the random split, the two-layer model did well. It recognized about 75% of real recipes with Random Forest and about 64% with XGBoost. For the hold out test, the results were once again horrible.

| Split | Random Forest | XGBoost |
|---|---|---|
| Random split | 74.5% | 63.6% |
| Held out Methanol+Water | 0.0% | 9.4% |
| Held out Acetonitrile+Water | 0.0% | 0.0% |
| Held out Acetone+Water | 0.0% | 4.3% |


**What this means**

This was the disappointing part. The whole point of the similarity layer was to let the model reason about unfamiliar solvents by relating them to familiar ones. If it worked, the hold-out-by-group numbers should have improved over the first test. They didn't, unfortunately. 

Likely, the reason lies in the design and data in the study. The similarity approach works by placing each recipe at a location in a chemical map and reasoning from nearby examples. But with only seven solvent groups, three of them large, an entirely held-out group lands in an empty region of that map with no training examples nearby.The bridge needs stepping stones, basically intermediate chemistries to connect the familiar to the unfamiliar, and there simply aren't enough distinct solvent systems in the data to form that path. Furthermore, with the limited number of data points included (344 in total) a solid bridge could not be formed due to the lack of data. 

The problem, therefore, is not with the study design but with the data. The two-layer model, the random split, the fingerprint similarity, all of these were reasonable approaches, and the design does what it should. However, the key issue in each of these tests was the data itself that was limiting how well the tests could have been performed. So the next step is to go back to the beginning and gather more data, specifically real negative results. Rather than relying on artificially generated failures, I'll pull non-critical conditions directly from the research papers already collected in this study. This can bolster data diversity and amount and can give machine learning models a wider range of information to work with.
