---
title: "Day 25: Snowverload"
description: Graph Theory (Bidirectional) <br/> Difficulty ★★★
layout: nested
---

# Day 25: Snowverload

[**link**](https://adventofcode.com/2023/day/25)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day25.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day25.py)

## Description

For this days problem we are presented with many machines that have been wired together. This is a graph with bidirectional edges.

## Part 1

We are asked to remove three wires such at least half of the machines are disconnected. i.e. this action should divide the components into two separate, disconnected groups. Once the wires have been removed, return the product of the number of machines within each of the disconnected groups.

I am not sure how I should approach this problem. I have seen similar problems solved using Physics simulations of graphs (modelling vertices as springs and such), but I am not sure this can be applied here.

<!-- ## Part 2 -->

<!-- ## Improvements -->

<!-- ### Part 1 -->

<!-- ### Part 2 -->

### Algorithms

I need to learn more graph theory to solve this. To begin, I would read about:

 - Karger's Algorithm
 - Ford-Fulkerson

<!-- ### Software Engineering -->


## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday25.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>