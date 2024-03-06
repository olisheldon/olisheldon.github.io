---
title: Day 1
description: String parsing
layout: nested
---

# Day 1: Trebuchet?!

[link](https://adventofcode.com/2023/day/1)

[input](https://adventofcode.com/2023/day/1/input)

[code](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day1.py)

## Description

The first problem of this year's Advent Of Code involves string parsing.

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

The time complexity of this algorithm is `O(N**2)` average. 

Before Python 3.10, the worst case performance was O(NM) where N is length of longest string and M is length of shorter string. [Boyer–Moore String-Search](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string-search_algorithm)

As of Python 3.10, the worst case performance was improved to O(N + M) by using Crochemore and Perrin's [Two-way string-matching algorithm](https://en.wikipedia.org/wiki/Two-way_string-matching_algorithm). This is explained in [this write-up](https://github.com/python/cpython/blob/main/Objects/stringlib/stringlib_find_two_way_notes.txt).

If performance was an issue, I could utilize a sliding window that has limited size (and the length of substring we are searching for is [1, 5]). This would improve the time complexity of searching for the boundary digits.


### Software Engineering

From a software quality perspective, my solution has been written in a way that minimizes code reuse. However, this comes at the expense of some performance (reversing strings). I have also standardized the logic for parsing values from the calibration string, so if the calibration value was parsed differently, the required change could be made very easily.

For example, if in an imaginary part 3 we were told that reversed digits ("eno", "owt", ...) were negative integers this could be implemented by adding a new Enum value to ParseType. The use of the ParseType enum class to handle this logic has separated concerns.