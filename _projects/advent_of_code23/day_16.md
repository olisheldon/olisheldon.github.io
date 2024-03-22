---
title: "Day 16: The Floor Will Be Lava"
description: Grid pathing <br/> Difficulty ★★
layout: nested
---

# Day 16: The Floor Will Be Lava

[**link**](https://adventofcode.com/2023/day/16)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day16.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day16.py)

## Description

This problem requires modelling laser beams moving through a configuration of mirrors and splitters. The configuration is given to us by a 2D grid. The mirrors ('`/`' and '`\`' characters) reflect the beam as you would expected, meanwhile splitters ('`-`' and '`|`') split the beam. A beam is split if the beam encounters a splitter while travelling perpendicular to its face. i.e. `-> \|`, `| <-` etc. A split beam results in two beams travelling parallel to the face of the splitter. 

The beams never react to each other, and energize the floor when passing over any part of the grid.

## Part 1

With a beam starting the top-left corner heading right, how many tiles end up being energized?

I solved this by maintaining a list of Laser's that have a coordinate and a direction. Iteratively, a laser is popped from the list and the laser is moved to its next tile and the affect this has is processed. Depending on the tile in which the laser lies, it may:

 - **Do nothing**: If on a ground tile, the laser with this new coordinate and same direction is added to the list of lasers.
 - **Change direction**: If on a mirror tile, the laser with this new coordinate but different direction is added to the list.
 - **Split**: If on a splitter tile, two new lasers with this new coordinate but perpendiular directions to the original laser (and opposite to each other) will be added to the list.

If a new laser is the same as one that has already been processed, it is skipped. This is done by maintaining a set of seen laser states.

Iterating until the list of lasers is empty, we return the number of grid tiles energized through this process by returning the length of the laser states set.

## Part 2

This process is repeated for lasers that begin at each edge of the grid pointing towards the center of the grid. We then return the maximumally energized grid produced by one of these lasers.

To do this, I repeated part 1 for each of the new laser states. No caching was used.

## Improvements

### Part 1

I stored the laser states to be processed in a list (first-in-last-out) data structure. Another implementation could use a queue (first-in-first-out) data structure.

A queue would produce a breadth-first search solution, meanwhile the list produces a depth-first search solution. But do these two approaches have different time complexity? Although in most problems, breadth-first search has a lower time complexity I argue that this is not the case for this problem and both approaches have the same time complexity because we avoid repeated work through the use of the laser_states set.

As we are not making any decisions, and instead are following a deterministic series of laser states, there is not necessarily any extra processing for the depth-first-style solution I used.

### Part 2

This is a very small extension of part 1, that can be solved using the same code in a reasonable amount of time.

However, my implementation could be much more efficient through caching but this would require large changes to the handling of seen laser states. 

Instead of only caching the seen laser states, we could also store a map of laser states to the number of energized states produced by this laser following this state. I think this change would make the solution approximately linear in time complexity at the cost of additional memory.

### Algorithms

### Software Engineering

I implemented laser states as having a coordinate and a direction, where the coordinates are two integers and the direction is NORTH, EAST, SOUTH, or WEST. 

The logic surrounding the grid tiles and new laser states could be massively simplfied by instead storing a laser states direction as the 2D Cartesian directions, i.e. NORTH=(-1, 0), EAST=(0, 1), SOUTH=(1, 0), or WEST=Coord(0, -1). 

I chose not to do this as this implies a laser could have a direction in any 2D direction but this is not true.


## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday16.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>