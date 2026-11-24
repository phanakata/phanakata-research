---
layout: post
title:  "KiriSMILES: kirigami as one line of text"
date:   2026-11-24 11:00:00
categories: kirigami
image: /img/kirismiles/panels.png
author: Paul Hanakata
---

**In one sentence:** KiriSMILES writes any kirigami cut pattern as one line of text, simulates it with an open finite element engine, and lets both researchers and AI agents design, check and simulate kirigami with the same tools.
[Code on GitHub](https://github.com/phanakata/kirismiles) (MIT) &middot; preprint on arXiv soon.

`P5x45S1/2O0[V42@0,0]N18E3` &rarr; the classic alternating-slit sheet

#### 1. The problem
Kirigami turns a flat sheet into something that stretches, twists, pops up or snaps, just by cutting it. But designs are shared as figures, one-off parameters or cut files with hundreds of coordinates, so they are hard to compare, reuse or collect into data sets.

<img src="{{ site.baseurl }}/img/kirismiles/panels.png" alt="Four simulated kirigami designs" />

#### 2. The idea: SMILES for kirigami
A crystal is a lattice plus a basis. A KiriSMILES string is a lattice plus a motif of cuts, or pieces combined by mirrors, inversions and repeats. Every string maps to one finite pattern, is checked before anything is cut, and gets a canonical identity, so the same design written two ways is recognised as one. Motifs can be grouped into **supercells**: four slits A&ndash;D as one cell, or a pitch cell (A) and a roll cell (B) in a 2&nbsp;&times;&nbsp;2 layout.

<img src="{{ site.baseurl }}/img/kirismiles/supercell.png" alt="Supercells shaded by cell type" />

#### 3. It moves
Each string becomes a mesh, solved with FEniCSx (a F&ouml;ppl&ndash;von K&aacute;rm&aacute;n plate and a Kirchhoff&ndash;Love shell) through buckling and large rotations. Pull the sheet and a cut cell pitches, rolls or yaws.

<table class="image"><caption align="bottom">pitch &middot; roll &middot; yaw</caption><tr>
<td><img src="{{ site.baseurl }}/img/kirismiles/pitch.gif" alt="pitch" /></td>
<td><img src="{{ site.baseurl }}/img/kirismiles/roll.gif" alt="roll" /></td>
<td><img src="{{ site.baseurl }}/img/kirismiles/yaw.gif" alt="yaw" /></td>
</tr></table>

#### 4. Combine cells: a motion sequence
Cells joined in series carry the same force, so the softest moves first. In the [A,&nbsp;B;&nbsp;B,&nbsp;A] sheet the roll cells (B) turn first; the pitch cells (A) wait until about 7% stretch, then tilt to 36&deg; while B reaches 67&deg;. The order is set by the cuts, a route to programmed motion sequences.

<img src="{{ site.baseurl }}/img/kirismiles/pitch_roll_2x2.gif" alt="Pitch and roll supercell stretched" />

#### 5. Published designs, replicated
Twenty designs from the literature written as strings and simulated: single slits (buckling force and scaling), kirigami actuators, rotating squares, multistable stars, hierarchical cuts, kirigami skins, and rolled kirigami shells whose pop-ups start at one end and spread, as in experiments. Any design also exports to MuJoCo, the physics engine behind much of robot learning.

<table class="image"><caption align="bottom">rolled kirigami shell &middot; the same string in MuJoCo, pulled by a robot gripper</caption><tr>
<td><img src="{{ site.baseurl }}/img/kirismiles/tube.gif" alt="rolled kirigami shell" /></td>
<td><img src="{{ site.baseurl }}/img/kirismiles/gripper.gif" alt="MuJoCo gripper" /></td>
</tr></table>

#### 6. One platform for people and AI agents
Notation, solver, job queue and a results database indexed by design identity. Researchers use a web app, the command line or Python; AI agents such as Claude use the same tools through an MCP server: write a design, check it, preview it, simulate it, export laser-cut files.

<img src="{{ site.baseurl }}/img/kirismiles/platform.png" alt="Platform diagram" />

#### Why I built it
> During my PhD and postdoc I wanted to solve the inverse design problem of kirigami: from a target behaviour back to the cuts. Writing the code was the bottleneck. Building KiriSMILES with an AI coding assistant changed that, and I hope it becomes a common language for kirigami and a testing ground for AI agents that design materials.

**Code:** [github.com/phanakata/kirismiles](https://github.com/phanakata/kirismiles) (release v0.2.0). Designs, feedback and collaborations welcome.
