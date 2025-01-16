---
title: "Day 3: Mull It Over"
description: Regular Expressions <br/> Difficulty ★
layout: nested
---

# Day 3: Mull It Over

[**link**](https://adventofcode.com/2024/day/3)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day3.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day3.py)

## Description

This problem involves parsing corrupted computer memory to find and execute valid multiplication instructions. The memory contains instructions in the format `mul(X,Y)` where X and Y are 1-3 digit numbers, but also includes various invalid characters and corrupted instructions that should be ignored.

```
xmul(2,4)%&mul[3,7]!@^do_not_mul(5,5)+mul(32,64]then(mul(11,8)mul(8,5))
```

## Part 1

The task is to find all valid `mul(X,Y)` instructions in the corrupted memory and sum their results. A valid instruction must:
- Start with "mul"
- Have exactly two numbers between 1-3 digits each
- Have proper parentheses and comma formatting

The solution uses a regular expression pattern `mul\\((\\d+),(\\d+)\\)` to match valid instructions:
- `mul\\(` matches the literal "mul("
- `(\\d+)` captures 1 or more digits
- `,` matches the literal comma
- Second `(\\d+)` captures the second number
- `\\)` matches the closing parenthesis

## Part 2

Part 2 introduces conditional instructions that enable or disable multiplication:
- `do()` enables future multiplications
- `don't()` disables future multiplications

The solution extends the regex pattern to `mul\\((\\d+),(\\d+)\\)|do\\(\\)|don't\\(\\)` to capture all three types of instructions along with their positions in the input string. It then processes instructions in order, keeping track of the enabled state and only executing multiplications when enabled.

## Improvements

### Algorithms

The solution has linear time complexity O(N) where N is the length of the input string, which is optimal for this problem as we need to examine each character at least once. The use of regular expressions provides a clean and efficient way to extract valid instructions.

### Software Engineering

Potential improvements could include:
1. Creating an Instruction class hierarchy to represent different instruction types
2. Separating the parsing logic from the execution logic
3. Adding input validation and error handling for malformed instructions
4. Using an enum for the enabled/disabled state

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday3.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
