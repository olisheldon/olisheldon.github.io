---
title: "Day 11: Plutonian Pebbles"
description: Simulation with linked list and optimization <br/> Difficulty ★★
layout: nested
---

# Day 11: Plutonian Pebbles

[**link**](https://adventofcode.com/2024/day/11)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day11.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day11.py)

## Description

This problem asks us to track the transformation of a series of numbered stones that follow specific rules when we "blink":

1. If a stone's value is 0, it changes to 1
2. If a stone's value has an even number of digits, it splits into two stones (left and right halves of the digits)
3. Otherwise, the stone's value is multiplied by 2024

## Part 1

For part 1, we need to determine how many stones we'll have after 25 blinks.

I implemented a linked list approach, where each stone is represented as a node. The linked list is a natural fit for this problem because stones can split into two, which would require expensive insertions in an array-based implementation.

The `blink_linked_list` function applies the transformation rules to each stone:
- For stones with value 0, simply update the value to 1
- For stones with an even number of digits, split the value into two nodes
- For other stones, multiply the value by 2024

After 25 iterations of this transformation, I count the total number of stones in the linked list.

## Part 2

Part 2 dramatically increases the challenge: we need to determine the number of stones after 75 blinks. The linked list approach from Part 1 would be too memory-intensive, as the number of stones grows exponentially.

To solve this, I created a more efficient `StoneTally` class that uses a Counter to track how many stones have each value. Instead of creating individual nodes for each stone, we just track the counts of each unique stone value.

This optimization allows us to handle the exponential growth efficiently. The `blink` method applies the same transformation rules but updates the counter instead of manipulating individual nodes.

Key optimizations:
- Using a Counter to track stone counts by value
- Caching digit lengths for better performance
- Processing stones with the same value all at once

## Improvements

### Algorithm Optimization

The time complexity for Part 1 is O(n·2^b) where n is the initial number of stones and b is the number of blinks, as the number of stones can double with each blink in the worst case.

For Part 2, using the Counter-based approach gives us a time complexity of O(u·b) where u is the number of unique stone values and b is the number of blinks. This is much more efficient since u << n·2^b for large values of b.

### Software Engineering

The solution demonstrates good separation of concerns:
- A class-based approach for the optimized solution
- Caching for frequently accessed values
- Consistent application of the transformation rules between implementations

One potential improvement would be to unify the approaches between Part 1 and Part 2, perhaps using the more efficient Counter-based approach for both parts.

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday11.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday11.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
