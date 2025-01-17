---
title: "Day 5: Print Queue"
description: Graph Dependencies & Topological Sort <br/> Difficulty ★★★
layout: nested
---

# Day 5: Print Queue

[**link**](https://adventofcode.com/2024/day/5)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day5.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day5.py)

## Description

This problem deals with dependency ordering in a print queue system, where certain pages must be printed before others. The input consists of:

1. A set of ordering rules in the format X|Y, meaning page X must be printed before page Y
2. A series of print jobs, each consisting of a list of page numbers

The challenge is to determine which print jobs are already correctly ordered according to all applicable rules, and then to fix those that aren't.

```
47|53
97|13
...

75,47,61,53,29
97,61,53,29,13
...
```

## Part 1

Part 1 asks us to identify which print jobs are already in the correct order and sum the middle page numbers of these valid jobs. A job is considered valid if for any two pages X and Y in the job, if there's a rule X|Y, then X appears before Y in the job's page list.

The solution takes a graph-based approach:
1. Build a dependency graph using the ordering rules
2. For each print job, verify that all page orderings respect their dependencies
3. Extract and sum the middle numbers from valid jobs

Key optimizations:
- Using sets to store dependencies for O(1) lookup
- Early termination of validation once any invalid ordering is found

## Part 2

Part 2 requires us to fix the incorrectly ordered print jobs by reordering their pages to satisfy all dependencies, then sum the middle numbers of these reordered jobs.

The solution uses a comparator-based sorting approach:
1. Build a cache of relative orderings between any two pages
2. Create a custom comparator function using this cache
3. Sort each invalid job using the comparator
4. Sum the middle numbers of the reordered jobs

This approach effectively implements a form of topological sorting, ensuring all dependencies are satisfied in the final ordering.

## Improvements

### Algorithms

The solution demonstrates the use of:
- Graph representation for dependencies
- Custom comparators for sorting
- Caching for optimization

Alternative approaches could include:
- Using a full topological sort algorithm
- Implementing Kahn's algorithm
- Using a dependency matrix representation

### Software Engineering

Notable Python features used:
- `defaultdict` for clean graph representation
- `cmp_to_key` for custom sorting
- List comprehensions for data processing
- Efficient set operations for dependency checks

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday5.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>