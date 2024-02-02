---
title: "Day 7: Camel Cards"
description: Sorting <br/> Difficulty ★
layout: nested
---

# Day 7: Camel Cards

[**link**](https://adventofcode.com/2023/day/7)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day7.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day7.py)

## Description

Model a card game called 'Camel Cards', a game like Poker but designed to be played on a camel(?).

In Camel Cards, a player gets a number of hands, with an integer bid amount for each hand. A hand is an ordered list of five standard playing cards.

These hands are ordered according to a set of rules, and each hand is assigned a 'rank' according to its position in the ordered hands (weakest hands get a lower rank starting from 1).

The ordering is defined by two properties of a hand:

 - Type
 - Card value

A hand is ordered first on the Type. For hands of the same Type, a strict ordering is enforced by comparing the cards within each hand in order, with the larger card defining the stronger hand.

### Type:

The five cards in a hand are assigned a type, similar to [poker](https://en.wikipedia.org/wiki/List_of_poker_hands).

In order of weakening hands:

 - Five of a kind: AAAAA
 - Four of a kind: AA8AA
 - Full house: 23332
 - Three of a kind: TTT98
 - Two pair: 23432
 - One pair: A23A4
 - High card: 23456

## Part 1

We must play a game of Camel Cards with a given set of hands. We parse our set of hands from the input. We then follow the rules of Camel Cards and return the total winnings, where the total winnings of a game is defined as the sum of `rank * bid` for each hand.

As playing a game of Camel Cards is really just sorting, I made use of default Python sorting behaviour to complete this part.

## Part 2

A joker is introduced to replace the JACK card.
Joker cards can represent any card. Within a hand, they represent the card that maximises the type of the hand. However, the Joker is the weakest card in the Card value ordering.

We must play a game of Camel Cards again and return the total winnings with this new card.

## Improvements

My solution has optimal time complexity.

### Algorithms

I use the built-in Python sort command, which has `O(NlogN)` time complexity. In this, I am assuming that the comparison between two of my `Hand` classes has constant time complexity, which is the case.

### Software Engineering

I used a [Mixin](https://en.wikipedia.org/wiki/Mixin) instead an abstract base class because it was not possible to inherit from abstract base class and IntEnum as this would cause errors about metaprogramming. The Mixin approach achieves the same effect of a shared interface, but without the promise of implementation in all *abstract* methods. 

My logic for generating the possible hands of cards in part 2 is unclear. There should be a much shorter, easier to follow recursive solution that I could use instead.


## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday7.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>