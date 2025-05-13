---
title: "Day 13: Claw Contraption"
description: Linear Equations <br/> Difficulty ★★★
layout: nested
---

# Day 13: Claw Contraption

[**link**](https://adventofcode.com/2024/day/13)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day13.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day13.py)

## Description

In this problem, we have a series of claw machines at an arcade, each with two buttons (A and B) that move the claw by specific amounts on the X and Y axes. Button A costs 3 tokens to press, while button B costs 1 token. Each machine has a prize at a specific location, and we need to determine the minimum number of tokens required to win all possible prizes.

## Part 1

For part 1, we need to solve a system of linear equations to determine if a prize can be won and, if so, with how many tokens. The core challenge is to find the number of A presses and B presses needed to position the claw exactly over the prize.

For each claw machine, we have:
- Button A moves the claw by (a_dx, a_dy)
- Button B moves the claw by (b_dx, b_dy)
- The prize is at position (prize_x, prize_y)

We need to find non-negative integers a_presses and b_presses such that:
```
a_presses * a_dx + b_presses * b_dx = prize_x
a_presses * a_dy + b_presses * b_dy = prize_y
```

The brute force approach I implemented initially checks all combinations of A and B presses (up to 100 of each, as per the problem statement) and finds the minimum token cost (3*a_presses + 1*b_presses) for any valid solution.

## Part 2

In part 2, the problem statement reveals that there was a unit conversion error, and all prize positions need to be adjusted by adding 10^13 to both X and Y coordinates. The brute force approach is no longer feasible with such large numbers.

Instead, I switched to solving the system of linear equations directly. Using Cramer's rule:

```
det = a_dx * b_dy - a_dy * b_dx
a_presses = (prize_x * b_dy - prize_y * b_dx) / det
b_presses = (a_dx * prize_y - a_dy * prize_x) / det
```

A solution exists only if:
1. The determinant is non-zero (the movements are linearly independent)
2. Both a_presses and b_presses are non-negative integers

With this approach, we can efficiently solve part 2 without iterating through billions of combinations.

## Algorithms

### System of Linear Equations

The core of this problem involves solving a system of linear equations with two variables. I used two approaches:

1. **Brute Force (Part 1)**: Checking all possible combinations of button presses up to a reasonable limit.
2. **Analytical Solution (Part 2)**: Using Cramer's rule to directly solve the system of equations.

This is a good example of how understanding the mathematical foundations of a problem can lead to vastly more efficient solutions.

### Software Engineering

The solution is structured with separate functions for:
1. `find_min_tokens`: The brute force approach for part 1
2. `solve_linear_equation`: The analytical solution for part 2
3. `parse`: Handling the input parsing logic in one place

This separation of concerns makes the code more maintainable and allows reuse of common functionality. The parsing function is particularly helpful as it transforms the text input into a structured format that both part 1 and part 2 can use.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday13.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
