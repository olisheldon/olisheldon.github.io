---
title: "Day 10: Pipe Maze"
description: Graph no pathfinding <br/> Difficulty ★★
layout: nested
---

# Day 10: Pipe Maze

[**link**](https://adventofcode.com/2023/day/10)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day10.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day10.py)

## Description

In day 10 we are asked to consider a 2D grid of tiles. Each tile can be occupied by ground, a starting position, or a pipe that connects any two different cardinal directions. There is an animal at the starting position, and we are guaranteed that the starting position contains a pipe. We are also guaranteed that this starting position is connected to a series of pipes that form a large loop.

## Part 1

For part 1, we need to analyse the loop containing the starting position, and return furthest distance (L1) from the starting point moving within this loop.

It is tempting to interpret this problem as a graph, but it is actually much simpler. As we are given a starting position within the pipe, and are guaranteed that the pipe forms a loop we just need to follow the logic of the pipe we are entering and bear in mind the direction in which we entered the pipe.

## Part 2

For part 2, we are asked to find the area enclosed by the loop. The natural solution to this is to 'flood' the outside of the loop, and then calculate the area inside the loop from this. However, the area inside the loop has a stricter definition that does not allow for this simple strategy.

To be outside of the loop, there does not need to be a path of ground tiles to the edge of the map for a region to be considered outside the loop. i.e. squeezing between the pipes is also allowed.

```
...........    ...........
.S-------7.    .S-------7.
.|F-----7|.    .|F-----7|.
.||.....||.    .||OOOOO||.
.||.....||. -> .||OOOOO||.
.|L-7.F-J|.    .|L-7OF-J|.
.|..|.|..|.    .|II|O|II|.
.L--J.L--J.    .L--JOL--J.
...........    .....O.....
```

but also

```
..........    ...........
.S------7.    .S------7.
.|F----7|.    .|F----7|.
.||....||.    .||OOOO||.
.||....||. -> .||OOOO||.
.|L-7F-J|.    .|L-7F-J|.
.|..||..|.    .|II||II|.
.L--JL--J.    .L--JL--J.
..........    ..........
```
(Taken from [**Advent of Code Day 10 Example**](https://adventofcode.com/2023/day/10))

A strategy for checking whether a coordinate is inside or outside of a loop is to count the number of times the loop is crossed. Looking at this, a few rules can be made:

 - An inside region requires an odd number of loop-crossing to reach the edge of the tiles.
 - An outside region requires an even number of loop-crossing to reach the edge of the tiles.

However, coding this implementation still gave me an incorrect answer. After some more thinking, it is clear that these rules for determining regions inside and outside of the loop, while correct, require a stricter definition of crossing the loop.

#### Crossing Examples

Consider the following examples where '>' shows our position and direction we are considering:

##### Crossing Example 1

```
>|
```

This is clear crossing.

##### Crossing Example 2

```
>-
```

For this example, we must already be on a pipe that connects to this one, so this does not cross.

##### Crossing Example 3

```
>L-7
```

How many crossings does this contain? I argue one (consider a 2D line, how many times would it cross?)

##### Crossing Example 4

```
>F-7
```

This does not count as a crossing.

### Part 2 Summary

With these extra rules for crossing, I get a value that is one larger than the correct answer. There is clearly a bug in the part 2 solution that should be debugged.

Following more testing with more inputs, it is clear that my solution will always find more interior parts than are actually present.


<!-- ## Improvements -->

<!-- ### Part 1 -->

<!-- ### Part 2 -->

My implementation has a bug in it so I do not get the correct answer. I need to look more into this.

<!-- ### Algorithms -->

### Software Engineering

A critique of my code is that the `Tile` class attribute 'segment' should be handled by the `Maze` instance.


## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday10.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>