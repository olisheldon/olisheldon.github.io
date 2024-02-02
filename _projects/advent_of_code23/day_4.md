---
title: "Day 4: Scratchcards"
description: Sets <br/> Difficulty ★
layout: nested
---

<style>
g { color: Green }
</style>

# Day 4: Scratchcards

[**link**](https://adventofcode.com/2023/day/4)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day4.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day4.py)

## Description

This problem mimics checking winning scratchcards for winning numbers. Our input is a number of scratchcards, each of which has its own set of winning numbers.

## Part 1

The number of winning numbers per scratchcard is the intersection of the sets of scratch card numbers and winning numbers. This is easily done Python's <g>set</g> data structure. Each scratch card scores `2**(N - 1)` points, where N is the number of winning scratchcard numbers on the scratchcard. We must return the sum of all scratch cards scores.

## Part 2

In part 2, winning numbers on a scrathccard wins more scratchcards equal to the number of winning numbers it has. i.e. card 10 with 5 matching numbers adds scratchcards 11, 12, 13, 14, 15 to your scratchcards. (Cards will never make you copy a card past the end of the table.) This process repeats until all scratchcards have been claimed. We must return the total number of scratchcards we process.

The means that scratchcards no longer earn points; Instead, the number of winning numbers on each card wins you one copy of the next cards. 

## Improvements

### Algorithms

My solution to part 2 is O(N) time complexity, where N is the number of scratchcards. As we must iterate through the total number of scrathcards, this can not be improved.

### Software Engineering

Part 2 has too much logic in the method. This should be pulled out into its own class, but the problem is so simple that this is not needed.


## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday4.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>