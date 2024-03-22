---
title: "Day 5: If You Give A Seed A Fertilizer"
description: Intervals <br/> Difficulty ★★★
layout: nested
---

# Day 5: If You Give A Seed A Fertilizer

[**link**](https://adventofcode.com/2023/day/5)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day5.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day5.py)

## Description

This problem is about 1-to-1 mappings of integers.

```
seeds: 79 14 55 13

seed-to-soil map:
50 98 2
52 50 48

soil-to-fertilizer map:
0 15 37
37 52 2
39 0 15

fertilizer-to-water map:
49 53 8
0 11 42
42 0 7
57 7 4

water-to-light map:
88 18 7
18 25 70

light-to-temperature map:
45 77 23
81 45 19
68 64 13

temperature-to-humidity map:
0 69 1
1 0 69

humidity-to-location map:
60 56 37
56 93 4
```

The seed values, stated at the top, are passed through maps producing a 'location' integer output. Each map contains a number of mappings that may change the value of the seed. For example, the mapping `50 98 2` in the seed-to-soil map gives us a _destination range_ of 50, a _source range start_ of 98, and a _range length_ of 2. This creates a mapping of 98 -> 50 and 99 -> 51. If a value queries a map that is not captured within the _source range start_ and _destination range_ of any mapping contained within it, the value passes through unchanged (identity operation).

## Part 1

Part 1 has us query the seeds given at the start of the input one-by-one, and return the smallest resulting location number that corresponds to any of these initial seeds. 

Looking at the actual input, seeds such as `2637529854` give us small hope to represent this problem in memory. As such, optimizations need to be made in how we treat the mappings.

The optimization I used for part 1 was to realize that each mapping would offset the input value by the same amount within certain ranges of values, so mappings could be implemented as three values: `(lower, upper, offset)`, if a value queries a mapping such that `lower <= value < upper`, then the mapping updates the value to `value -> value + offset`. 

As there are only 20 seed values to query, this is efficient enough to quickly receive the answer.

## Part 2

For part 2, we no longer interpret the seeds as separate integer values. The seed values are instead pairs of values that represent an initial seed value and the number of seeds to consider after that. i.e. `79 14` correspond to the seeds values `79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92`.

Although a small change to the idea, this showed the inefficiency of my approach to solving part 1. For the actual input, the first seed range we would now consider is `2637529854 223394899`, corresponding to 223394899 seeds. For the approach taken in part 1, this would mean iterating `~1e9` times: Far too many, making this approach impossible.

Part 2 has essentially changed our input from individual seed values to intervals of values. I mirrored this change by changing my logic to handle mapping intervals of values (input seed intervals) by intervals of values (mappings). Therefore, when querying a mapping with a value, this value must be change to represent an interval of values. 

Each time that an interval of values queries a mapping, anywhere between 1 and 3 intervals may be produced depending on how the interval and mapping intersects. 

<!-- This easiest to show visually:

```
SHOWING VISUALLY!
``` -->

Implementing this was tricky as I had never considered a problem like this before, but after much trial and error I got the correct answer.

## Improvements

### Part 1

As part of my solution to part 2, I made sure that I could recreate my answer to part 1 using the same logic. In terms of which approach is better, for querying singular seeds the implementation I used in part 1 is superior as it is much simpler.

### Part 2

For part 2, once I had completed it, I experimented with adding some more ideas to further optimize the problem.

One idea I had was to add the ability to merge intervals. This operation would look like:

```
merge( Interval(200, 300), Interval(250, 350) ) -> Interval(200, 350) 
```

The idea behind this was to reduce the amount of redundant work and to prevent the exponential growth of the number of intervals. After I implemented this I found that this optimization made little to no difference to the running time of this particular problem.

Without optimization:
```bash
~/projects/my_projects/AdventOfCode23/python$ time python3 days/day5.py 
323142486
79874951

real    0m0.044s
user    0m0.016s
sys     0m0.017s
```
With optimization:
```bash
~/projects/my_projects/AdventOfCode23/python$ time python3 days/day5.py 
323142486
79874951

real    0m0.041s
user    0m0.032s
sys     0m0.000s
```

As we can see, this created ~10% faster completion rate for this problem. To show how this optimization would scale further with increasing input size, I increased the total number of maps (not mappings) by 100x. In this situation, we see:

Without optimization:
```bash
~/projects/my_projects/AdventOfCode23/python$ time python3 days/day5.py 
237346661
2826183

real    0m13.056s
user    0m13.037s
sys     0m0.011s
```
With optimization:
```bash
~/projects/my_projects/AdventOfCode23/python$ time python3 days/day5.py 
237346661
2826183

real    0m3.393s
user    0m3.384s
sys     0m0.001s
```

With this, we can see that this optimization does have a significant affect on the time complexity for this solution, but only for inputs that have a very large number of mappings/maps. 


### Algorithms

Algorithms for merging and manipulating intervals of integers.

### Software Engineering

I found a very nice Python feature:

Instead of writing `lower <= x < upper` to test if a value is within an interval/range, you can instead write `x in range(lower, upper)`. In this example, Python utilizes the generator-nature of the range object to perform a check within the range without calling for the memory required to create a list [lower, ..., upper - 1].

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday5.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>