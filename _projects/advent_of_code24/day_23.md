---
title: "Day 23: LAN Party"
description: Graph Theory / Set Analysis <br/> Difficulty ★★★
layout: nested
---

# Day 23: LAN Party

[**link**](https://adventofcode.com/2024/day/23)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day23.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day23.py)

## Description

Day 23 presents an interesting graph theory problem centered around analyzing computer networks. The input represents connections between computers in a network, where each line shows a bidirectional connection between two computers. We're asked to find specific patterns of connections to help locate a LAN party.

### Input Example

```
kh-tc
qp-kh
de-cg
ka-co
yn-aq
qp-ub
cg-tb
vc-aq
tb-ka
wh-tc
yn-cg
kh-ub
ta-co
de-co
tc-td
```

## Part 1

For part 1, we need to find all sets of three computers that are fully interconnected (forming a triangle in graph theory terms), then count how many of these sets contain at least one computer with a name starting with 't'.

### Graph Construction

The solution starts by parsing the input into an adjacency list representation using a defaultdict. Each computer becomes a vertex, and each connection becomes an undirected edge:

```python
adj = defaultdict(set)
for u, v in connections:
    adj[u].add(v)
    adj[v].add(u)
```

### Finding Connected Triples

To find all sets of three interconnected computers, we:
1. Iterate through all computers as potential first vertices
2. For each first computer, check its neighbors as potential second vertices
3. For each second computer, check its neighbors as potential third vertices
4. Verify that all three computers are connected to each other
5. Store unique sets using frozenset to avoid duplicates

```python
seen = set()
for first_computer in computers:
    for second_computer in adj[first_computer]:
        for third_computer in adj[second_computer]:
            three_computers = frozenset([first_computer, second_computer, third_computer])
            if len(three_computers) != 3:
                continue
            if (
                first_computer in adj[second_computer] and
                first_computer in adj[third_computer] and
                second_computer in adj[third_computer]
            ):
                seen.add(three_computers)
```

### Filtering Results

Finally, we filter the sets to only count those containing at least one computer starting with 't':

```python
def contains_element_starting_with_t(iter):
    return any(element.startswith('t') for element in iter)
return len(list(filter(lambda x: contains_element_starting_with_t(x), seen)))
```

## Part 2

Part 2 asks us to find the largest set of computers that are all fully connected to each other (a maximum clique in graph theory terms), and output its members in alphabetical order, separated by commas.

### DFS Approach

The solution uses depth-first search (DFS) to build increasingly larger sets of fully connected computers:

1. Start with each computer as a potential member of the maximum clique
2. For each computer, try to add neighbors that are connected to all current members
3. Keep track of all valid sets found
4. Finally, select the largest set and format it as required

```python
def dfs(u, required):
    key = tuple(sorted(required))
    if key in sets:
        return
    sets.add(key)
    
    for v in adj[u]:
        if v in required:
            continue
        if not all(v in adj[req] for req in required):
            continue
        dfs(v, {*required, v})

for computer in computers:
    dfs(computer, {computer})
return ",".join(sorted(max(sets, key=len)))
```

### Optimization

The solution uses several optimizations:
1. Uses sets for O(1) membership testing
2. Sorts and tuples the sets for efficient memoization
3. Early pruning of candidates that aren't fully connected
4. Skips redundant paths using memoization

## Improvements

### Memory Optimization

The current solution stores all intermediate sets in memory. For very large graphs, we could modify the code to only keep track of the maximum set found so far, reducing memory usage.

### Alternative Approaches

For Part 2, the Bron-Kerbosch algorithm could potentially be used as an alternative approach for finding the maximum clique, though the current solution performs well enough for the given input sizes.

### Software Engineering

The solution is clean and well-structured, with clear separation between parsing, part 1, and part 2 logic. The use of defaultdict and set operations makes the code both efficient and readable.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday23.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>