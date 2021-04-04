+++
title = "Robotcards: Week 4"
date = 2021-04-04
[taxonomies]
tags = ["Rust", "Legion"]
[extra]
image="../static/images/robotcards/week4.PNG"
description="Walking the skeleton"
+++

## Progress this week

This week has been easter vacation, i expected that I would get a lot more done than normal. But instead I have spend time with family.

I have finished about 21 points, which is a lot more than usual, so maybe i should expected that I can do 13 points in a week instead of 10.


## Sprite batch

One thing that I should have thought of doing a lot earlier is sprite batches as a component. Meaning a single entity can have a sprite batch that is a stack of sprites that will be rendered in order (first on bottom).
As an example a card can cotain a background, a color and an icon, before I would make one entity pr sprite, now i can have a single entity (which also is how I think of a card, as one entity) but with multiple sprites.
This too a bit of rewrite of the render.

## Premature optimization

When I had to redo a bit of the render I thought to myself, wow this code looks really unoptimized. What i do is I find every single sprite to render, then i add them to a list and then sort that list based on the sprites position and its "z-index". This is to prevent a background sprite from overlapping a foreground sprite. I took a break and thought how I could improve it, and came up with all kinds of advanced ways of improving it, including a priority heap solution... but I thought, i better profile my game to see where it is slow.
I used AMD uProf because that is what seemed to work on windows. The results where ... wierd... the most expensive function was something from the library, looks like it was what schedules all the different systems in the ECS. I doug into it for like an hour... then i thought, how much cpu is this game actually using?
On my AMD Ryzen 3600 i takes up 0.1% CPU and 30mb ram, so I think that ANY optimization i would do to the renderer right now would be premature.
I am constantly surpriced at how fast things can get in Rust or just in programming in general when you don't have to deal with IO.

## Team select

This week I made a team selection screen. One of my favorite feature of the game Into The Breach is that you can pick 3 robots to make up your team for the run. It gives a lot of varirity and gives control in the randomness of a "rouge-like". In slay the spire, you select a "person" to play as, but the biggest difference between the players are the cards that they can get.
In my game my first idea was to also have 3 units that you control, but while designeing that select screen, I thought "what if these players are not the direct units, but only control the starting cards and what kind of cards you get offered as rewards as the game goes on".

The current design is that the team members are "workers" on the game run, so a programmer gets a lot of basic movement cards, since they can move the features around, while the artist gets cards that can create things and so on.

## Overworld

I also made the overworl this week. The overworld lets you move from skirmish to skirmish, and shows you the next options you have for skirmishes.
I will go more into detail on this once I have the core gameplay more narrowed down.

## What is fun?

I am excited for the deckbuilding and creating a starter deck for each run.

## What is not fun?

There are only 2 level types and the goals are still not clear, so I have to work on that.

## Next week

I think that the next week will focus on:

1. Abilities
2. Picking rewards / Deck Building
3. Levels and Goals

While i am doing that I will work on sprites and card art.