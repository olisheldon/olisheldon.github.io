---
title: "Day 20: Pulse Propagation"
description: Graphs <br/> <br/> Difficulty ★★★
layout: nested
---

# Day 20: Pulse Propagation

[**link**](https://adventofcode.com/2023/day/20)

[**input**](https://adventofcode.com/2023/day/20/input)

[**code**](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day20.py)

## Description

This problem requires modelling a system of communication modules connected to each other. These modules communicate through pulses that can be HIGH or LOW. Each module has a number of destination modules that it sends its ouput pulse to.

### Module Types

#### Flip-Flop

 - Symbol: %
 - State: On / Off
 - Default state: Off

'Flip-flop modules (prefix %) are either on or off; they are initially off. If a flip-flop module receives a high pulse, it is ignored and nothing happens. However, if a flip-flop module receives a low pulse, it flips between on and off. If it was off, it turns on and sends a high pulse. If it was on, it turns off and sends a low pulse.'
(From AoC day 20 description)

#### Conjunction

 - Symbol: &
 - State: On / Off
 - Default state: Off

Conjunction modules (prefix &) remember the type of the most recent pulse received from each of their connected input modules; they initially default to remembering a low pulse for each input. When a pulse is received, the conjunction module first updates its memory for that input. Then, if it remembers high pulses for all inputs, it sends a low pulse; otherwise, it sends a high pulse. 
(From AoC day 20 description)

#### Starter modules

 - Begin the 

## Part 1

## Part 2

## Improvements

### Part 1

### Part 2

### Algorithms

### Software Engineering
