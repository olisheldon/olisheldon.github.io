---
title: Day 7
description: Difficulty ★
layout: nested
---

# Day 7: Camel Cards

[**link**](https://adventofcode.com/2023/day/7)

[**input**](https://adventofcode.com/2023/day/7/input)

[**code**](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day7.py)

## Description

Model a card game called 'Camel Cards' (like Poker but designed to be played on a camel(?))

In Camel Cards, a player gets a number of hands, with an integer bid amount for each hand. A hand is an ordered list of five standard playing cards.

These hands are ordered according to a set of rules, and each hand is assigned a 'rank' according to its position in the ordered hands (weakest hands get a lower rank starting from 1).

The ordering is defined by two properties of a hand:

 - Type
 - Card value

A hand is ordered first on the Type. For hands of same Type, a strict ordering is enforced by comparing the cards within each hand in order, with the larger card defining the stronger hand.

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

### Card value

For two hands of the same Type, the hands are strictly compared by comparing (in order) the cards. For each pair of cards between each hand, the hand that has the larger card within the pair is stronger.

## Part 1

We must play a game of Camel Cards with a give set of hands and return the total winnings. The total winnings of a game is defined as the sum of rank * bid for each hand.

## Part 2

A joker is introduced to replace the JACK card.
Joker cards can represent any card. Within a hand, they represent the card that maximises the type of the hand. However, the Joker is the weakest card in the Card value ordering.

We must play a game of Camel Cards again and return the total winnings with this new card.

## Improvements

This problem is more difficult in setting up the logic of sorting than worrying about time complexity.

### Algorithms

The built in Python sorting will use an O(NlogN) sorting algorithm.

### Software Engineering

My logic for generating the possible hands of cards in part 2 is unclear. There should be a much shorter, easier to follow recursive solution.
