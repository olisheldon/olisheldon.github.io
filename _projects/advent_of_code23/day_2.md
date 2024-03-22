---
title: "Day 2: Cube Conundrum"
description: Constraint checking <br/> Difficulty ★
layout: nested
---

# Day 2: Cube Conundrum

[**link**](https://adventofcode.com/2023/day/2)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day2.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day2.py)

## Description

This problem requires asserting whether pulling a number of coloured cubes from a bag, then replacing and repeating, is possible. The number of cubes of each colour in the bag is known.

## Part 1

This problem is a simple logic problem with the majority of the difficult coming from correctly parsing the input.

## Part 2

Part 2 requires calculating the fewest number of cubes of each colour that are needed for each game that makes the game possible. We must return the sum of the power of each set of required cubes, where the power is equal to the numbers of red, green, and blue cubes multiplied together.

To achieve this, I made it possible for each DiceBag instance to track the maximum value of each colour dice encountered.


## Improvements

### Algorithms

There are no improvements possible for the time complexity of this problem.

### Software Engineering

I used a dictionary to map each dice bag's colour and count pair. This implementation detail was hidden from users by wrapping the dictionary in a class (DiceBag). This means that, in the future, if it was decided that there is a better data structure for this problem than a dictionary changes can be made without affecting the interface/functionality seen by users of the code.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday2.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>