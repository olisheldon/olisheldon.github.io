---
title: Day 12
description: INCOMPLETE
layout: nested
---

# Day 12: Hot Springs

[link](https://adventofcode.com/2023/day/12)

[input](https://adventofcode.com/2023/day/12/input)

[code](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day12.py)

## Description

This problem presents rows of springs containing springs that are either damaged, operational, or unknown. Unknown springs can be either damaged or operational. For each row, we are also given a configuration in the form of a list of integers. This configuration give us the size of each contiguous group of damaged springs listed in the order those groups appear in the row. This list always accounts for every damaged spring, and each number is the entire size of its contiguous group (that is, groups are always separated by at least one operational spring: #### would always be 4, never 2,2). 

## Part 1

For each row, calculate the number of possible arrangements for the row configuration.

This problem can be solved using either dynamic programming problem or recursion, I use recursion for simplicity.

The most difficult part of this problem is working out the decision tree.

### Base Cases

The base cases of the recursion are if

 - The subproblem has no springs left
 - The subproblem has no configuration left

When there are no springs left in the subproblem, this path of recursion can only be valid if configuration is also empty. 

When there is no configuration left, this path of recursion can only be valid if there are no more damaged springs within the subproblems list of springs, else it is invalid.

### Decisions

If we have passed the base cases, we must make decisions based on the state of the springs and configuration. In the following we can either treat an unknown spring as an operational spring, or if we are at the start of a damaged block.

#### Decision Tree

[comment]: <> (treeart, print(binary_edge("(springs, configuation)","(springs[1:], configuration)","(springs[configuration[0] + 1 : ], configuration[1:])"))
```
              ╭────────────────(springs, configuation)─────────────────╮
              |                                                        |                            
              1                                                        2                            
              |                                                        |                            
(springs[1:], configuration)                 (springs[configuration[0] + 1 : ], configuration[1:])
```


If the first spring in our springs subproblem is operational or unknown, we pretend the unknown spring is operational and recurse on the `springs[1:], configuration` subproblem.

If the first spring in our springs subproblem is damaged or unknown, we treat the unknown spring as a damgaged spring and check a number of conditions are true:

 - The number of possible springs we are considering must be less than number of springs left
 - The block of damaged springs can't contain operational spring
 - (There are no springs left, so number of springs left equals the configuration) OR (if there are springs afterwards the next spring must not be damaged)

If all of these conditions are met, we recurse on the subproblem `springs[configuration[0] + 1 : ], configuration[1:]`. This is done because we are looking for new damaged blocks and we know springs[configuration[0] + 1] is unknown or operational from our our final condition. We also found a damaged block, so remove the first config.

## Part 2

Part 2 slightly modifies the input to the problem, but maintains the logic of the recursion. We reinterpret the input as being folded, such that an input of `[springs] -> [springs + ? + springs + ? + springs + ? + springs + ? + springs]`, a folding factor of five.

This is simple to change, but shows the slowness of this recursive solution without caching. To calculate these larger problems in a reasonable time, caching had to implemented. In Python this is remarkably easy with the use of functools.lru_cache, where lru_cache stands for 'least-recently-used cache'. This decorator wraps a function and implements memoization for you based on the calls to the function. Each function call has its signature saved to its return value, if the same signature is called again it returns the cached value.

This was a very easy implementation of caching, and allowed the completion of part 2 with minimal code change.

## Improvements

The use of recursion without memoization in part 1 gives a times complexity of O(2 ** N) where N is the length of configuration. With memoization this reduces to O(N) as we avoid repeated work, but this comes at the cost of increased memory complexity.

This problems seems like it is solvable using dynamic programming. This would not reduce the time complexity from the linear solution presented here, but would reduce the memory complexity to linear (or maybe even constant if a bottom-up dynamic programming solution is possible!).

### Software Engineering

I made sure to implement my recursion on tuple representations of the springs and configuration subproblems to avoid Pythonic issues of passing mutable containers to functions. I think my code is well structured as minimal code changes were needed to solve part 2, and the code changes did not require changing the method calls for solving part 1.