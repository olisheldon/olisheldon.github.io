---
title: Day 4
description: Set intersections, stack.
layout: nested
---

# Day 4: Scratchcards

[link](https://adventofcode.com/2023/day/4)

## Description

This problem mimics checking winning scratchcards. We are given a number of scratchcards with their own winning numbers.

## Part 1

Each scratch scores 2**(n - 1) points for each winning number. We return the sum of all scratch cards scores.

My approach represents each scratchcard and its numbers as sets and returns the size of their intersection to get the number of winning numbers.

## Part 2

The idea of scratch cards being worth is points is discarded. Instead, the number of winning numbers on each card wins you one copy of the next cards. i.e. card 10 with 5 matching numbers adds scratchcards 11, 12, 13, 14, 15 to your scratchcards. (Cards will never make you copy a card past the end of the table.)

We must process all of the original and copied scratchcards until no more scratchcards are won. We then return the number of scratchcards we had to process to end the sequence.

## Improvements

### Algorithms

My solution to part 2 is currently O(N) time complexity, where N is the number of scratchcards. However, this assumes that the number of winning numbers per scratchcard is much less than the number of scratchcards. If the number of winning numbers is instead unbound, this becomes an O(N**2) problem. 

### Software Engineering

part_2() has too much logic in the method. This should be pulled out into its own class.
