---
title: Backtracking
description: Subsets, Combinations, Permutations
layout: nested
---

# Backtracking

## Subsets

### Without Duplicates

Question: What are all possible distinct subsets given a list of distinct integers?

For each element we have a choice: to include in the subset or not -> Decision tree

[comment]: <> (treeart, print(binary_edge([], binary_edge([1], binary_edge([1,2], [1,2,3], [1,2]), binary_edge([1], [1,3], [1])), binary_edge([],binary_edge([2],[2,3],[2]),binary_edge([],[3],[])))))
```
subsets([1,2,3])
```
```
                 ╭─────────────[]───────────────╮
         ╭──────[1]────────╮              ╭────[]──────╮   
    ╭─[1, 2]───╮        ╭─[1]──╮       ╭─[2]──╮     ╭─[]──╮
[1, 2, 3]   [1, 2]   [1, 3]   [1]   [2, 3]   [2]   [3]   []
```

For this decision tree, each list takes O(N) and athere are `2**N` lists, therefore `O(N2**N)` time complexity and `O(N)' memory complexity (height of tree).

```python
# Time: O(n * 2^n), Space: O(n)
def subsets_without_duplicates(nums: list[int]) -> list[list[int]]:
    subsets, curSet = [], []
    helper(0, nums, curSet, subsets)
    return subsets

def helper(i, nums: list[int], curSet: list[int], subsets: list[list[int]]) -> None:
    if i >= len(nums):
        subsets.append(curSet.copy())
        return
    
    # decision to include nums[i]
    curSet.append(nums[i])
    helper(i + 1, nums, curSet, subsets)
    curSet.pop()

    # decision NOT to include nums[i]
    helper(i + 1, nums, curSet, subsets)
```

### With Duplicates

Question: What are all possible distinct subsets given a list of integers that are not necessarily distinct?

Firstly sort, as the `O(NlogN)` of this operation will be dominated by `O(N2**N)` time complexity 

```python
# Time: O(n * 2^n), Space: O(n)
def subsets_with_duplicates(nums: list[int]):
    nums.sort()
    subsets, curSet = [], []
    helper2(0, nums, curSet, subsets)
    return subsets

def helper2(i, nums: list[int], curSet: list[int], subsets: list[list[int]]) -> None:
    if i >= len(nums):
        subsets.append(curSet.copy())
        return
    
    # decision to include nums[i]
    curSet.append(nums[i])
    helper2(i + 1, nums, curSet, subsets)
    curSet.pop()

    # decision NOT to include nums[i]
    while i + 1 < len(nums) and nums[i] == nums[i + 1]:
        i += 1
    helper2(i + 1, nums, curSet, subsets)

```


## Combinations

Question: Given two integers N & K, what are all possible combinations of values in [1, N] of size K? (i.e. N choose K)

DIAGRAM!



```python
# Time: O(k * 2^n)
def combinations(n: int, k: int) -> list[list[int]]:
    combs = []
    helper(1, [], combs, n, k)
    return combs

def helper(i: int, cur_comb: list[int], combs: list[list[int]], n: int, k: int) -> None:
    if len(cur_comb) == k:
        combs.append(cur_comb.copy())
        return
    if i > n:
        return
    
    # decision to include i
    cur_comb.append(i)
    helper(i + 1, cur_comb, combs, n, k)
    cur_comb.pop()
    
    # decision to NOT include i
    helper(i + 1, cur_comb, combs, n, k)
```

or improved efficiency!

```python
# Time: O(k * C(n, k))
def combinations2(n: int, k: int) -> list[list[int]]:
    combs = []
    helper2(1, [], combs, n, k)
    return combs

def helper2(i: int, cur_comb: list[int], combs: list[list[int]], n: int, k: int) -> None:
    if len(cur_comb) == k:
        combs.append(cur_comb.copy())
        return
    if i > n:
        return
    
    for j in range(i, n + 1):
        cur_comb.append(j)
        helper2(j + 1, cur_comb, combs, n, k)
        cur_comb.pop()
```


## Permutations

Question: What are all distinct permutatinos of a list of integers?

```python
# Time: O(n^2 * n!)
def permutations_recursive(nums: list[int]) -> list[list[int]]:
    return helper(0, nums)
        
def helper(i: int, nums: list[int]) -> list[list[int]]:   
    if i == len(nums):
        return [[]]
    
    res_perms = []
    perms = helper(i + 1, nums)
    for p in perms:
        for j in range(len(p) + 1):
            p_copy = p.copy()
            p_copy.insert(j, nums[i])
            res_perms.append(p_copy)
    return res_perms
```

`O(N! * N**2)`

```python
# Time: O(n^2 * n!)
def permutations_iterative(nums: list[int]) -> list[list[int]]:
    perms = [[]]

    for n in nums:
        next_perms = []
        for p in perms:
            for i in range(len(p) + 1):
                p_copy = p.copy()
                p_copy.insert(i, n)
                next_perms.append(p_copy)
        perms = next_perms
    return perms
```