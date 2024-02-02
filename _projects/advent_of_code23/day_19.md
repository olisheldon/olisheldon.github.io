---
title: "Day 19: Aplenty"
description: Trees, intervals <br/> Difficulty ★★★
layout: nested
---

# Day 19: Aplenty

[**link**](https://adventofcode.com/2023/day/11)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day11.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day11.py)

## Description

This problem presents parts, defined by four integer attributes, and workflows through which these parts move. 

These workflows ultimately accept or reject a part based on conditions placed on the part's attributes. These attributes are four categories:

 - x
 - m
 - a
 - s

This means that each part has form Part(x=x_i, m=m_i, a=a_i, s=s_i). Workflows are made of ordered rules that apply conditions to a part. The rules test one of the rules categories, judging whether a part within the category is greater than or less than a value. Each rule also has an outcome, for when/if the part passes the condition imposed by the rule. This outcome can be a new workflow (for the part to be processed further) or a final outcome, that will accept ('A') or reject ('R') the part.

An example workflow may look like `px{a<2006:qkq,m>2090:A,rfg}`. In this example, the workflow is named 'px', has 2 rules (a<2006:qkq,m>2090), and 1 default outcome (new workflow 'rfg').

There are two possible outcomes from each rule within a workflow: 

 - PASS: If the part passes the rules condition, the part follows the rules output which can be A (accept), R (reject), or the name of a new workflow to process the part further. If a part is sent to a new workflow, the part is processed by that workflow *and never returns*.
 - FAIL: If there is another rule in the workflow, process the part with this rule. Otherwise, as no rules matched the part and we are at the end of the workflow, follow the workflows _default outcome_ shown at the end of the workflow.

## Part 1

For part 1 we must, for each given part, figure out whether a part will be accepted or rejected by the workflows and then return a property of these accepted parts.

We are given 200 parts to consider in the input file.

I first modelled the system of workflows as a tree. This is tempting because of the structure of the workflows: A workflow is made of rules (nodes of the tree), with each rule linking to another rule based on a condition placed on the part that is being processed.

The idea of a default workflow outcome came with a tricky design decision for how to handle this. I decided to handle this by interpreting default workflow outcomes using the same Rule interface that all of the workflow rules implemented, only with the rules always passing. This allowed for nicer, more general code.

Using this approach and building the tree by interpreting the workflows as lists of nodes, I solved part 1.

## Part 2

For part 2, we are told to consider the workflows differently. Instead of querying the workflow with a part to receive a single outcome, we must find the number of parts with all combinations of possible part category values within a certain range will be accepted by the workflows.

This change makes my approach to part 1 obsolete as the size of the input has increased dramatically. The part category value ranges within which we must consider all combinations is `[0, 4000]`. This increases the number of parts we need to consider to `4000 ** 4 = 256000000000000`.To put this into perspective, part 1 had us consider 200 parts. This number of parts would produce an unfeasibly long runtime for the problem if we continue our strategy outlined in part 1. Instead, we need to change our workflows to operate on intervals of numbers.

Similar to [**day 5**](https://olisheldon.github.io/projects/adventofcode23/day_5.html), we use intervals to our problem tractable. Instead of rules passing or failing a part, they instead split an interval of parts into multiple intervals. Each of these new intervals will then follow the workflow in which it must go.

I decided to implement this new strategy using recursion within my container coordinating all of the individual workflows. The base cases for this recursion are if a workflowm results in an ACCEPT ('A') or REJECT ('R'). 

When passed to a workflow, each interval is queried by all of the rules contained by it. Each rule splits an interval into a 'pass' subinterval and 'fail' subinterval. These new subintervals must then be sent to different workflows, or returned as they have been assigned an outcome.

<!-- [comment]: <> (VISUALIZE DECISION TREE) -->


To reduce redundant code, I removed my solution to part 1 and solved it using my solution to part 2.

## Improvements

<!-- ### Part 1 -->

### Part 2

I used the same Interval data structure to complete day 5. In that problem I used the merging of Intervals to decrease the runtime. Is this possible for this problem? 

The answer is no, because we are never considering a list of intervals, only a single interval at a time.

<!-- ### Algorithms -->

### Software Engineering

Throughout writing my solution, I found my code suffering from 'drilling' as many of the classes I created to solve this problem just passed their work further down a chain if classes with similar interfaces until the class at the bottom finally handled it. I tried to rewrite my solution to prevent this, but I think I was only partly successful in this.

The classes I created are too dependent on each other. For example, the Operator enum class I created for handling the '<' and '>' logic has a method that has direct knowledge of the Interval interface. This felt natural while writing this code, but I am not sure of the best way to remedy this.


## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday19.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>