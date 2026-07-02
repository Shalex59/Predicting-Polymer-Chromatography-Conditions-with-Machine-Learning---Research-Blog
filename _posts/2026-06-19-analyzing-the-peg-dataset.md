---
layout: post
title: "Analyzing the PEG Dataset"
date: 2026-06-19
---
June 19 2026 Entry

In my first post, I explained how LCCC works: it's a way of running polymers through a chromatography column so that their size stops mattering, leaving only structural differences like branching or end groups to separate them. Today I started actually digging into real data to see what that looks like in practice, using one specific polymer as a starting point: PEG.

PEG, or polyethylene glycol, is a simple, well-studied polymer made of a repeating chain of small oxygen and carbon units. It shows up constantly in research and industry, in things like drug delivery, cosmetics, and lab chemistry, partly because it is cheap, well understood, and easy to modify. Because it's so widely used and so well studied, these factors make it a good first polymer to dig into before moving to less-studied ones.

**What the dataset is**

The dataset I'm working with contains every PolyCrit entry for PEG, 129 separate cases pulled from published research, each one describing a specific recipe (a solvent mix, a column type, a temperature) that successfully got PEG to its critical point. Each entry also comes with a quality and reliability rating, since not every published result is equally trustworthy. For now, I'm keeping every entry in the dataset rather than removing any, as considering all factors at once would multiply the complexity manyfold.

Before I could really look at the data, it needed some cleanup. Some entries didn't report a temperature at all, so I filled those in with 25°C (room temperature), since that's where almost all of the experiments cluster anyway. The bigger issue was that researchers reported their solvent amounts in two different ways, some by weight, some by volume, so I converted everything to one consistent format (weight percent) using the actual densities of each solvent. That way, every entry can be compared apples to apples.

**Getting more information about the solvents**

To understand the solvents a little better, I used a tool called RDKit, free chemistry software that can take a molecule and describe it using a few simple numbers, like how water-loving or oil-like it is, and how much it tends to form hydrogen bonds. My mentor suggested this as a way to add some chemical context behind the plain solvent names. Right now, I'm just using these numbers as background information, not drawing any conclusions from them yet.

**Why this kind of analysis matters**

The bigger goal here is prediction. If I can collect and organize enough confirmed recipes like these, I can start looking for patterns in what makes a recipe actually work for a given polymer. That matters because finding these recipes by hand, through trial and error in a lab, takes a lot of time and money. Getting a clear, organized picture of the data that already exists is the first step before any of that prediction work can happen. This post, however, is the first of many posts

**Narrowing the factors**

I talked with my mentor about all the different details tracked in the dataset, and which ones actually matter most for this kind of analysis. She confirmed that six factors are the key ones to focus on for now: the polymer itself, the solvents used, the solvent ratio, the temperature, the stationary phase, and the base material of the column. Everything else tracked in the dataset can be set aside for the time being. Going forward, this analysis and the posts that follow will focus on just these six factors.

**An explanation of each of the factors**
The polymer itself. This is just which polymer is being tested, PEG in this case. It matters because every polymer has its own chemistry, so the recipe that works for one won't necessarily work for another.

The solvents used. This is the liquid (or mix of liquids) pushed through the column. Different solvents have different chemical personalities and behaviors.

The solvent ratio. When more than one solvent is used together (which is most of the time), this is the proportion of each one in the mix, like 80% methanol and 20% water. Even with the same two solvents, changing this ratio can be the difference between hitting the critical point and missing it entirely.

The temperature. How hot or cold the column is kept during the run. Temperature affects how strongly the polymer interacts with the column material

The stationary phase. This is the actual column itself, specifically, the type of coating or chemistry on the beads packed inside it that the polymer interacts with as it flows past. This is what was called "Phase" in the data, normal, reverse, or HILIC, referring to whether the surface is polar or hydrophobic.

The base material of the column. This is what the beads themselves are physically made of, before any coating is applied, most commonly silica in this dataset. It's the underlying structural material that the stationary phase chemistry is built on top of.

Together, these six are basically "what polymer, in what liquid, at what ratio, at what temperature, through what kind of surface, built on what material," which is the full recipe needed to describe any single LCCC experiment (at least for the most part).
