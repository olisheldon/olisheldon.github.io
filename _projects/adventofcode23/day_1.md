---
title: Day 1
description: String parsing, scanning, and manipulation
layout: nested
---

# Day 1: Trebuchet?!

[link](https://adventofcode.com/2023/day/1)

[input](https://adventofcode.com/2023/day/1/input)

[code](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day1.py)

## Description

As the first problem of this year's Advent Of Code, this problem is very easy.

## Part 1

This problem requires parsing a 'calibration value' from a string. A calibration value is parsed as the first and final digits from a string of characters, and then interpreted as a number by concatenating the digits to form a two digit number. 

In the problem, we are given many of strings from which we must find the calibration value. We should return the sum of all calibration values.

## Part 2

For part 2, the problem is made more difficult by including strings such as 'one', 'two', etc in considering digits within each line. To modify my solution for this change, I performed the checking for the integers and strings ('one', 'two', ...) through a dictionary of strings to integers. This allowed the same strategy to be used for part 1 and part 2.

However, the use of the same strategy for both parts comes at a performance hit.

## Improvements

### Algorithms

Python features a very nice syntax for finding substrings that I used to search for both the strings and integers within each calibration line.

```python
>>> "example string" in "this is an example of a string"
True
>>> "1" in "this is an example of 1 string"
True
```

The time complexity of this algorithm is O(N) average. 

Before Python 3.10, the worst case performance was O(NM) where N is length of longest string and M is length of shorter string. [Boyer–Moore String-Search](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string-search_algorithm)

As of Python 3.10, the worst case performance was improved to O(N + M) by using Crochemore and Perrin's [Two-way string-matching algorithm](https://en.wikipedia.org/wiki/Two-way_string-matching_algorithm). This is explained in [this write-up](https://github.com/python/cpython/blob/main/Objects/stringlib/stringlib_find_two_way_notes.txt).

To improve performance I could utilize a sliding window that has limited size (and the length of substring we are searching for is [1, 5]). This would improve the time complexity of searching for the boundary digits to O(N) instead of O(N**2) by searching for substrings. (Explain why)


### Software Engineering

