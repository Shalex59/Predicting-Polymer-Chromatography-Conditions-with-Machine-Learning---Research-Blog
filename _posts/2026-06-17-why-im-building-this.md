---
layout: post
title: "My first post: Motivation and Background"
date: 2026-06-17
---
June 17 2026 Entry

Polymer chemists trying to characterize complex polymer samples, branching, end groups, chain topology, rather than just molecular weight, rely on a specialized chromatography technique called LCCC (liquid chromatography at critical conditions). The challenge is the substantial amount of time, effort, and empirical data such characterization requires, along with the associated costs. Finding the right combination of solvent ratio, column type, and temperature to actually reach that critical condition for a given polymer is largely a matter of trial and error, and the data on what has worked before is scattered across decades of individual papers.

I am collaborating with Yongmei Wang, Professor of Chemistry at the University of Memphis, whose recent paper with co-authors Brinton Eldridge and Dillon Baker, [PolyCrit: An Online Collaborative Platform for Polymer Characterization](https://doi.org/10.1016/j.chroma.2025.465821), introduced a curated database of 428 confirmed critical conditions collected from over 300 papers.

This research aims to build a predictive model trained on PolyCrit's confirmed conditions, then test whether it can predict a likely solvent ratio, column, and temperature, along with other relevant parameters, for polymers it was not trained on. Rather than asking a flat yes-or-no question, whether or not a given combination would result in LCCC, the model is framed as a recipe-prediction problem, checking how close its suggestion lands to the real, confirmed condition reported in the dataset. That validation step is not the end goal; the actual aim is to eventually predict likely conditions for polymers and solvent systems that have never been tested at all, giving researchers using PolyCrit a starting recipe to save time and effort.

Updates will be posted here as the data processing, model development, and evaluation progress.
