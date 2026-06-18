---
layout: post
title: "How LCCC Works, and Why It Matters"
date: 2026-06-18
---
June 18 2026 Entry

Today's focus was building a clearer picture of the actual mechanism behind LCCC, and what that mechanism is good for in practice.

**The basic mechanism**

Liquid chromatography, broadly, works by dissolving a sample in a liquid and pushing it through a column packed with tiny beads. How long each molecule takes to exit the column depends on how it interacts with those beads. Standard chromatography techniques pick one of two strategies. Size Exclusion Chromatography (SEC) uses beads with small pores, so smaller molecules wander into the pores and are delayed, while larger molecules pass through faster, sorting everything by molecular weight. Liquid Adsorption Chromatography (LAC) does the opposite, using a bead surface that chemically attracts the polymer, so molecules that stick more come out later.

LCCC works by balancing two opposite forces acting on the polymer near the surface of the tiny beads packed inside the column.

The first force, entropy, pushes the chain away from the bead surface. A polymer chain likes having lots of room to bend and coil into different shapes. Near a surface, it has less room to do that, so it tends to stay away if it can.

The second force, enthalpy, pulls the chain toward the bead surface. If the beads are chemically "sticky" to the polymer, the chain wants to cling to them.

LCCC happens when these two forces are designed to exactly cancel each other out. When that balance is met, the polymer's size stops mattering at all, long chains and short chains of a class of polymers all behave the same way. The only thing left to cause separation is structure: things like branching, shape, or what's attached to the ends of the chain.

**Why this matters: applications**

*Quality control.* Manufacturers producing polymers for specific uses need more than the right molecular weight, they need the right structure. A polymer with unwanted branching or incomplete end-group reactions can behave very differently from the intended product, even if its average molecular weight looks correct. Since SEC cannot detect this, LCCC fills the gap by separating samples purely on structural grounds, making it possible to verify that a batch was actually synthesized correctly.

*Purification and enrichment.* Because LCCC strips molecular weight out of the separation entirely, whatever comes off the column at a given retention time is structurally uniform, even if the original sample was a mixture of sizes. This is especially useful for block copolymers (polymers built from two joined segments), where a common synthesis problem is leftover unreacted homopolymer that never successfully joined to the other block. Running the mixture at the critical condition of one segment separates the true block copolymer from this leftover material, an enrichment step that SEC cannot achieve since the leftover homopolymer and the finished copolymer can have overlapping molecular weights.

