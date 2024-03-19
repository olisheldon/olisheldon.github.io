---
title: "Day 22: Sand Slabs"
description: Tetris Physics <br/> <br/> <br/> Difficulty ★★
layout: nested
---

# Day 22: Sand Slabs

[**link**](https://adventofcode.com/2023/day/22)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day22.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day22.py)

## Description

This problem considers cuboids, defined by their edge points, falling with 'Tetris-style' physics in the -Z direction.

We are supplied with a snapshot of these cuboids edge points as they are falling, given in 3D integer cartesian coordinates.

Tetris physics means there is no toppling, so a cuboid will stop falling if there is an occupied space anywhere immediately beneath it.

The free-falling bricks can only be positioned in integer coordinates.


## Part 1

### Falling

We must let the bricks fall, and then determine how many of the bricks in this equilibrium, fallen state can be individually destroyed without causing any other bricks to fall.

To solve this, I first found it important sort the bricks in order of height. I then found a way to calculate if two bricks overlap in the x-y plane. Then, with this information, a nested loop lcan be run on each pair of bricks in height-ascending order, if the pair of bricks overlap we then update the higher bricks Z-position to the lower bricks Z-position + 1. 

After iterating through each pair in this way, we are guaranteed to have found the equilibrium state for the falling bricks.

This is an `O(N**2)` time complexity. Could a better algorithm be used to solve this?

### Disintegrating

Using this equilibrium state, we must now determine how many of the bricks in this fallen state can be individually destroyed without causing any other bricks to fall.

I approached this by creating two dictionaries:

 - A dictionary of bricks to the bricks it supports
 - A dictionary of bricks to the bricks it is supported by

Using these dictionaries, finding the bricks that are safe to disintegrate is trivial. For each brick, find the bricks supported by it and check if they are all supported by at least one other brick. If this is true, the brick can be safely disintegrated.

And with this, part 1 is complete.


## Part 2

For part 2, we consider the effect of distintegrating each brick and the chain reaction caused by each individual disintegration. For each brick, we disintegrate it and count the number of bricks that will fall due to this disintegration. We find this number for each brick, and return their sum.

To solve this we use breadth-first fill. For each brick, we disintegrate it and create a queue of objects which we only prevented from falling by that brick. We also maintain a set of bricks that are now falling due to this brick's disintegration. 

With this disintegrated brick and queue of bricks that are now falling directly because of the disintegrated brick, we iterate through the queue as follows:

For each no-longer supported brick, iterate through each brick that will now cascade because it was being supported by the brick that has now been disintegrated. If this cascading brick is not already falling, and everything that supports the cascading brick is already falling (or was disintegrated), then we have determined that this cascading brick is a falling brick, so we must add the cascading brick to the queue **AND** add it to the set of falling bricks. We iterate in this way through the queue until the queue is finally empty, add the number of cascading bricks to a count and move onto considering the next bricks disintegration. 

## Improvements

### Part 1

#### Falling

The `O(N**2)` algorithm for is definitely not optimal.

#### Disintegrating

### Part 2

### Algorithms

### Software Engineering

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday22.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>