---
title: Day 19
description: INCOMPLETE
layout: nested
---

# Day 19: Aplenty

[link](https://adventofcode.com/2023/day/11)

[input](https://adventofcode.com/2023/day/11/input)

[code](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day11.py)

## Description

This problem presents parts, defined by four integer attributes, and workflows through which these parts move. 

These workflows ultimately accept or reject a part based on conditions placed on the part's attributes. These attributes are four categories:

 - x
 - m
 - a
 - s

So a part may look like Part(x=x_i, m=m_i, a=a_i, s=s_i). The workflows are made of rules that apply conditions to a part. The rules test one of the rules categories, judging whether a part within the category is greater than or less than a value. Each rule also has an outcome, for when the part passes its condition. This outcome can be a new workflow (for the part to be processed further) or a final outcome, that will accept ('A') or reject ('R') the part.

A workflow looks like `px{a<2006:qkq,m>2090:A,rfg}`. In this example, the workflow is named 'px', has 2 rules (a<2006:qkq,m>2090), and 1 default outcome (new workflow 'rfg').

There are two possible outcomes from each rule within a workflow: 

 - PASS: If the part passes the rules condition, the part follows the rules output which can be A (accept), R (reject), or the name of a new workflow to process the part further. If a part is sent to a new workflow, the part is processed by that workflow *and never returns*.
 - FAIL: If there is another rule in the workflow, process the part with this rule. Otherwise, as no rules matched the part and we are at the end of the workflow, follow the workflows _default_ rule (that has no condition attributed).

## Part 1

For part 1 we must, for each given part, figure out whether a part will be accepted or rejected by the workflows and then return a property of these accepted parts.

We are given 200 parts to consider in the input file.


In my first attempt at solving this puzzle, I tried to model the system of workflows as a tree. This is tempting because of the structure of the workflows: A workflow is made of rules (nodes of the tree), with each rule linking to another rule based on a condition placed on the part that is being processed.

Using this approach, I quickly solved part 1.

## Part 2

For part 2, we are told to consider the workflows differently. Instead of querying the workflow with a part to receive a single outcome, we must find the number of parts with all combinations of possible part category values within a certain range will be accepted by the workflows.

This change makes my approach part 1 obsolete as the size of the input has increased dramatically. The part category value ranges within which we must consider all combinations is 0 and 4000. This increases the number of parts we need to consider to `4000 ** 4 = 256000000000000`.To put this into perspective, part 1 had us consider 200 parts. This number of parts creates an intractable problem if we continue our strategy outlined in part 1. Instead, we need to change our workflows to operate on intervals of numbers.

Similar to [day 5](link), using intervals makes our problem tractable.


## Improvements

### Part 1

### Part 2

### Algorithms

### Software Engineering

My code suffers from 'drilling', many of the classes I created to solve this problem just pass the work further down the chain until a class finally handles it. This felt like the natural way to write it when I began.

The classes I created are also too dependent on each other, for example, the Operator enum class I created for handling the '<' and '>' logic has a method that has direct knowledge of the Interval interface. Should this have been handled differently?
