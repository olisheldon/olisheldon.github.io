---
title: Dynamic Programming
description: 1D, 2D
layout: nested
---

# Dynamic Programming

## 1D Dynamic Programming

The Fibonacci sequence can be easily solved more efficiently using 1-dimensional dynamic programming techniques.

### Brute Force

```python
def brute_force(n) -> int:
    if n <= 1:
        return n
    return brute_force(n - 1) + brute_force(n - 2)
```

[comment]: <> (treeart, print(binary_edge(5,binary_edge(4,binary_edge(3,binary_edge(2,1,0), 1), binary_edge(2,1,0)),binary_edge(3,binary_edge(2,1,0), 1))))
```
          ╭───────5──────╮
     ╭────4───╮       ╭──3──╮
  ╭──3──╮   ╭─2─╮   ╭─2─╮   1
╭─2─╮   1   1   0   1   0    
1   0              
```

Time complexity: O(2**N) caused by repeated work. This is improved by using memoization.

### Top-Down Dynamic Programming

Continued use of recursion, but store results to a cache to prevent repeated work.

```python
# Memoization
def memoization(n: int, cache: dict[int, int]) -> int:
    if n <= 1:
        return n
    if n in cache:
        return cache[n]

    cache[n] = memoization(n - 1) + memoization(n - 2)
    return cache[n]
```

Time complexity: O(N)

### Bottom-Up Dynamic Programming

The 'true' dynamic-programming solution.

```python
def dp(n: int) -> int:
    if n < 2:
        return n

    dp = [0, 1]
    i = 2
    while i <= n:
        dp[0], dp[1] = dp[1], dp[0] + dp[1]
        i += 1
    return dp[1]
```

Time complexity: O(N)
Memory complexity: O(1)

## 2D Dyanmic Programming

Question: What are the number of unique paths from top left to bottom right while only moving down or right.

### Brute Force

```python
def brute_force(coords: tuple[int, int], grid_dims: tuple[int, int]) -> int:
    row, col = coords
    rows, cols = grid_dims

    if row == rows or col == cols:
        return 0
    if row == rows - 1 and col == cols - 1:
        return 1
    
    return (brute_force((row + 1, col), grid_dims) +  
            brute_force((row, col + 1), grid_dims))

print(brute_force((0, 0), (4, 4)))
```

Time complexity: O(2 ** sum(grid_dims))
Space: O(sum(grid_dims))

### Top-Down Dynamic Programming

```python
from collections import defaultdict


def memoization(coords: tuple[int, int], grid_dims: tuple[int, int], cache: dict[tuple[int, int], int]):
    row, col = coords
    rows, cols = grid_dims

    if row == rows or col == cols:
        return 0
    if cache[coords] > 0:
        return cache[coords]
    if row == rows - 1 and col == cols - 1:
        return 1
    
    cache[coords] = (memoization((row + 1, col), grid_dims, cache) +  
        memoization((row, col + 1), grid_dims, cache))
    return cache[coords]

print(memoization((0, 0), (4, 4), defaultdict(int)))
```
Time complexity: O(n * m)
Memory complexity: O(n * m)

### Bottom-Up Dynamic Programming

```python
def dp(grid_dims: tuple[int, int]):
    rows, cols = grid_dims

    prevRow = [0] * cols

    for row in range(rows - 1, -1, -1):
        curRow = [0] * cols
        curRow[cols - 1] = 1
        for col in range(cols - 2, -1, -1):
            curRow[col] = curRow[col + 1] + prevRow[col]
        prevRow = curRow
    return prevRow[0] 
```

TODO: DIAGRAM

Time complexity: O(n * m)
Memory complexity: O(m), where m is num of cols