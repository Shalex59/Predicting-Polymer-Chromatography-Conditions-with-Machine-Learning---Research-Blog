---
layout: post
title: "Breaking Down the Six Factors"
date: 2026-06-21
---
June 21 2026 Entry

I previously narrowed the PEG dataset down to six factors that matter most: the polymer, the solvents, the solvent ratio, the temperature, the stationary phase, and the base material. Today I looked closer at what each of those six factors actually contains, then set up a specific test to see whether a machine learning model can learn anything useful from them. I did decide to combine 2 factors (base material and stationary phase temporarily for this post as they are similar enough and can be grouped). During the actual algorithm run, they will be seperated again into 2 factors.

**1. Polymer**

Every entry in this dataset is the same polymer, PEG. There's no variation to look at here yet, since this file was filtered down to just one polymer from the start. This will matter more once a second polymer is brought in for comparison.

**2. Phase, and why I'm narrowing to reverse phase**

Before getting into the solvent details, one factor needs explaining first: phase. Every stationary phase in the dataset is categorized as normal, reverse, or HILIC. A normal-phase column has a polar surface, while a reverse-phase column has a hydrophobic, carbon-coated surface, and the solvent recipe that works for one is generally not the recipe that works for the other. Because of that, lumping both together would blur the patterns in the data rather than reveal them.

Of the 129 total PEG entries, 88 are reverse phase, 26 are normal phase, 2 are HILIC, and 13 don't report a phase at all. Since reverse phase makes up the large majority of well-documented entries, the rest of this analysis, and the model test below, will focus only on reverse-phase data going forward.

**3. Solvents (reverse phase only)**

After combining entries that listed the same solvents in a different order, there are 8 distinct solvent groups in the reverse-phase data:

- Methanol + Water — 32 entries
- Acetonitrile + Water — 23 entries
- Acetone + Water — 23 entries
- Hexane + Tetrahydrofuran — 3 entries
- Acetone + Methanol + Water — 3 entries
- Water (single solvent, no pairing) — 2 entries
- Acetonitrile + Methanol + Water — 1 entry
- Chloroform + Heptane + Methanol — 1 entry

But since water itself isn't a solvent pair, we will exclude it from this data set (therefore 7 left）.

Three systems, methanol/water, acetonitrile/water, and acetone/water, make up 78 of the 88 entries between them. Everything else is rare, several groups appear only once, twice, or three times, therefore relatively insignificant in terms of this specific test.

**4. Solvent ratio (reverse phase only)**

Solvent amounts were originally reported in two different units, some by weight and some by volume, so all of them were converted to a single consistent format (weight percent) using the actual density of each solvent (taken from RDKit). For each system, the average composition and its standard deviation tell us both the typical recipe and how consistent that recipe is across studies:

- Methanol + Water (32 entries): 80.6% methanol / 19.4% water, standard deviation 4.6%
- Acetonitrile + Water (23 entries): 43.5% acetonitrile / 56.5% water, standard deviation 10.2%
- Acetone + Water (23 entries): 54.4% acetone / 45.6% water, standard deviation 31.0%
- Hexane + Tetrahydrofuran (3 entries): 29.0% hexane / 71.0% THF, no spread (all three identical)
- Acetone + Methanol + Water (3 entries): roughly 15% acetone / 41% methanol / 43% water, with wide variation
- Acetonitrile + Methanol + Water (1 entry): 24.2% acetonitrile / 56.8% methanol / 19.0% water
- Chloroform + Heptane + Methanol (1 entry): 74.6% chloroform / 21.0% heptane / 4.4% methanol 

**5. Temperature (reverse phase only)**

93 of the original 129 entries reported an actual temperature; the rest were filled in with 25°C, room temperature. Looking at just the entries that reported a real value, the average is 29.4°C with a standard deviation of 9.9°C, and the full range runs from 1.5°C up to 68°C. Most experiments cluster near room temperature, but a meaningful number run hotter.

**6. Stationary phase and base material (reverse phase only)**

Within the reverse-phase entries, there are 39 distinct named stationary phase products overall, the two most common being Nucleosil C18 (22 entries) and Novapak C18 (8 entries), both carbon-18-coated columns. For base material, silica dominates heavily across the dataset (111 of 129 entries total), with a small number of alternative materials making up the rest.

