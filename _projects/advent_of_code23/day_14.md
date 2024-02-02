---
title: "Day 14: Parabolic Reflector Dish"
description: Physics simulation <br/> Difficulty ★★
layout: nested
---

# Day 14: Parabolic Reflector Dish

[**link**](https://adventofcode.com/2023/day/14)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day14.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day14.py)

## Description

This problem considers a 2D plane covered in two kinds of objects: rollable and non-rollable rocks. The 2D plane can tilt in any of the cardinal directions, causing the rollable rocks to move in the direction until meeting another object or the side of the plane. 

## Part 1

The objective for part one is to tilt the initial distribution of rocks in the north direction, and then calculate a value based on the distribution of these rocks on the dish, known as the total load. The total load is the sum of the number_of_rollable_rocks[index] * (index - plane.size()). Visualized below is a result of a tilting process, and the method for finding total load.

```
OOOO.#.O.. 10 = 5 * 10 +
OO..#....#  9 = 2 * 9  +
OO..O##..O  8 = 4 * 8  +
O..#.OO...  7 = 3 * 7  +
........#.  6 = 0 * 6  +
..#....#.#  5 = 0 * 5  +
..O..#.O.O  4 = 3 * 4  +
..O.......  3 = 1 * 3  +
#....###..  2 = 0 * 2  +
#....#....  1 = 0 * 1
                 = 136
``` 

My approach to solving this was to iterate through all rocks, moving each one a single unit until a whole iteration of this resulted in no rocks moving. At this point, I know that the tilting has produced its stable state and the total load can be calculated.

## Part 2

For part 2, the complexity is increased massively. Instead of a single tilt in the northern direction to produce a stable state, we instead tilt in each cardinal direction: north, west, south, and finally east, with each tilt producing its stable state. Then, this 'cycle' is repeated for a total number of 1000000000 times.

This is equivalent to performing the algorithm for part one 1000000000 * 4 times! Although my part one solution is quite fast, this number of runs is not feasible in a realistic amount of time. In fact, I calculated that my part one solution would take 34348000 seconds or ~one year to complete.

To complete this, it was important to realize that the process of tilting the cardinal directions pushed the rollable rocks to the outside of the 2D plane. Therefore, if we consider a state to be the position of every rock, as well as its rollability, on the plane we can utilize caching of these states to massively reduce our time complexity.

So this is what I did, I created a dictionary mapping a state (2D plane of rocks) to its next state. Then, while iterating if I found that a cycle resulted in the same score as the previous cycle then we must have already calculated the result of a cycle from this starting state. This means that all cycles from this point have already been determined and we can simply return the score from the beginning of this cycle.

## Improvements

### Part 1

### Part 2

### Algorithms

I don't know of any algorithms to improve this solution.

### Software Engineering

There is lots of repeated code in the algorithms for tilting in the cardinal directions. This could be greatly simplified by exploiting the symmetry of tilting. i.e. You can tilt a 2D array in the southernly direction using a northernly algorithm by reversing the array. However, this would also come with a performance hit due to copying and reversing the array.

I also wonder if the caching could have been written in a nicer way, using functools.lru_cache instead of my own solution.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday14.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>