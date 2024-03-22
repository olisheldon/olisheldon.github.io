---
title: "Day 6: Wait For It"
description: SUVAT <br/> Difficulty ★
layout: nested
---

# Day 6: Wait For It

[**link**](https://adventofcode.com/2023/day/6)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day6.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day6.py)

## Description

This problem simulates a number of toy boat races. Each race is defined by the amount of allowed time for that race. 

Each boat participating in a race must choose to pause for x time units before then setting off at a speed of x. A boat wins the race if they move the furthest (largest distance).

The input to this problem is a number of time, distance pairs. Each of these represents a race (defined by the time), and a distance achieved in the race. Our task is to determine the number of ways that the distance in each race could be beaten, and multiply this value for all races.

## Part 1

This problem is very easy, and boils down to the formula `distance = t * (T - t)`, where T is the race time and t is the time spent pressing the button.

The size of the problem we are tying to solve is also very small, with race times being ~10 seconds. This removes the need for optimisation.

## Part 2

Part 2 asks us the same problem, but to parse the input as one large race by concatenating the race times and distances into one large race.

This creates a race of time ~ 1e8. This still produces a small input that we can brute force in a reasonable time (~10 seconds).

## Improvements

For the input given, this solution is sufficient. If the race times were much longer, or there were many more of them, many optimisations could be made:

 - Exploit the symmetry of problem (eg. in a 10 second race holding for 2 seconds and holding for 8 seconds achieve the same distance)
 - Find the time used in each race for the target distance using binary search `(O(N) -> O(logN) search)`
 - Solve the quadratic equation: `t * (T - t) = distance` for a constant time solution.

### Algorithms

I used brute force because the input size is small.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday6.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>