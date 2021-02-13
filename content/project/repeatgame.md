+++
title = "Repeat Game"
date = 2020-11-01
[taxonomies]
tags = ["Rust", "Monte Carlo Search","Legion","SDL 2"]
+++

A turnbased time travel game.

This is one of my games written in Rust, Legion and SDL 2. The game is a turn based unit control game (think chess) where you take turns making moves. The idea is that once you have played one unit, the board will reset and you can play the next, then the first unit will repeat what you just did. So in other words, you are orchestrating what each unit should do, one at a time. The kicker is that you might end up saving a unit that was originally destroyed, but removing the oponents peices first. 

The big problem with this game was that I needed an AI to play against, an AI that could "think in teese wierd ways".

## Monte Carlo Search (MCS)

Initially I thought of hardcoding some behavoirs into the ai, but that did not turn out well. So i looked up how GO and Chess AIs could be implemented. I found Monte Carlo Tree Search. The idea is that you give the algorithm a set number of iterations it can do, and it then tries to find the next move to do that "seems the best at the time". This is all explained in details in the following video:

{{ youtube(id="UXW2yZndl7U") }}

Implementing MCS had one big problem, you need to iterate up and down in the tree, so each node needs to know its parent and each parent needs to know its children.
This is not easy to do in Rust because of its borrow rules, to solve this problem I implemented a [Node Zipper](https://en.wikipedia.org/wiki/Zipper_(data_structure))

## Tick Tac Toe

To test out the MCS I implemented a little tic tac toe game, and given enough iterations the AI never really looses.
All in all a very fun project.

## Will come back to it

This is one of the projects that I will come back to, I had the idea of Project Noah and I started that instead, but I will come back to this idea. There are a lot of things I know to do better with Legion and SDL 2 now.