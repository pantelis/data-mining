---
title: Ensemble Methods
---

# Ensemble Methods [^1]

[^1]: The problem statement is from [Freund and Schapire 1999](https://cseweb.ucsd.edu/~yfreund/papers/IntroToBoosting.pdf) 

A horse-racing gambler, hoping to maximize his winnings, decides to create a computer program
that will accurately predict the winner of a horse race based on the usual information (number of
races recently won by each horse, betting odds for each horse, etc.). 

To create such a program, he asks a highly successful expert gambler to explain his betting strategy. Not surprisingly, the expert
is unable to articulate a grand set of rules for selecting a horse. 

On the other hand, when presented
with the data for a specific set of races, the expert has no trouble coming up with a “rule of thumb”
for that set of races (such as, “Bet on the horse that has recently won the most races” or “Bet on
the horse with the most favored odds”). Although such a rule of thumb, by itself, is obviously very
rough and inaccurate, it is not unreasonable to expect it to provide predictions that are at least a
little bit better than random guessing. Furthermore, by repeatedly asking the expert’s opinion on
different collections of races, the gambler is able to extract many rules of thumb.

In order to use these rules of thumb to maximum advantage, there are two problems faced by
the gambler: 

1. First, how should he choose the collections of races presented to the expert so as to
extract rules of thumb from the expert that will be the most useful? 

2. Second, once he has collected
many rules of thumb, how can they be combined into a single, highly accurate prediction rule?

The answer to these questions is of great importance to machine learning and the category of algorithms that try to address them are called _ensemble learning_ methods.