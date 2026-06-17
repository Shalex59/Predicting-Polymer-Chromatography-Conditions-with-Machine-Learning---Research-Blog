layout: post
title: "Why I'm Building This"
date: 2026-06-17

Polymer chemists trying to characterize complex polymer samples, branching, end groups, chain topology, rather than just molecular weight, rely on a specialized chromatography technique called LCCC (liquid chromatography at critical conditions). The issue is the large amount of time, effort, and empirical data required for these projects, not to mention the costs associated with such a project. Finding the right combination of solvent ratio, column type, and temperature to actually reach that critical condition for a given polymer is mostly trial and error, and the data on what's worked before is scattered across decades of individual papers.

Working with Yongmei Wang, a Professor of Chemistry at the University of Memphis, whose recent paper in collaboration with Brinton Eldridge and Dillon Baker I have included here (https://doi.org/10.1016/j.chroma.2025.465821) introduced a curated database of 428 confirmed critical conditions hand collected from over 300 papers.

This project is my attempt to build a predictive model that is trained on PolyCrit's confirmed conditions, then test whether it can predict a likely solvent ratio, column, temperature, as well as other parameters for polymers it wasn't trained on. Rather than asking a flat yes-or-no question (whether or not the certain combination would result in LCCC), I'm framing it as a recipe-prediction problem, then checking how close the model's suggestion lands to the real, confirmed condition reported in the data set. But that validation step isn't the end goal, the real point is to eventually predict likely conditions for polymers and solvent systems that have never been tested at all, giving scientists using PolyCrit a starting recipe to save time and effort.

I'll be posting updates here as I work through the data processing, the model itself, and how well it actually holds up.
