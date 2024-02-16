---
title: Day 1
description: String parsing, scanning, and manipulation
layout: nested
---

# Day 1: Trebuchet?!

[link](https://adventofcode.com/2023/day/1)


## Part 1

This is a very simple problem that involves parsing the first and final digits from a string of characters, then interpreting these digits as a two digit number. The result is the sum of these digits for all strings.

## Part 2

Part 2 is largely the same, except substrings that are the english word for a digit ALSO count.


## Improvements

### Algorithms

Python features a very nice for finding substrings

```python
>>> "example string" in "this is an example string"
True
```

The time complexity of this algorithm is O(N) average. 

Before Python 3.10, the worst case performance was O(NM) where N is length of longest string and M is length of shorter string. [Boyer–Moore String-Search](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string-search_algorithm)

As of Python 3.10, the worst case performance was improved to O(N + M) by using Crochemore and Perrin's [Two-way string-matching algorithm](https://en.wikipedia.org/wiki/Two-way_string-matching_algorithm). This is explained in [this write-up](https://github.com/python/cpython/blob/main/Objects/stringlib/stringlib_find_two_way_notes.txt).

To improve performance I could utilize a sliding window that has limited size (and the length of substring we are searching for is [3, 5]). This would improve the constants in our time complexity.


### Software Engineering

There is quite a lot of repeated code in _parse_edge_digits_only and _parse_edge_digits_and_strings. This could be removed by pulling the common code out into its own method.