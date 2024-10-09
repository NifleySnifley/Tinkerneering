---
layout: project
projid: aocvis
title:  "AoC Visualizations"
date:   2022-12-1 00:00:00 -0500
categories: project
description: Visualizations I have created for various Advent of Code problems that I have solved
image: aoc/passagepathing.png
links:
 - "[ObservableHQ Collection](https://observablehq.com/collection/@nifleysnifley/advent-of-code-visualizations)"
---

### Some Fun Interactive Visualizations

<div id="observablehq-display-534c2430"></div>
<p>Credit: <a href="https://observablehq.com/@nifleysnifley/advent-of-code-2021-day-12-passage-pathing">Advent of Code 2021 day 12 - Passage Pathing by Nifley</a></p>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@observablehq/inspector@5/dist/inspector.css">
<script type="module">
import {Runtime, Inspector} from "https://cdn.jsdelivr.net/npm/@observablehq/runtime@5/dist/runtime.js";
import define from "https://api.observablehq.com/@nifleysnifley/advent-of-code-2021-day-12-passage-pathing.js?v=3";
new Runtime().module(define, name => {
  if (name === "display") return new Inspector(document.querySelector("#observablehq-display-534c2430"));
});
</script>

<br/>

<div id="observablehq-vis-f4a897c7"></div>
<p>Credit: <a href="https://observablehq.com/d/dfbc255dac63ec6c">Advent of Code 2022 day 12 by Nifley</a></p>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@observablehq/inspector@5/dist/inspector.css">
<script type="module">
import {Runtime, Inspector} from "https://cdn.jsdelivr.net/npm/@observablehq/runtime@5/dist/runtime.js";
import define from "https://api.observablehq.com/d/dfbc255dac63ec6c.js?v=3";
new Runtime().module(define, name => {
  if (name === "vis") return new Inspector(document.querySelector("#observablehq-vis-f4a897c7"));
});
</script>

<br/>

<div id="observablehq-vis-1791fb54"></div>
<p>Credit: <a href="https://observablehq.com/@nifleysnifley/smoke-basin@807">Advent of Code 2021 day 9 - Smoke Basin by Nifley</a></p>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@observablehq/inspector@5/dist/inspector.css">
<script type="module">
import {Runtime, Inspector} from "https://cdn.jsdelivr.net/npm/@observablehq/runtime@5/dist/runtime.js";
import define from "https://api.observablehq.com/@nifleysnifley/smoke-basin@807.js?v=3";
new Runtime().module(define, name => {
  if (name === "vis") return new Inspector(document.querySelector("#observablehq-vis-1791fb54"));
});
</script>

<br/>
<div id="observablehq-vis-62f40790"></div>
<p>Credit: <a href="https://observablehq.com/@nifleysnifley/chiton@712">AOC 2021 Day 15 - Chiton by Nifley</a></p>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@observablehq/inspector@5/dist/inspector.css">
<script type="module">
import {Runtime, Inspector} from "https://cdn.jsdelivr.net/npm/@observablehq/runtime@5/dist/runtime.js";
import define from "https://api.observablehq.com/@nifleysnifley/chiton@712.js?v=3";
new Runtime().module(define, name => {
  if (name === "vis") return new Inspector(document.querySelector("#observablehq-vis-62f40790"));
});
</script>

### 2023 Day 16

<iframe width="100%" height="512" src="https://www.youtube.com/embed/YhZxmCaunBw" title="AdventOfCode 2023 Day 16 Visualization" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<br/>

### 2023 Day 17

<div style="width: 100%; height: fit-content, display: block; overflow: auto;">
{% include image.html file="aoc/2023_17_p1.png" astyle="width:40%; float:left;margin-left:5%" caption="Part 1 solution" %}
{% include image.html file="aoc/2023_17_p2.png" astyle="width:40%; float: right; margin-right: 5%" caption="Part 2 solution" %}
</div>
<br/>

### 2023 Day 23

<div style="width: 100%; height: fit-content, display: block; overflow: auto;">
{% include image.html file="aoc/2023_23.png" astyle="width:40%; float:left;margin-left:5%" caption="Compressed Graph" %}
{% include image.html file="aoc/2023_23_txt.png" astyle="width:40%; float: right; margin-right: 5%" caption="Maze sections to be compressed" %}
</div>
<br/>

### 2023 Day 24

<iframe src="https://www.desmos.com/3d/8fb47d9770" width="100%" style="min-height:60vh"></iframe>
<br/>

### APCSA Treasure Hunt

This isn't an Advent of Code visualization, but its a visualization/rewrite of a project I was assigned in computer science class involving the solving of mazes of varying complexity. The solution uses Dijkstra's algorithm to find the shortest paths between the starting position, and between the multiple treasures if applicable. If there are multiple treasures, the 2-opt local search algorithm is used to find a reasonable solution in to the traveling salesperson problem without excessive computation. I won 1st place overall in the competition between AP Computer science students amongst the three local high schools.
<div id="observablehq-rendering-dfc1b664"></div>
<div id="observablehq-viewof-target-dfc1b664"></div>
<div id="observablehq-viewof-mapSel-dfc1b664"></div>
<p>Credit: <a href="https://observablehq.com/d/5cdae8bc4d6c5dd8">Pathfinding by Nifley</a></p>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@observablehq/inspector@5/dist/inspector.css">
<script type="module">
import {Runtime, Inspector} from "https://cdn.jsdelivr.net/npm/@observablehq/runtime@5/dist/runtime.js";
import define from "https://api.observablehq.com/d/5cdae8bc4d6c5dd8.js?v=3";
new Runtime().module(define, name => {
  if (name === "rendering") return new Inspector(document.querySelector("#observablehq-rendering-dfc1b664"));
  if (name === "viewof target") return new Inspector(document.querySelector("#observablehq-viewof-target-dfc1b664"));
  if (name === "viewof mapSel") return new Inspector(document.querySelector("#observablehq-viewof-mapSel-dfc1b664"));
  return ["map","treasureDistances","sortedTreasures","totalPath","calculatePathCost","cellSize","calculateTraversalCost","optimizedTreasures"].includes(name);
});
</script>
